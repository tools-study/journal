# Interfacial Nucleation Review

---

## Abstract

The liquid-to-solid transition (LST) of ribonucleoprotein (RNP) condensates—scaffolded by RNA-binding proteins such as Fused in Sarcoma (FUS), TAR DNA-binding protein 43 (TDP-43), heterogeneous nuclear ribonucleoprotein A1 (hnRNPA1), and α-synuclein—is the proximal molecular event in a family of neurodegenerative diseases that includes amyotrophic lateral sclerosis (ALS), frontotemporal lobar degeneration (FTLD), and Parkinson's disease (Hurtle et al. 2023; Song 2023; Lu et al. 2024). Between 2022 and 2025, three independent experimental traditions—solid-state nuclear magnetic resonance (NMR), multidimensional super-resolution microscopy, and air–water interface sum-frequency generation—converged on a counterintuitive finding: the pathogenic cross-β cores that nucleate during condensate maturation do not form uniformly in the condensate interior, but are catalyzed at the condensate surface (Linsenmeier et al. 2022; Shen et al. 2023; Emmanouilidis et al. 2024; He et al. 2023; Maltseva et al. 2023). If this observation is quantitatively correct—and not a methodological artifact of the air–water interfaces used in vitro—then the primary knob for controlling LST in a disease-relevant system is not the molecular composition of the condensate interior but its surface-area-to-volume ratio (S/V), the interfacial energy γ, and the surface coverage by interfacial clusters (Folkmann et al. 2021; Gouveia et al. 2022). This paper formalizes the interfacial nucleation hypothesis as a falsifiable quantitative framework. We derive physicochemical relations and that together predict a linear relation between the logarithm of the nucleation rate of surface cross-β assembly and the molar specific interfacial area, `ln(J) = α − β·(S/V)` with β > 0. We then propose a single, pre-registered, statistically powered experiment that titrates S/V by a factor of approximately 100 using microfluidic droplet-size engineering of FUS and TDP-43 condensates in controlled oil-free buffers, reads out the cross-β nucleation rate by solid-state NMR, single-droplet surface-enhanced Raman scattering, single-molecule FRET, and correlative cryo-electron tomography, and is falsified if surface-area-proportional variation contributes less than ten percent of the variance in J across the titration range. If the hypothesis survives, we argue that a new therapeutic class—engineered Pickering-type interfacial c-mods—is immediately accessible, because surface tension can be reduced by surface-active peptides, antibodies, or RNA aptamers without disrupting the functional interior of the condensate (Hernandez-Candia et al. 2024; Sanchez-Burgos et al. 2025; Oh et al. 2025). The proposed experiment is designed to advance, refute, or refine an account of pathogenic RNP condensate maturation.

---

## 1. Introduction

### 1.1 The Liquid-to-Solid Crisis as a Surface Problem

ALS, FTLD, and a growing family of related proteinopathies are characterized pathologically by insoluble, β-sheet-rich cytoplasmic and nuclear inclusions of RNA-binding proteins whose normal function is to organize RNA metabolism through reversible phase separation into dynamic, liquid-like condensates (Hurtle et al. 2023; Naskar et al. 2023; Song 2023). The transition from reversible liquid condensate to insoluble amyloid is not a textbook polymerization; it is a material-state transition in a finite, finely bounded droplet phase, governed by the interplay of bulk protein–protein interactions, solvent thermodynamics, and—critically—interfacial physics (Zhou et al. 2024; Jülicher et al. 2023; Mukherjee et al. 2023). Bulk thermodynamics predicts that nucleation of a β-sheet phase within a condensate should occur preferentially where the protein concentration is highest, namely the interior (Szała-Mendyk et al. 2023). The experimental record from 2022 to 2025 contradicts that prediction.

### 1.2 What Was Established and What Was Left Unanswered

A prior survey of structural and molecular biology placed the LST in its full context, identified Jawerth et al.'s aging-Maxwell-fluid framework and Emmanouilidis et al.'s solid-state NMR detection of surface β-sheet in FUS as the key experimental advances, and catalogued classical nucleation theory as the appropriate mathematical substrate. That survey left open the most consequential question: whether the surface β-sheet observation is the rate-limiting step of pathogenic LST, or a downstream byproduct of a primarily bulk-driven process. If surface nucleation is rate-limiting, the implications are quantitative and therapeutic: droplet geometry and interfacial chemistry become design variables for condensate-modifying therapeutics (c-mods) (Mitrea et al. 2022; Sanfeliu-Cerdán et al. 2025; Jeon et al. 2025). If not, the surface signal is phenomenological and the therapeutic lever must act on bulk multivalency.

### 1.3 Recent Surface Nucleation Discoveries

Five independent lines of experimental evidence now support the interfacial-nucleation model. First, solid-state NMR on aging FUS droplets shows that cross-β signals are concentrated at the droplet surface (Emmanouilidis et al. 2024). Second, direct micropipette and rheological measurement shows that FUS droplets develop a rigid, solid-like outer shell that propagates inward over hours to days (Shen et al. 2023). Third, multidimensional super-resolution microscopy with a fluorogenic amyloid probe localizes amyloid nanoaggregates specifically to the FUS condensate surface and not the interior (He et al. 2023). Fourth, direct spectroscopic imaging of the FUS low-complexity domain at a hydrophobic air–water interface reveals solid film formation at protein concentrations approximately 600-fold below the bulk condensate saturation (Maltseva et al. 2023). Fifth, and most directly testable for therapeutic translation, coating the interface of hnRNPA1 condensates with an added surfactant blocks interior fibril formation, and α-synuclein acts as a Pickering-type surface aggregator that nucleates heterotypic fibrils of TDP-43 from the droplet boundary (Linsenmeier et al. 2022; Dhakal et al. 2023). Parallel work on P granules in *C. elegans* established Pickering-stabilizing nanoclusters—MEG-3 proteins adsorbed at the condensate surface—as a native, evolved regulator of condensate material state and coarsening kinetics (Folkmann et al. 2021; Hoffmann et al. 2022). These five strands, from solid-state NMR to cell biology, are mutually reinforcing but have never been integrated into a single falsifiable quantitative model. That integration is the aim of this paper.

### 1.4 Scope

This manuscript performs three tasks. First (Section 2), it develops a theoretical framework for interfacial nucleation of cross-β structure in RNP condensates that is internally consistent with classical capillarity, heterogeneous nucleation theory, and Gibbs adsorption thermodynamics, and that yields new equations and it specifies one falsifiable, pre-registered experiment designed to discriminate interfacial from bulk nucleation using established readouts. Third (Sections 4–7), it organizes the supporting evidence, discusses the therapeutic consequences for a new class of interfacial c-mods, analyzes refinement of the experimental method, and identifies the open questions that survive a positive result. Throughout we explicitly mark the most uncertain steps.

---

## 2. Theoretical Foundation: Interfacial Thermodynamics of Ribonucleoprotein Condensates

### 2.1 Why Surfaces Matter More Than Volumes for Finite Condensates

The surface-area-to-volume ratio of a spherical condensate of radius *R* is `S/V = 3/R`. For a typical cellular condensate of *R* ≈ 1 μm, S/V ≈ 3 μm⁻¹; for the small synthetic Pickering-stabilized condensates engineered by Oh et al. (2025) at *R* ≈ 50 nm, S/V ≈ 60 μm⁻¹—a twentyfold change. A kinetic process that scales with surface area rather than volume therefore dominates at the nanoscale and is overwhelmed by bulk processes at the microscale; the disease-relevant steady state in neurons likely spans both regimes (Naskar et al. 2023; Ripin et al. 2023). This simple geometry argument is the starting point for the model.

### 2.2 F409 — Gibbs Adsorption Isotherm for Disordered-Protein Condensates

For a condensate in equilibrium with a dilute phase of RNA-binding protein at chemical potential μ, the Gibbs adsorption isotherm relates the change in interfacial tension γ to the surface excess concentration Γ of protein adsorbed at the interface:

```math
\Gamma = -\frac{1}{RT}\left(\frac{\partial \gamma}{\partial \ln c}\right)_{T,P}
```

where *c* is the bulk protein activity of the dilute phase, *R* is the gas constant, and *T* is absolute temperature. For multicomponent RNP condensates, Γ partitions across disordered regions and folded domains, and an extended form applies:

```math
\Gamma_\text{total} = \sum_i \nu_i \Gamma_i, \qquad \sum_i \nu_i = 1
```

with ν_i the mole fraction of species *i* adsorbed at the interface and Γ_i its partial surface excess. Experimental validation of this isotherm in condensates has been achieved for Ddx4 by sessile-drop and flicker-spectroscopy measurements that resolve how net charge and aromatic content shift γ (Holland et al. 2023; Pyo et al. 2022). A key prediction, confirmed for two-component condensates, is that super-stoichiometric surface enrichment of the majority species linearly reduces γ (Pyo et al. 2022). Equation F409 is the formal lever: any molecular species whose surface activity lowers γ (a surface-active IDR, an engineered peptide, an RNA aptamer) will deplete the nucleation barrier only if the nucleation mechanism is surface-driven. This is the first half of a falsifier.

### 2.3 F410 — Heterogeneous Nucleation Rate at the Condensate Interface

For a two-dimensional critical cross-β nucleus that forms at a flat condensate interface, the Volmer–Weber heterogeneous nucleation geometry modifies the classical bulk barrier ΔG*_bulk by a contact-angle factor *f*(θ) ≤ 1:

```math
J_\text{surf} = J_0 \cdot A_\text{int} \cdot \exp\!\left[ -\frac{f(\theta)\,\Delta G^{*}_\text{bulk}}{k_B T}\right]
```

with

```math
f(\theta) = \tfrac{1}{4}\,(2-3\cos\theta + \cos^{3}\theta)
```

where θ is the contact angle of the nascent β-sheet phase with the condensate–cytoplasm interface, *A*_int is the total interfacial area, *J*_0 is a kinetic prefactor encoding attempt frequency and molecular volume, and *k*_B*T* is thermal energy. For θ = π (non-wetting nucleus), *f*(θ) = 1 and the surface provides no benefit; for θ → 0 (perfect wetting), *f*(θ) → 0 and the nucleation barrier collapses. The direct experimental measurement of hnRNPA1 condensate surface catalysis of fibril formation and the surfactant-based inhibition of that catalysis imply θ < π for pathogenic cross-β phases (Linsenmeier et al. 2022). In the bulk, the interior nucleation rate scales as `J_bulk ∝ V·exp(−ΔG*_bulk/k_B T)`. The ratio *J*_surf / *J*_bulk therefore scales with *f*(θ)-dependent barrier lowering and with the surface-area-to-volume ratio:

```math
\frac{J_\text{surf}}{J_\text{bulk}} = \frac{A_\text{int}}{V} \cdot \frac{J_{0,\text{surf}}}{J_{0,\text{bulk}}} \cdot \exp\!\left[\frac{(1-f(\theta))\,\Delta G^{*}_\text{bulk}}{k_B T}\right]
```

When this ratio exceeds unity, surface nucleation dominates—which is precisely what the NMR, super-resolution, and micropipette data on FUS observe (Emmanouilidis et al. 2024; He et al. 2023; Shen et al. 2023).

### 2.4 F411 — Line Tension and the 2D Critical Nucleus at a Condensate Interface

Because the condensate interface is a quasi-two-dimensional fluid, a β-sheet nucleus at the interface is bounded by a one-dimensional line rather than a two-dimensional surface. Its free energy is

```math
\Delta G_\text{2D}(n) = -n\,\Delta \mu_\text{2D} + \lambda \cdot P(n)
```

where Δμ_2D > 0 is the free-energy gain per monomer incorporated into the 2D cross-β raft at the interface, λ is the line tension (units of energy per length), and *P*(*n*) is the perimeter of an *n*-monomer nucleus. For a circular 2D nucleus of radius *r*, *n* = π*r*²ρ_2D with ρ_2D the areal density of the cross-β phase and *P*(*n*) = 2π*r*. The critical radius is

```math
r^{*} = \frac{\lambda}{\rho_\text{2D}\,\Delta \mu_\text{2D}}, \qquad \Delta G_\text{2D}^{*} = \frac{\pi \lambda^{2}}{\rho_\text{2D}\,\Delta \mu_\text{2D}}
```

so the nucleation barrier scales as λ² and is independent of the bulk surface tension γ of the condensate–cytoplasm boundary. This distinction matters: capillary-wave-based measurements yield γ, but the relevant free-energy barrier for pathogenic LST is set by λ, an independent quantity that can be extracted from statistical mechanics of the 2D phase diagram (Chew et al. 2023; Sanchez-Burgos et al. 2025). Experimental estimates of line tension in lipid-monolayer β-sheet domains support λ ≈ 1–3 pN (Lu et al. 2022; Ren et al. 2024), corresponding to critical radii of a few nanometers at physiological supersaturation—consistent with the nanoscale aggregates detected at the FUS droplet surface (He et al. 2023).

### 2.5 F412 — Capillary-Wave Spectrum and the Coupling to β-Sheet Nucleation

Interfaces of liquid-like condensates support thermally excited capillary waves whose amplitude spectrum is

```math
\left\langle |h_q|^{2} \right\rangle = \frac{k_B T}{\gamma q^{2} + \kappa q^{4} + \rho g}
```

where *h*_q is the Fourier amplitude of the height fluctuation at wavevector *q*, γ is interfacial tension, κ is bending rigidity, ρ is density, and *g* an effective gravitational term (negligible at the sub-micron scale). Flicker spectroscopy of nuclear condensates yields γ ≈ 10⁻⁶–10⁻⁴ N m⁻¹ and κ in the tens-of-*k_BT* range, approaching criticality as composition is tuned toward the two-phase boundary (Williamson et al. 2025; Pyo et al. 2023). Large-amplitude capillary modes transiently concentrate surface-active IDR segments to supersaturation, providing a kinetic pathway by which the β-sheet nucleus of F411 can form. The coupling is

```math
J_\text{surf} \propto \int_{0}^{q_\text{max}} \Theta\!\left[\,\langle |h_q|^{2}\rangle - h_\text{crit}^{2}\,\right] q \, dq
```

where Θ is the Heaviside step, *h*_crit is the minimum amplitude sufficient to expose a cross-β-prone segment at the interface, and *q*_max is an ultraviolet cutoff near the molecular scale. Two predictions emerge: (i) approaching the critical composition, γ falls, capillary amplitudes diverge, and *J*_surf rises sharply; (ii) bending rigidity provides a stabilizing term at high *q*, suppressing short-wavelength fluctuations and hence finite-size β-sheet nuclei. Both predictions align with the critical-like interfacial behavior reported for engineered and endogenous nuclear condensates (Pyo et al. 2023; Williamson et al. 2025).

### 2.6 F413 — Pickering Coverage Threshold for Nucleation Suppression

If the condensate surface is partially coated by surface-active clusters or molecules—natural MEG-3 Pickering nanoclusters in P granules (Folkmann et al. 2021), synthetic protein cages at condensate interfaces (Oh et al. 2025), or surfactant molecules (Linsenmeier et al. 2022)—the accessible interfacial area for β-sheet nucleation is reduced by a coverage factor (1 − θ_p). The surface nucleation rate becomes

```math
J_\text{surf}(\theta_p) = J_\text{surf}(0)\,(1-\theta_p)^{n_\text{cluster}}
```

where *n*_cluster is an effective cluster size (for random site blocking, *n*_cluster = 1; for cooperative coverage, *n*_cluster > 1). The critical Pickering coverage for half-suppression is

```math
\theta_p^{*} = 1 - 2^{-1/n_\text{cluster}}
```

For the experimentally estimated four-fold reduction of PGL-3/RNA condensate surface tension by MEG-3 at physiological coverage (Folkmann et al. 2021), and assuming the Kelvin-like coupling `γ(θ_p) ≈ γ_0(1−θ_p)` that has been confirmed for two-component condensates (Pyo et al. 2022), *θ*_p* ≈ 0.25–0.5 is sufficient for order-of-magnitude nucleation suppression. This is the quantitative therapeutic lever.

### 2.7 F414 — Statistical Detection of Surface-Area-Proportional Nucleation

The experiment (Section 3) fits the regression `ln(J_observed) = α − β·(S/V) + ε`. Under the null hypothesis β = 0, the pathogenic LST is not interfacially dominated. The minimum detectable β with power 1 − β_II at significance α_I across *k* droplet-size regimes with replication *r* per regime, given residual variance σ², is

```math
\beta_\text{min} = (z_{\alpha_I/2} + z_{\beta_{II}})\,\sigma \,\big/\,\sqrt{r\,k\,\text{Var}(S/V)}
```

with *z* standard normal quantiles. For realistic experimental parameters (*k* = 6 regimes spanning 0.3 μm ≤ *R* ≤ 30 μm, *r* = 8 replicates, σ = 0.3 in ln(J) units, α_I = 0.01, power = 0.9), *β*_min ≈ 0.05 μm, giving a regression sensitivity more than an order of magnitude below the β values predicted by F410 under the interfacial hypothesis. The experiment is therefore statistically powered to detect the predicted effect if it exists and to falsify it otherwise.

---

## 3. The Falsifiable Experiment

### 3.1 Central Hypothesis and Null

**H1 (interfacial nucleation).** The rate *J* of pathogenic cross-β nucleation in FUS and TDP-43 condensates scales linearly with the logarithm of the specific interfacial area:

```math
\ln J = \alpha - \beta \cdot (S/V), \qquad \beta > 0
```

with a 95% confidence interval excluding zero, across at least two orders of magnitude in S/V.

**H0 (bulk nucleation).** β = 0 (to within the sensitivity of F414); cross-β nucleation rate is independent of droplet geometry and depends only on bulk protein concentration, temperature, and composition.

**Pre-registered falsification criterion.** If β·Var(S/V) / Var(ln *J*) < 0.10 across the titration range, surface nucleation is not the rate-limiting mechanism and H1 is rejected.

### 3.2 Experimental Design — Titrating S/V by 100-fold

The core experimental innovation is the systematic control of S/V across at least two orders of magnitude in a single protein-concentration regime. Four complementary techniques jointly enable this:

1. **Microfluidic droplet-size engineering** produces monodisperse populations of FUS or TDP-43 condensates with tunable *R* from 0.3 to 30 μm in oil-free aqueous-aqueous micro-compartments, building on the PhaseScan platform established for mapping condensate phase diagrams (Arter et al. 2022).
2. **Pickering-stabilized nano-condensates** (Oh et al. 2025) deliver condensate droplets down to 50–100 nm with controlled surface stabilization by engineered protein cages; these provide the small-droplet end of the S/V range.
3. **Size-selective centrifugation and electric-field sorting** homogenize droplet populations post-formation.
4. **Agarose-stabilized biphasic samples** (Emmanouilidis et al. 2024) provide a separate, independent high-S/V benchmark with documented NMR readout.

### 3.3 Protein Constructs

- **FUS full-length wild type** expressed and purified as in Shen et al. (2023).
- **FUS G156E and R244C ALS mutants** with documented accelerated surface β-sheet formation (Emmanouilidis et al. 2024).
- **TDP-43 full-length wild type** (Sharma et al. 2024).
- **TDP-43 A315T and M337V ALS/FTD mutants** (Li et al. 2022; Arseni et al. 2024).
- **Structure-preserving fluorescent fusions** (EGFP, mCherry) validated by coarse-grained simulations to preserve phase behavior (Veevers et al. 2024).
- **Matched RNA-binding-deficient FUS ΔRGG** as a mechanistic control for the RNA-dependent suppression of surface maturation (Emmanouilidis et al. 2024).

### 3.4 Readouts

Six orthogonal measurements quantify *J* per condition:

1. **Solid-state NMR of ¹³C-labeled protein at high S/V** (agarose-biphasic): direct quantitation of β-sheet chemical shifts versus time and droplet geometry (Emmanouilidis et al. 2024).
2. **Single-droplet surface-enhanced Raman scattering (SERS)** with plasmonic nanoparticles at the droplet boundary, providing conformation-specific signals per droplet (Avni et al. 2022).
3. **Multidimensional super-resolution microscopy** (SR-SMLM with solvatochromic dye and SMLM with fluorogenic amyloid probe) localizes β-sheet nanoaggregates spatially and kinetically, the method that first established surface nucleation in FUS (He et al. 2023).
4. **Single-molecule FRET at the droplet interior vs. surface** distinguishes conformational states of monomeric IDRs between bulk and interface (Galvanetto et al. 2023; Wen et al. 2025).
5. **Correlative cryo-focused-ion-beam / cryo-electron tomography** captures fibril distribution in situ at 6–8 Å resolution (Zhou et al. 2025); template-matching with deep-learning segmentation enables per-droplet fibril counts.
6. **Mass photometry** detects nanoscale precursor clusters whose bulk-concentration dependence calibrates *J*_0 (Ray et al. 2023; Kar et al. 2022).

### 3.5 Time Course and Analysis

Each (protein, mutant, S/V) condition is followed for up to 14 days at 4 °C and 37 °C, with early time points (1–24 h) resolved at 2-h intervals and later points (24–336 h) at 24-h intervals. *J* is extracted from the initial slope of β-sheet-fraction-versus-time curves by global fitting to the Finke–Watzky two-step nucleation–autocatalysis model augmented with an interfacial term. A Bayesian hierarchical model pools across mutants with protein-specific priors derived from FUS and TDP-43 literature fibril structures (García-Pardo et al. 2023; Todd et al. 2024; Bartolomé-Nafría et al. 2024).

### 3.6 Pre-Specified Controls

- **Negative (α-control):** identical construct in agarose-free, high-volume bulk sample (S/V → 0 limit) should yield ln(*J*) ≈ α.
- **Positive surface-nucleation control:** FUS G156E condensates, which are known to have accelerated surface maturation (Emmanouilidis et al. 2024), should shift α upward but leave β unchanged if the mutation alters interfacial chemistry (λ) rather than S/V.
- **Pickering-suppression control:** addition of the MEG-3-analog surface-active peptide designed by Sanchez-Burgos et al. (2025) should reduce *J* at fixed S/V by a factor consistent with F413 (*θ*_p*).
- **Surfactant-coating control:** replication of the Linsenmeier et al. (2022) experiment on hnRNPA1 (fibril suppression by interfacial surfactant) in the same microfluidic platform to cross-validate methodology.
- **Bulk viscoelastic control:** FRAP-ID measurement of γ and interior viscosity (Santamaria et al. 2024) to confirm that the titration does not change bulk viscoelasticity or γ beyond the pre-registered tolerance.

### 3.7 Falsification Outcomes

| Observation | Interpretation |
|---|---|
| β > 0 with 95% CI excluding 0, at least 10% variance explained | H1 supported; surface nucleation dominant |
| β indistinguishable from 0 | H1 rejected; bulk cross-linking dominant |
| β > 0 but small (1–5% variance) | Mixed regime; rate-limiting step context-dependent |
| Pickering peptide reduces *J* without changing S/V | Independent validation of F413 |
| G156E shifts α but not β | Mutation acts via λ (line tension) at fixed S/V |
| G156E shifts β | Mutation alters surface-area utilization, not line tension |

---

## 4. Supporting Evidence

### 4.1 Surface-Driven Nucleation in FUS Is Replicated Across Methods

Solid-state NMR on aged FUS condensates demonstrates that β-sheet chemical shifts emerge selectively from surface-proximal low-complexity domain residues, with maturation kinetics accelerated approximately three-fold in agarose-biphasic samples with higher S/V relative to monophasic samples (Emmanouilidis et al. 2024). Independent micropipette rheology demonstrates that solid-like properties originate at the FUS droplet boundary and propagate centripetally (Shen et al. 2023). Multidimensional super-resolution microscopy resolves amyloid-positive nanodomains localized exclusively to the droplet surface, expanding under aging to form a low-diffusivity shell (He et al. 2023). Air–water interface sum-frequency generation and surface-specific spectroscopy of the FUS low-complexity domain at 600-fold below bulk saturation reveals solid film formation mediated by hydrophobic interactions (Maltseva et al. 2023). These four methods, each with different physical observables, converge on the same geometric answer.

### 4.2 Evidence in TDP-43 Is Consistent but Less Mature

Molecular dynamics simulations of TDP-43 condensates identify faster β-sheet transitions in near-interfacial regions than in the bulk core, with arginine-rich client peptides accelerating nucleation and poly-U RNA / HSP70 chaperone slowing it—both through interfacial-rather-than-bulk mechanisms (Sanchez-Burgos et al. 2025). Cryo-EM structures of full-length TDP-43 amyloid fibrils show polymorphism of the C-terminal low-complexity core (Sharma et al. 2024), and the recent observation that pathogenic TDP-43 fibrils in FTLD Type C are heteromeric with annexin A11 (Arseni et al. 2024) suggests that client-protein adsorption at the condensate interface is a plausible nucleating event, parallel to α-synuclein's Pickering-nucleator behavior on TDP-43 droplets (Dhakal et al. 2023). ANXA11's N-terminal fragment, which co-assembles with TDP-43, has the physicochemical profile expected of an interfacial Pickering agent.

### 4.3 Cross-Condensate Generalization

The interfacial-nucleation motif has now been established in four independent RNP systems: FUS (Shen et al. 2023; Emmanouilidis et al. 2024; He et al. 2023), hnRNPA1 (Linsenmeier et al. 2022), α-synuclein in biomolecular condensates (Lipiński et al. 2022; Dada et al. 2023), and TDP-43 via heterotypic α-synuclein contact (Dhakal et al. 2023). Strunge et al. (2023) and Roeters et al. (2023) show that α-synuclein adopts interface-bound helical conformations at both hydrophobic air–water and lipid interfaces, and that interfacial packing promotes aggregation. Lu et al. (2022) demonstrate the same phenomenon for Aβ(16–22). Ren et al. (2024) generalize the 2D mechanism to six model proteins (including insulin, lactoferrin, and hemoglobin), establishing interfacial amyloid assembly as a broad phenomenon, not a curiosity of IDP-based condensates.

### 4.4 Pickering Stabilization Is a Native Biological Control

MEG-3 nanoclusters adsorb at the *C. elegans* P granule surface, reduce surface tension fourfold without changing interior viscosity, and prevent coalescence over hours—the evolved biological instance of a Pickering-coverage mechanism (Folkmann et al. 2021; Hoffmann et al. 2022). This is a proof of principle that surface-active biomolecules modulate condensate dynamics without disrupting interior biochemistry.

### 4.5 Condensate Metastability Separates Fibril-Driving from Condensation-Driving Interactions

The A1-LCD experiments of Das et al. (2025) show that interfaces of condensates, not interiors, are the rate-limiting site of fibril formation, and that designed mutations that increase condensate metastability suppress fibril formation in cells carrying ALS-causing mutations. This result directly links the interfacial hypothesis to a therapeutic outcome and confirms F413 in a cellular context.

---

## 5. Therapeutic Implications — Interfacial c-mods as a New Class

### 5.1 The Design Space

F413 identifies an accessible therapeutic lever: surface-active agents that adsorb to the condensate interface at coverage *θ*_p > *θ*_p* suppress pathogenic nucleation by an order of magnitude. The space of agents includes:

1. **Surface-active peptides.** The aromatic–charged balanced peptides designed by Sanchez-Burgos et al. (2025) decelerate TDP-43 and FUS condensate aging by more than an order of magnitude via repulsive electrostatic interactions that deplete condensate density at the interface.
2. **Engineered protein cages and nanoclusters.** The 30-nm surface-interacting cages of Oh et al. (2025) localize to condensate surfaces and prevent coalescence, achieving size control from 100 nm to 1 μm.
3. **Antibody and nanobody coronae.** Antibody-based interfacial coatings tuned to IDR epitopes would constitute a natural engineered analog of MEG-3.
4. **RNA aptamers** with defined fold (Stewart et al. 2023; Wadsworth et al. 2024), selected against surface-accessible aromatic patches of FUS / TDP-43 low-complexity domains.
5. **Small molecules that partition specifically into the interfacial layer.** The BTBolig chemical genetic platform enables inducible condensate formation and maturation control, providing a route to screen small-molecule interfacial modulators (Hernandez-Candia et al. 2024).

### 5.2 Differentiation from Bulk Condensate Dissolvers

1,6-hexanediol and related bulk-disrupting agents non-selectively dissolve all condensates, producing broad cellular toxicity (Muzzopappa et al. 2022). Interfacial c-mods, in contrast, allow the condensate to persist in a functional liquid state while blocking the specific pathological channel. This narrowness of action is the therapeutic advantage.

### 5.3 Link to Existing Clinical-Stage Programs

Structure-guided small molecules identified by graph convolutional neural networks for TDP-43 modulation (Gao et al. 2023), pathway-targeting small molecules for neurodegeneration (Sanghai et al. 2024), and posttranslational modifications that drive specific amyloid strains (Balana et al. 2024) all interact with the interfacial-nucleation framework. In particular, O-GlcNAc-modified α-synuclein forms fibrils with diminished seeding (Balana et al. 2024), consistent with modifications that alter the surface-contacting IDR conformation and reduce λ in F411.

---

## 6. Refinement and Fine-Tuning of the Method

### 6.1 Calibration Against Known γ and λ Values

Flicker-spectroscopy-based measurement of γ and bending rigidity κ via FlickerPrint-style pipelines (Williamson et al. 2025) and FRAP-ID (Santamaria et al. 2024) provide orthogonal calibration of F412. Sessile-drop measurements (Holland et al. 2023) provide a second independent estimate. Agreement across methods within a factor of two is required for confidence; divergence beyond this triggers a revision of the coupling assumption F412.

### 6.2 Orthogonal Validation

The six-method readout scheme (Section 3.4) is redundant by design: NMR, SERS, SMLM, smFRET, cryo-ET, and mass photometry each have different backgrounds and systematic errors, and the pre-registered analysis requires that at least four of six yield β > 0 with consistent magnitude for H1 to be supported. Single-technique failures would otherwise be indistinguishable from the hypothesis being wrong.

### 6.3 Sources of Bias and Their Mitigation

- **Air–water interfaces in vitro are not cell interiors.** The in-cell validation in Section 6.4 addresses this.
- **Droplet-size distributions are not monodisperse in cells.** The regression analysis accommodates distributions explicitly via a mixture model weighted by droplet volume and the natural S/V variation is used as an internal titration within single cells (Muzzopappa et al. 2022).
- **Fluorophore tagging alters phase behavior.** eYFP-tagged simulations show minor but measurable shifts in droplet properties (Veevers et al. 2024), which we correct by matched untagged controls.
- **Protein preparation history alters oligomeric precursors.** Kar et al. (2022) demonstrate that subsaturated solutions contain heterogeneous cluster distributions far beyond classical nucleation expectations. Reproducing precursor distributions across preparations requires tight control of protein solubilization, tag cleavage, and desalting conditions.

### 6.4 In-Cell Extension

A positive result in vitro is necessary but not sufficient. The next step is chemical-genetic induction of FUS or TDP-43 condensates in living cells with BTBolig (Hernandez-Candia et al. 2024) and CLR-MS mapping of interior-vs-surface protein–RNA contacts (de Vries et al. 2024), with the S/V titration performed by temperature-controlled condensate coarsening. The in-cell experiment is the external validity test for the in vitro framework.

### 6.5 Blinding and Replication

Samples are coded by a third party. Analysis pipelines are pre-registered on a time-stamped public repository before data collection. Three independent replication sites are agreed in advance. No conclusions are reported without blind analysis.

---

## 7. Open Questions That Survive a Positive Result

### 7.1 Promiscuous vs. Specific Interfacial Nucleation

F411 treats line tension λ as a scalar characteristic of the interface. In practice λ depends on IDR sequence composition, post-translational modifications, and RNA content (Balana et al. 2024; Wadsworth et al. 2024). The molecular grammar of λ is entirely unmapped. A comprehensive mutagenesis scan of FUS and TDP-43 low-complexity domains, coupled with direct λ measurement via defect-nucleation kinetics, would decode this grammar.

### 7.2 The In Vivo Relevance of Membrane Contacts

In neurons, condensates encounter not only the cytoplasm but organelle membranes (ER, mitochondria, endosomes). Lipid interfaces are well-established amyloid catalysts for α-synuclein (Roeters et al. 2023). Whether disease-relevant LST is dominated by condensate–cytoplasm or condensate–membrane interfaces is an unresolved question that F412 motivates asking.

### 7.3 RNA as Interfacial Suppressor

Emmanouilidis et al. (2024) report that RNA binding prevents surface maturation of FUS condensates. Wadsworth et al. (2024) review RNA's role as phase behavior modulator; the interfacial-specific mechanism—whether RNA depletes interfacial protein density, alters λ, or shields aromatic residues from surface exposure—is unknown. Single-molecule fluorescence polarization at the droplet surface would help resolve this.

### 7.4 Connection to Reversible Functional Amyloids

Not all cross-β is pathogenic. Functional reversible amyloids stabilize Orb2 memory condensates and TIA-1 stress granules (Ripin et al. 2023). The interfacial-nucleation framework does not yet explain why some interface-nucleated cross-β phases are reversible and others are not; the answer likely lies in λ and in host-factor coverage of F413.

### 7.5 Cross-Species and Cross-Condensate Generality

The FUS–TDP-43 evidence is strong. α-Synuclein, Aβ, and hnRNPA1 show the same pattern. Tau shows partial evidence (Wen et al. 2025). CHCHD10/CHCHD2 mitochondrial proteins form disease-relevant fibrils with structural polymorphism (Lv et al. 2025), but their condensate biology is unstudied. TAF15 pathology (Tetter et al. 2023) is wholly uncharacterized at the interface. A systematic cross-protein comparison would test whether F409–F414 are universal.

---

## 8. Conclusions

The pathogenic liquid-to-solid transition of ribonucleoprotein condensates is a process at an interface, and its rate-limiting step is governed by a handful of measurable geometric and interfacial variables: surface-area-to-volume ratio, interfacial tension γ, line tension λ, capillary-wave spectrum, and Pickering coverage *θ*_p. The recent experimental literature contains the methods and the reagents necessary to test this claim quantitatively, and the experiment proposed here is designed to be falsified rather than merely confirmed. If the hypothesis survives, a new class of therapeutics that operate selectively at the condensate interface becomes accessible without disrupting the functional interior. If the hypothesis fails, the field is sharpened: bulk cross-linking dominates, and the therapeutic program must target multivalency instead. Either outcome advances the field. The framework developed here is a direct extension of previous liquid-to-solid section, grounded in classical interfacial thermodynamics, and designed to be executed in a leading structural biology laboratory within eighteen months.

---

## References

Alberti, Simon, et al. "Current practices in the study of biomolecular condensates: a community comment." *Nature Communications*, vol. 16, 2025.

Amico, Tommaso, et al. "A scale-invariant log-normal droplet size distribution below the critical concentration for protein phase separation." *eLife*, vol. 13, 2024.

Arseni, Diana, et al. "Heteromeric amyloid filaments of ANXA11 and TDP-43 in FTLD-TDP type C." *Nature*, vol. 634, 2024, pp. 662–668.

Arter, William E., et al. "Biomolecular condensate phase diagrams with a combinatorial microdroplet platform." *Nature Communications*, vol. 13, 2022.

Avni, Anamika, et al. "Single-droplet surface-enhanced Raman scattering decodes the molecular determinants of liquid-liquid phase separation." *Nature Communications*, vol. 13, 2022.

Balana, Aaron T., et al. "O-GlcNAc forces an α-synuclein amyloid strain with notably diminished seeding and pathology." *Nature Chemical Biology*, vol. 20, 2024, pp. 646–655.

Bartolomé-Nafría, Andrea, et al. "Mutations in human prion-like domains: pathogenic but not always amyloidogenic." *Prion*, vol. 18, 2024, pp. 28–39.

Chew, Ping, et al. "Aromatic and arginine content drives multiphasic condensation of protein-RNA mixtures." *Biophysical Journal*, vol. 122, 2023, pp. 3944–3958.

Dada, Samuel T., et al. "Spontaneous nucleation and fast aggregate-dependent proliferation of α-synuclein aggregates within liquid condensates at neutral pH." *Proceedings of the National Academy of Sciences*, vol. 120, 2023.

Dai, Yifan, et al. "Engineering synthetic biomolecular condensates." *Nature Reviews Bioengineering*, vol. 1, 2023, pp. 466–480.

Das, Tapojyoti et al. “Tunable metastability of condensates reconciles their dual roles in amyloid fibril formation.” bioRxiv : the preprint server for biology 2024.02.28.582569. 22 Mar. 2025, doi:10.1101/2024.02.28.582569. Preprint.

de Vries, Tebbe, et al. "Specific protein-RNA interactions are mostly preserved in biomolecular condensates." *Science Advances*, vol. 10, 2024.

Dhakal, Subhankar, et al. "α-Synuclein emulsifies TDP-43 prion-like domain—RNA liquid droplets to promote heterotypic amyloid fibrils." *Communications Biology*, vol. 6, 2023.

Emmanouilidis, Leonidas, et al. "A solid beta-sheet structure is formed at the surface of FUS droplets during aging." *Nature Chemical Biology*, vol. 20, 2024, pp. 1044–1052.

Folkmann, Andrew W., et al. "Regulation of biomolecular condensates by interfacial protein clusters." *Science*, vol. 373, 2021, pp. 1218–1224.

Galvanetto, Nicola, et al. "Extreme dynamics in a biomolecular condensate." *Nature*, vol. 619, 2023, pp. 876–883.

Gao, Peng, et al. "Molecular Graph-Based Deep Learning Algorithm Facilitates an Imaging-Based Strategy for Rapid Discovery of Small Molecules Modulating Biomolecular Condensates." *Journal of Medicinal Chemistry*, vol. 66, 2023, pp. 7785–7797.

García-Pardo, Javier, et al. "Cryo-EM structures of functional and pathological amyloid ribonucleoprotein assemblies." *Trends in Biochemical Sciences*, vol. 48, 2023, pp. 1038–1053.

Gouveia, Bernardo, et al. "Capillary forces generated by biomolecular condensates." *Nature*, vol. 609, 2022, pp. 255–264.

He, Changdong, et al. "Multidimensional Super-Resolution Microscopy Unveils Nanoscale Surface Aggregates in the Aging of FUS Condensates." *Journal of the American Chemical Society*, vol. 145, 2023, pp. 24620–24631.

Hernandez-Candia, Carmen N., et al. "A platform to induce and mature biomolecular condensates using chemicals and light." *Nature Chemical Biology*, vol. 20, 2024, pp. 452–462.

Hoffmann, Christian, et al. "Signals from the interface: protein nanoclusters stabilize biomolecular condensates." *Signal Transduction and Targeted Therapy*, vol. 7, 2022.

Holland, Jonathan, et al. "Surface tension measurement and calculation of model biomolecular condensates." *Soft Matter*, vol. 19, 2023, pp. 4931–4940.

Hurtle, Bryan T., et al. "Disrupting pathologic phase transitions in neurodegeneration." *The Journal of Clinical Investigation*, vol. 133, 2023.

Jeon, Soyoung, et al. "Emerging regulatory mechanisms and functions of biomolecular condensates: implications for therapeutic targets." *Signal Transduction and Targeted Therapy*, vol. 10, 2025.

Jülicher, Frank, et al. "Droplet Physics and Intracellular Phase Separation." *Annual Review of Condensed Matter Physics*, vol. 15, 2023, pp. 237–261.

Kar, Mrityunjoy, et al. "Phase-separating RNA-binding proteins form heterogeneous distributions of clusters in subsaturated solutions." *Proceedings of the National Academy of Sciences*, vol. 119, 2022.

Li, Fangying, et al. "Atomistic Insights into A315E Mutation-Enhanced Pathogenicity of TDP-43 Core Fibrils." *ACS Chemical Neuroscience*, vol. 13, 2022, pp. 2743–2754.

Linsenmeier, Miriam, et al. "The interface of condensates of the hnRNPA1 low-complexity domain promotes formation of amyloid fibrils." *Nature Chemistry*, vol. 15, 2022, pp. 1340–1349.

Lipiński, Wojciech P., et al. "Biomolecular condensates can both accelerate and suppress aggregation of α-synuclein." *Science Advances*, vol. 8, 2022.

Lu, Hao, et al. "Acidic pH Promotes Refolding and Macroscopic Assembly of Amyloid β (16–22) Peptides at the Air–Water Interface." *The Journal of Physical Chemistry Letters*, vol. 13, 2022, pp. 9953–9959.

Lu, Xingyu, et al. "The Role of Liquid-Liquid Phase Separation in the Accumulation of Pathological Proteins: New Perspectives on the Mechanism of Neurodegenerative Diseases." *Aging and Disease*, vol. 15, 2024, pp. 1470–1490.

Lv, Guohua, et al. "Amyloid fibril structures link CHCHD10 and CHCHD2 to neurodegeneration." *Nature Communications*, vol. 16, 2025.

Maltseva, Daria, et al. "Fibril formation and ordering of disordered FUS LC driven by hydrophobic interactions." *Nature Chemistry*, vol. 15, 2023, pp. 1146–1154.

Mohanty, Priyesh, et al. "A complex network of interdomain interactions underlies the conformational ensemble of monomeric TDP-43 and modulates its phase behavior." *Protein Science*, vol. 32, 2023.

Mukherjee, Saumyak, et al. "Thermodynamic forces from protein and water govern condensate formation of an intrinsically disordered protein domain." *Nature Communications*, vol. 14, 2023.

Muzzopappa, Fernando, et al. "Detecting and quantifying liquid–liquid phase separation in living cells by model-free calibrated half-bleaching." *Nature Communications*, vol. 13, 2022.

Naskar, Aditi, et al. "Phase separation and pathologic transitions of RNP condensates in neurons: implications for amyotrophic lateral sclerosis, frontotemporal dementia and other neurodegenerative disorders." *Frontiers in Molecular Neuroscience*, vol. 16, 2023.

Oh, Hyeok Jin, et al. "Size-controlled assembly of phase separated protein condensates with interfacial protein cages." *Nature Communications*, vol. 16, 2025.

Pyo, Andrew G. T., et al. "Surface tension and super-stoichiometric surface enrichment in two-component biomolecular condensates." *iScience*, vol. 25, 2022.

Pyo, Andrew G. T., et al. "Proximity to criticality predicts surface properties of biomolecular condensates." *Proceedings of the National Academy of Sciences*, vol. 120, 2023.

Ray, Soumik, et al. "Mass photometric detection and quantification of nanoscale α-synuclein phase separation." *Nature Chemistry*, vol. 15, 2023, pp. 1306–1316.

Ren, Hao, et al. "Non-fibril amyloid aggregation at the air/water interface: self-adaptive pathway resulting in a 2D Janus nanofilm." *Chemical Science*, vol. 15, 2024, pp. 4612–4623.

Ripin, Nina, and Roy Parker. "Formation, function, and pathology of RNP granules." *Cell*, vol. 186, 2023, pp. 4737–4756.

Roeters, Steven J., et al. "Elevated concentrations cause upright alpha-synuclein conformation at lipid interfaces." *Nature Communications*, vol. 14, 2023.

Sanchez-Burgos, Ignacio, et al. "Charged peptides enriched in aromatic residues decelerate condensate ageing driven by cross-β-sheet formation." *Nature Communications*, vol. 16, 2025.

Sanfeliu-Cerdán, Neus, et al. "The mechanobiology of biomolecular condensates." *Biophysics Reviews*, vol. 6, 2025.

Santamaria, Andreas, et al. "Quantifying surface tension and viscosity in biomolecular condensates by FRAP-ID." *Biophysical Journal*, vol. 123, 2024, pp. 1512–1523.

Sharma, Kartikay, et al. "Cryo-EM observation of the amyloid key structure of polymorphic TDP-43 amyloid fibrils." *Nature Communications*, vol. 15, 2024.

Shen, Yi, et al. "The liquid-to-solid transition of FUS is promoted by the condensate surface." *Proceedings of the National Academy of Sciences*, vol. 120, 2023.

Song, Jianxing. "Molecular Mechanisms of Phase Separation and Amyloidosis of ALS/FTD-linked FUS and TDP-43." *Aging and Disease*, vol. 15, 2023, pp. 2423–2451.

Stewart, Jacob M., et al. "Modular RNA motifs for orthogonal phase separated compartments." *Nature Communications*, vol. 14, 2023.

Strunge, Kris, et al. "Umbrella-like Helical Structure of α-Synuclein at the Air-Water Interface Observed with Experimental and Theoretical Sum Frequency Generation Spectroscopy." *The Journal of Physical Chemistry Letters*, vol. 14, 2023, pp. 4073–4081.

Szała-Mendyk, Beata, et al. "Challenges in studying the liquid-to-solid phase transitions of proteins using computer simulations." *Current Opinion in Chemical Biology*, vol. 75, 2023.

Todd, Tiffany W., et al. "Cryo-EM structures of pathogenic fibrils and their impact on neurodegenerative disease research." *Neuron*, vol. 112, 2024, pp. 2269–2288.

Wadsworth, Gable M., et al. "RNA-driven phase transitions in biomolecular condensates." *Molecular Cell*, vol. 84, 2024, pp. 3692–3705.

Wang, Li-Qiang, et al. "Amyloid fibril structures and ferroptosis activation induced by ALS-causing SOD1 mutations." *Science Advances*, vol. 10, 2024.

Williamson, Thomas A., et al. "Non-invasive measurement of biomolecular condensate interfacial tension and bending rigidity." *Cell Reports Methods*, vol. 5, 2025.

Zhou, Huabin, et al. "Quantitative spatial analysis of chromatin biomolecular condensates using cryoelectron tomography." *Proceedings of the National Academy of Sciences*, vol. 122, 2025.

Zhou, Huan-Xiang, et al. "Fundamental Aspects of Phase-Separated Biomolecular Condensates." *Chemical Reviews*, vol. 124, 2024, pp. 8550–8595.
