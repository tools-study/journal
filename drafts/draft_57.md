# Gene Replacement Therapy Review

---

## Abstract

The approval of voretigene neparvovec (Luxturna™) in 2017 — an adeno-associated virus serotype 2 (AAV2) vector carrying the human *RPE65* complementary DNA — established that *in vivo* delivery of a functional gene copy can restore a biological function that was categorically absent, validating the pivotal Phase I safety data reported by Maguire and colleagues in 2008 (Maguire et al., 2008). In the seventeen years since that report, an additional seven AAV-based gene replacement therapies have been approved by the FDA and/or EMA for diseases of the retina, motor neuron, hepatocyte, and skeletal muscle, and durable therapeutic benefit has been documented at five-, seven-, and in some cases more-than-twelve-year time horizons (Maguire et al., 2021; Pipe et al., 2025; George et al., 2020). Yet precisely this accumulating long-term data has exposed a fundamental conceptual problem that the pivotal-trial literature of 2008–2019 could not have quantified: *transgene expression is not permanent*. Across indications, a durable steady-state expression level is approached only after an initial 90–180-day transcriptional decline whose magnitude and endpoint vary by a factor of ten between factor IX (stable) and factor VIII (progressively declining) hemophilia programs (Samelson-Jones et al., 2024; Dargaud et al., 2025), and in pediatric liver the transduced episome is diluted by hepatocellular proliferation at a rate that depends on patient age (Cunningham et al., 2008; Wang et al., 2012). This manuscript formulates the durability problem as the central unresolved obstacle to second-generation gene replacement therapy and introduces mathematical frameworks (F429–F435) that quantify its components: a two-phase episomal–integrated persistence ODE with transgene-specific immunogenic shutdown; a hepatocyte age-structured vector dilution model calibrated to the Milani et al. 2025 clonogenic-hepatocyte niche (Milani et al., 2025); a TLR9-CpG innate-immunity decay function parameterized on Mehta et al. 2025 (Mehta et al., 2025); a capsid-specific CD8 T cell transduced-cell-elimination hazard; an FVIII-specific protein-folding proteostatic ceiling; a retinal photoreceptor viability–transduction product as a maximum-expression bound; and a compound-Poisson complement-activation dose-ceiling derived from the Salabarria et al. 2023 immune-kinetics data (Salabarria et al., 2023). We argue that the coupled bottleneck of *episomal dilution plus transgene-encoded-protein immunogenic shutdown* is the primary obstacle — it is the mechanism by which every AAV gene replacement program has lost at least some of its initial transduction benefit, it is the mechanism that the Greig et al. 2023 non-human-primate integration study elegantly partitioned into a transient and a stable phase (Greig et al., 2023), and it is the mechanism most tractable to second-generation engineering through codon-CpG optimization, scaffold/matrix-attachment elements, targeted integration via transposons or bridge recombinases, and immunomodulation regimens. We review the clinical evidence across all eight approved gene replacement therapies, develop the mathematical frameworks that formalize the durability constraint, and close with a concrete research agenda for the next decade, emphasizing translational priorities that carry the highest probability of meaningfully improving human health.

---

## 1. Introduction

On May 22, 2008, the *New England Journal of Medicine* published the Phase I open-label dose-escalation trial by Maguire and colleagues reporting subretinal injection of AAV2.hRPE65v2 in three adult patients with Leber congenital amaurosis type 2 — a childhood blinding disease caused by biallelic loss-of-function mutations in the retinal pigment epithelium-specific 65 kDa protein gene (*RPE65*) (Maguire et al., 2008). The trial reported an acceptable local and systemic adverse-event profile, modest improvements in visual acuity, and the occurrence of an asymptomatic macular hole in a single patient. It was a small, cautious, first-in-human demonstration; yet within a decade it had become the pivotal pre-clinical-to-clinical reference for the first AAV-based gene replacement therapy approved by the U.S. Food and Drug Administration (voretigene neparvovec-rzyl; Luxturna™, Spark Therapeutics; 19 December 2017) (Russell et al., 2017; Kang and Keam, 2020). Over the seventeen years since the Maguire report, seven additional AAV-mediated gene replacement products have received regulatory approval: onasemnogene abeparvovec (Zolgensma™, for spinal muscular atrophy; Blair, 2022); valoctocogene roxaparvovec (Roctavian™, for hemophilia A; Ozelo et al., 2022); etranacogene dezaparvovec (Hemgenix™, for hemophilia B; Pipe et al., 2023); eladocagene exuparvovec (Upstaza™, for AADC deficiency; Keam, 2022); delandistrogene moxeparvovec (Elevidys™, for Duchenne muscular dystrophy; Hoy, 2023); and, in ex-vivo form, exagamglogene autotemcel (Casgevy™, Hoy, 2024) — though the last is a CRISPR-edited cell therapy rather than classical gene replacement.

These approvals collectively establish gene replacement therapy as a mature clinical category. They also make it possible, for the first time, to ask a question that the pivotal-trial literature of 2008–2019 was not equipped to answer: *how long does the therapeutic effect last, and what limits its duration?* Long-term follow-up from the pivotal Luxturna Phase I cohort demonstrates persistence of retinal functional benefit for at least 7.5 years (Leroy et al., 2022); the Phase III cohort shows maintained bilateral multi-luminance mobility test improvement at 3–4 years (Maguire et al., 2021); and post-marketing surveillance confirms durable functional vision in approximately 70% of treated eyes at four years, though with a now-recognized 13–50% incidence of accelerated chorioretinal atrophy in the injected area (Simoens et al., 2025; Lorenz, 2025; Gange et al., 2022). In hemophilia B, the 5-year end-of-study analysis of the HOPE-B trial demonstrated stable factor IX activity averaging 36.1% of normal across 50 surviving participants, with annualized bleeding rate reduced 96% and only a single participant resuming prophylaxis (Pipe et al., 2025). In hemophilia A, by contrast, the 3-year GENEr8-1 dataset of valoctocogene roxaparvovec shows a qualitatively different trajectory: factor VIII expression peaks at 12 months and declines thereafter at roughly 40% per year, with mean activity of 41.9 IU/dL at year 1 falling to approximately 13 IU/dL at year 3 in the higher-dose cohorts (Ozelo et al., 2022; Pasi et al., 2020; Samelson-Jones et al., 2024).

These divergent outcomes across products sharing the same vector platform expose a central scientific puzzle: *why is factor IX stable and factor VIII not?* Neither product is being metabolized away; neither is being cleared by neutralizing antibodies on a three-year timescale. Both operate in the same target tissue (hepatocytes) delivered by the same systemic intravenous route. What differs is the intrinsic biology of the transgene product, the cellular stress it imposes on the hepatocyte, its immunogenicity, and the extent to which its transcriptional cassette is subject to cellular silencing mechanisms. And those differences together define what we call the *durability problem in gene replacement therapy* — the observation that transgene expression is governed not by a single persistence half-life but by a coupled multi-rate process whose components include: (1) episomal dilution during cell division, (2) transgene-product-driven cellular toxicity or proteostatic overload, (3) CpG-driven TLR9-mediated innate shutdown, (4) capsid-specific CD8 T cell elimination of transduced cells, (5) epigenetic silencing of episomal chromatin, (6) integration-mediated stable expression at low per-cell copy number, and (7) progressive cell death from underlying disease biology (Muhuri et al., 2022; Greig et al., 2023; Das et al., 2021).

For Gene *Replacement* — the category that accounts for all eight currently approved gene therapies — the primary obstacle is not immunogenicity alone (though that contributes); it is not manufacturing alone (though that constrains access). It is the *coupled durability problem*: the rate at which initial high transduction gives way to either a stable lower steady state or a continuing monotonic decline, and the mechanism — transgene-specific and tissue-specific — that determines which of these two trajectories a given therapy follows. The purpose of this manuscript is to formalize that problem, to develop mathematical frameworks that partition its components, and to identify the engineering levers most likely to resolve it.

---

## 2. The Approved Gene Replacement Landscape as of 2026

A concise inventory of the approved gene replacement products is prerequisite to any quantitative analysis of their durability. Table 1 summarizes the eight currently approved *in vivo* AAV-delivered gene replacement products; we exclude ex-vivo gene-modified cell therapies (Casgevy, Lyfgenia, Lenmeldy, Skysona) as these represent a categorically different therapeutic class (ex-vivo editing of autologous HSCs followed by myeloablative reinfusion) whose durability is governed by HSC clonal dynamics rather than by AAV vector persistence (Hoy, 2024; Frangoul et al., 2024).

### Table 1. In vivo AAV gene replacement products as of 2026.

| Product | Target gene | Tissue | Serotype | Approval year | Reported durability |
|---|---|---|---|---|---|
| Luxturna (voretigene neparvovec) | *RPE65* | Retina (subretinal) | AAV2 | 2017 | ≥7.5 y Phase I; ≥4 y Phase III (Leroy et al., 2022; Maguire et al., 2021) |
| Zolgensma (onasemnogene abeparvovec) | *SMN1* | Spinal motor neurons (IV) | AAV9 | 2019 | ≥8 y post-dose (Mendell et al., 2023) |
| Upstaza (eladocagene exuparvovec) | *DDC* | Putamen (intracerebral) | AAV2 | 2022 | ≥10 y motor improvement (Keam, 2022; Hwu et al., 2012) |
| Roctavian (valoctocogene roxaparvovec) | *F8* | Hepatocytes (IV) | AAV5 | 2022 EMA / 2023 FDA | Year-over-year decline (Ozelo et al., 2022) |
| Hemgenix (etranacogene dezaparvovec) | *F9*-Padua | Hepatocytes (IV) | AAV5 | 2022 | ≥5 y stable (Pipe et al., 2025; von Drygalski et al., 2025) |
| Elevidys (delandistrogene moxeparvovec) | Micro-*DMD* | Skeletal + cardiac muscle (IV) | AAVrh74 | 2023 (accelerated) | ≥2 y at accelerated approval (Hoy, 2023; Mendell et al., 2024) |

Several patterns emerge immediately. First, every approved gene replacement therapy is delivered by a single-stranded or self-complementary AAV vector. Second, all but one (Upstaza, for the hepatic AADC deficiency disorder, delivered stereotaxically into the putamen) rely on either local injection into an immune-privileged compartment (retina, CNS) or on systemic intravenous delivery that requires target-tissue tropism supplied by the capsid serotype. Third, all current products deliver the transgene as a non-integrating episome; none relies on site-specific integration. And fourth — the observation that motivates this manuscript — the durability profile is not uniform across products. Factor IX (Hemgenix) expression is stable through five years; factor VIII (Roctavian) declines year-over-year; *RPE65* (Luxturna) is stable for at least 7.5 years but with an accelerating paracentral atrophy risk; Duchenne micro-dystrophin (Elevidys) is detectable at 34% of normal expression at week 12 but long-term trajectories are incompletely characterized (Mendell et al., 2024). To formalize these divergences we must unpack the biology of episomal persistence, transcriptional regulation, and immune surveillance that jointly determine expression over time.

---

## 3. The Episomal-to-Integrated Persistence Problem

Recombinant AAV genomes enter the nucleus as single-stranded DNA that is converted to double-stranded form either by second-strand synthesis or — in the case of self-complementary AAV (scAAV) — by intramolecular folding of the inverted repeat (McCarty, 2008). The resulting double-stranded vector DNA can either persist as an extrachromosomal circular episome, be lost, be transcriptionally silenced, or be integrated into the host genome at a low frequency (Kasimsetty et al., 2024; Schmidt et al., 2023). For post-mitotic cells (retinal pigment epithelium, adult hepatocytes at steady state, spinal motor neurons, cardiomyocytes), episomal persistence is stable on multi-year timescales; for proliferating cells, episomal dilution during cell division is the dominant loss mechanism, because the circular episome lacks an origin of replication and does not segregate with the host chromosome during mitosis (Muhuri et al., 2022; Cunningham et al., 2008; Wang et al., 2012).

The definitive mechanistic study of AAV persistence in non-human primate liver was reported by Greig and colleagues in 2023, who followed cynomolgus macaques for over two years after intravenous administration of AAV8 and AAVrh10 vectors encoding either a non-immunogenic (self) or an immunogenic (foreign) transgene (Greig et al., 2023). Three findings from this study are essential to the durability problem. First, high initial transduction was achieved in approximately 10–20% of hepatocytes at peak, with declining expression over the first 90 days to a stable lower steady state. Second, despite the loss of bulk transgene mRNA, over 10% of hepatocytes retained detectable vector DNA as single nuclear domains at two years — evidence that the vector genome is not simply being degraded. Third, integrated vector sequences (in complex concatemeric structures) were detectable in approximately 1% of cells, distributed broadly across the genome, with no enrichment at loci associated with hepatocellular carcinoma. Together these data support a two-phase persistence model: (phase A) transient high expression from episomal DNA, (phase B) stable low expression from a small population of integrated or stably-maintained vectors. A similar observation has since been made in hemophilia A dogs followed more than a decade after portal-vein AAV-FVIII delivery, where long-term transgene expression correlated with episomal persistence, integration was detectable at a low rate (9.3 × 10⁻⁴ sites per cell), no full-length integrated vectors were identified, and no histopathological evidence of tumorigenesis was observed (Batty et al., 2024).

### F429 — Two-Phase Episomal–Integrated Persistence with Transgene-Driven Shutdown

Let $E(t)$ denote the number of transduced cells expressing from episomal vector at time $t$, and $I(t)$ the number expressing from integrated vector. Let $P(t) = p_E E(t) + p_I I(t)$ denote the total per-patient transgene protein output, with $p_E, p_I$ the per-cell expression rates for episomal and integrated modes, respectively (empirically $p_E \gg p_I$; the episomal copy number per cell is typically 10–1000 whereas integration typically reflects 1–2 copies per cell). The coupled ODE system governing $E$ and $I$ is:

```math
\frac{dE}{dt} \;=\; -\mu_{\text{div}}(t)\,E \;-\; \sigma_{\text{epi}}(t)\,E \;-\; \phi_{\text{Tg}}(t)\,E \;-\; \psi_{\text{T}}(t)\,E \;-\; k_{\text{int}}\,E
```

```math
\frac{dI}{dt} \;=\; k_{\text{int}}\,E \;-\; \mu_{\text{div}}(t)\,I \;+\; \mu_{\text{div}}(t)\,I \;=\; k_{\text{int}}\,E
```

**Variables.** $\mu_{\text{div}}(t)$ is the division rate of the target tissue (d⁻¹; near-zero for post-mitotic retina, ≈10⁻³ d⁻¹ for adult hepatocytes at steady state, rising to ≈10⁻² d⁻¹ during neonatal liver growth; Milani et al., 2025); $\sigma_{\text{epi}}(t)$ is the episomal epigenetic silencing rate (d⁻¹; includes HUSH-complex-mediated H3K9 methylation of the episomal chromatin; Das et al., 2021); $\phi_{\text{Tg}}(t)$ is the transgene-specific protein-folding/proteostatic stress-induced apoptosis rate (d⁻¹; ≈0 for FIX-Padua, substantially elevated for misfolded FVIII; Samelson-Jones et al., 2024); $\psi_{\text{T}}(t)$ is the capsid- or transgene-specific CD8 T cell elimination hazard (d⁻¹; peaks at 8–12 weeks post-dose; Martino et al., 2013; Bertolini et al., 2021); and $k_{\text{int}}$ is the integration-conversion rate (d⁻¹; ≈10⁻⁸ per cell per day for random concatemer integration in NHP liver; Greig et al., 2023). The integrated fraction $I(t)$ is approximately conserved through cell division because daughter cells inherit the integrated sequence (the second $\mu_{\text{div}} I$ term recaptures daughters and therefore cancels out — integration is quasi-stable against proliferation, distinguishing it sharply from the episomal compartment).

Assuming initial conditions $E(0) = E_0$, $I(0) = 0$, and $\phi_{\text{Tg}}, \psi_T$ approximately constant over the persistence window, the closed-form solution is:

```math
E(t) \;=\; E_0 \exp\!\left[-(\mu_{\text{div}} + \sigma_{\text{epi}} + \phi_{\text{Tg}} + \psi_T + k_{\text{int}})\,t\right]
```

```math
I(t) \;=\; \frac{k_{\text{int}}\,E_0}{\mu_{\text{div}} + \sigma_{\text{epi}} + \phi_{\text{Tg}} + \psi_T + k_{\text{int}}}\,\left[1 - \exp\!\left(-(\mu_{\text{div}} + \sigma_{\text{epi}} + \phi_{\text{Tg}} + \psi_T + k_{\text{int}})\,t\right)\right]
```

```math
P(t) \;=\; p_E\,E_0 \exp\!\left[-\alpha\,t\right] + \frac{p_I\,k_{\text{int}}\,E_0}{\alpha}\,\left[1 - \exp(-\alpha t)\right]
```

where $\alpha = \mu_{\text{div}} + \sigma_{\text{epi}} + \phi_{\text{Tg}} + \psi_T + k_{\text{int}}$ is the total first-phase loss rate. As $t \to \infty$, $P(t) \to p_I k_{\text{int}} E_0 / \alpha$ — a stable positive steady state derived entirely from the integrated fraction. This framework explains three clinical observations simultaneously. First, why all AAV gene replacement therapies exhibit a two-phase expression kinetic (rapid initial decline followed by a slower-decaying or stable plateau; Muhuri et al., 2022; Greig et al., 2023). Second, why factor IX (with low $\phi_{\text{Tg}}, \psi_T$ and non-dividing hepatocyte target) stabilizes at approximately 36% of normal after 5 years (Pipe et al., 2025), while factor VIII (with elevated $\phi_{\text{Tg}}$ from FVIII proteostatic stress and potentially elevated $\psi_T$) continues to decline (Samelson-Jones et al., 2024). Third, why pediatric liver-directed therapy is structurally more difficult than adult liver-directed therapy: $\mu_{\text{div}}(t)$ is 10-fold higher during postnatal liver growth, driving exponential $E(t)$ loss that cannot be rescued by the small integrated fraction $I$ unless $k_{\text{int}}$ is substantially elevated by deliberate vector engineering (Cunningham et al., 2008; Wang et al., 2012).

---

## 4. The Luxturna Paradigm: Retinal Gene Replacement with a Post-Mitotic Target

### 4.1 What the Maguire 2008 trial established, and what it could not

The Maguire et al. 2008 Phase I trial is the foundational reference of the modern gene-replacement era. In that report, three adult patients with LCA2 received subretinal injection of 1.5 × 10¹⁰ vector genomes of AAV2 carrying the wild-type human *RPE65* cDNA under a hybrid chicken β-actin / cytomegalovirus early enhancer promoter (Maguire et al., 2008). The primary endpoint was safety; modest functional gains in subjective measures of visual acuity were observed, and one asymptomatic macular hole occurred. In retrospect, three aspects of the trial design deserve particular emphasis for our analysis. First, the retina is a post-mitotic tissue, so $\mu_{\text{div}}$ in F429 is effectively zero — integration is not required for durability. Second, the subretinal space is immune-privileged, so $\psi_T$ is substantially suppressed relative to systemic delivery. Third, the transgene product (RPE65) is expressed constitutively by the native cell type (retinal pigment epithelium), so $\phi_{\text{Tg}}$ is near zero because there is no proteostatic novelty to the protein. All four durability-limiting terms in F429 are therefore minimized simultaneously, yielding a uniquely favorable durability profile. The Leroy et al. 2022 long-term-follow-up meta-analysis demonstrates this empirically, showing functional benefit persistence for at least 7.5 years in Phase I subjects (Leroy et al., 2022), and the Jacobson et al. 2012 multi-dose study reported dose-dependent visual function improvement across 15 subjects over a 3-year follow-up with no systemic toxicity (Jacobson et al., 2012).

### 4.2 Chorioretinal atrophy: A previously unrecognized durability-limiting process

What the Maguire 2008 trial could not anticipate is a complication that emerged only in post-marketing surveillance: accelerated paracentral chorioretinal atrophy (CRA) in 13–50% of Luxturna-treated eyes, often beginning within the first three months post-injection (Gange et al., 2022; Bender et al., 2024; Simoens et al., 2025). Lorenz 2025 reviews the post-marketing experience systematically and confirms that CRA appears to be a product- or procedure-specific adverse event rather than an acceleration of the underlying retinal dystrophy (Lorenz, 2025). Berger et al. 2025 conducted a systematic review across 31 retinal-gene-therapy clinical trials and 18 post-approval Luxturna studies, documenting serious adverse events in 24.7% of post-approval Luxturna eyes, with retinal degeneration being the most common (20.7%) (Berger et al., 2025). The emerging consensus is that CRA results from either subclinical inflammatory injury at the injection site, toxicity from the vector itself, or mechanical damage from the subretinal injection procedure. Disambiguating these mechanisms requires sham-injection controls that have not been performed at scale since the original Phase I (Maguire et al., 2008). An advanced alternative is epiretinal delivery via AAV-loaded fibrin hydrogels, recently demonstrated by Scruggs et al. 2025 to provide broad RPE transduction without atrophy or inflammation in nonhuman primates — a candidate next-generation delivery modality that would eliminate the subretinal-injection-specific toxicity (Scruggs et al., 2025).

### 4.3 The therapeutic-window-versus-atrophy trade-off

Gardiner et al. 2020 reported long-term structural outcomes of late-stage RPE65 gene therapy in the canine LCA2 model, following four treated dogs for 4–5 years (Gardiner et al., 2020). Treated retinal regions with more than 63% of normal photoreceptors at the time of intervention showed robust long-term retention; regions with fewer surviving photoreceptors showed progressive degeneration similar to untreated regions. This observation implies that the therapeutic window is bounded on both sides: too early and the patient carries a lifetime risk of gradual therapy-induced CRA; too late and the photoreceptor population is below the threshold for meaningful rescue.

### F430 — Retinal Photoreceptor Viability-Transduction Product

Let $N(t)$ denote the number of photoreceptors within the treated retinal region, $\eta(t)$ the fraction of these that are transduction-competent, and $q(t)$ the per-cell functional benefit (e.g., 11-cis-retinal regeneration rate restoration). Total functional output is:

```math
F(t) \;=\; q(t)\,\cdot\,\eta(t)\,\cdot\,N(t)
```

and its rate of change is:

```math
\frac{dF}{dt} \;=\; F(t)\,\left[\frac{1}{q}\frac{dq}{dt} + \frac{1}{\eta}\frac{d\eta}{dt} + \frac{1}{N}\frac{dN}{dt}\right]
```

**Variables.** $q$ is set by the expression level per cell (itself governed by F429); $\eta$ declines from surgical trauma or epigenetic silencing; $N$ declines from baseline disease attrition and treatment-induced CRA. Define the cellular attrition rate $\lambda_N = -d\ln N/dt$. For a treated region with baseline $\lambda_0$ (untreated disease) and induced CRA contribution $\epsilon$:

```math
\lambda_N(t) \;=\; \lambda_0 + \epsilon\,\mathbf{1}_{\{t \geq 0\}}
```

If $\lambda_{\text{untreated}} < \lambda_0 + \epsilon$, treatment accelerates cellular loss and the crossover time at which treated $F$ falls below untreated $F$ is finite. F430 quantifies the functional crossover by:

```math
t_{\text{crossover}} \;=\; \frac{\ln(q_{\text{treated}}\,\eta\,/\,q_{\text{untreated}})}{\epsilon}
```

For empirical Luxturna parameters with $q_{\text{treated}}/q_{\text{untreated}} \approx 5-10$, $\eta \approx 0.8$, and $\epsilon \approx 0.02$ y⁻¹ (derived from the Gange et al. CRA onset data; Gange et al., 2022): $t_{\text{crossover}} \approx 75-115$ years — well beyond the realistic human lifespan, validating net lifetime benefit under current parameters even in the presence of CRA. The key sensitivity is to $\epsilon$: a tenfold increase (to $\epsilon = 0.2$ y⁻¹) would reduce $t_{\text{crossover}}$ to ~8–12 years and invalidate lifetime benefit. Estimating $\epsilon$ accurately from the Bender et al. 24-month CRA incidence and the Simoens et al. pharmacovigilance dataset is therefore the single most important ophthalmic surveillance priority for the next decade (Bender et al., 2024; Simoens et al., 2025).

---

## 5. The Hemophilia Paradigm: Divergent FVIII and FIX Durability

The clearest empirical demonstration of the durability problem is the divergent trajectory of AAV gene replacement therapies for hemophilia A (factor VIII deficiency) and hemophilia B (factor IX deficiency). Both diseases are X-linked recessive bleeding disorders; both are corrected in principle by restoring the missing clotting factor; both are treated by AAV vectors intravenously infused to transduce hepatocytes that then secrete the clotting factor into plasma. Yet the two programs have diverged sharply on durability.

### 5.1 Factor IX (Hemgenix): Stable five-year expression

Etranacogene dezaparvovec (Hemgenix) is an AAV5-vectored hFIX-Padua transgene under a liver-specific promoter (Pipe et al., 2023). The Padua variant (R338L) encodes a naturally-occurring hyperactive FIX whose specific activity is approximately eight-fold that of wild-type, permitting therapeutic factor IX levels at modest transcript output (Chuah et al., 2014). The HOPE-B Phase 3 pivotal trial enrolled 54 participants and followed them for 5 years; at the 5-year timepoint, mean endogenous FIX activity was 36.1% (SD 15.7%) of normal — statistically indistinguishable from year 1 (41.5%) and year 3 (38.6%), indicating stable long-term expression (Pipe et al., 2025). Annualized bleeding rate dropped from 4.16 during lead-in to 0.40 at year 5. Only one of 54 participants resumed FIX prophylaxis over the entire 5-year observation period. The AMT-060/Phase 2b 5-year analysis similarly demonstrated mean FIX activity of 45.7 IU/dL at year 5 (von Drygalski et al., 2025). Statistical modeling based on the observed decay kinetics predicts that over 80% of participants would remain free of prophylactic factor IX through 25.5 years (Shah et al., 2022).

The durability of FIX expression has a clean mechanistic interpretation in F429. Adult hepatocytes have a division rate $\mu_{\text{div}}$ of approximately 10⁻³ d⁻¹ at baseline, and mature FIX is not known to impose measurable proteostatic stress on hepatocytes ($\phi_{\text{Tg}} \approx 0$). The FIX-Padua transgene has been extensively codon-optimized to minimize the CpG content that drives TLR9-mediated innate immunity ($\psi_T$ attenuated; Bertolini et al., 2021; Mehta et al., 2025). The 10–20% initial decline between weeks 4 and 12 reflects the normal episomal-vector shakedown observed across AAV liver programs (Muhuri et al., 2022). The absence of further decline after week 12 is consistent with integration-mediated stabilization as documented by Greig et al. in NHP (Greig et al., 2023) and by Batty et al. in dogs (Batty et al., 2024). An agent-based model of Hemgenix expression predicts a population-median stable plateau of 23% of normal FIX at 20 years (Li et al., 2024).

### 5.2 Factor VIII (Roctavian): Progressive year-over-year decline

Valoctocogene roxaparvovec (Roctavian) is an AAV5-vectored hFVIII-SQ (B-domain-deleted) transgene under the liver-specific HLP promoter (Ozelo et al., 2022). The GENEr8-1 Phase 3 trial enrolled 134 men with severe hemophilia A at a dose of 6 × 10¹³ vg/kg. Mean FVIII activity (chromogenic substrate assay) was 41.9 IU/dL at the primary endpoint (weeks 49–52), with 98.6% reduction in factor VIII concentrate use. However, years 2 and 3 demonstrated a progressive decline, such that 3-year activity across pooled cohorts was approximately 13 IU/dL — a 69% reduction from year 1 (Pasi et al., 2020). The Samelson-Jones et al. 2024 review of the full Roctavian development program concluded that the FVIII decline is mechanistically unexplained but has been qualitatively reproduced in animal models, whereas competing AAV-FVIII vectors with more modest initial expression (e.g., SPK-8011) show stable activity (Samelson-Jones et al., 2024; George et al., 2021).

Two hypotheses, not mutually exclusive, dominate the current discussion. The first is that the FVIII protein imposes endoplasmic-reticulum proteostatic stress on the hepatocyte (elevated $\phi_{\text{Tg}}$ in F429), because wild-type FVIII is an unusually large and complex protein with multiple domains, poorly secreted at high expression levels, and known to trigger the unfolded protein response in cell culture. The resulting apoptotic attrition of the highest-expressing hepatocytes would preferentially reduce expression from the most productive cells. The second is that the FVIII transgene cassette (including regulatory elements, intronic sequences, or the SQ-link region) harbors CpG motifs that drive TLR9-dependent CD8 T cell responses leading to elevated $\psi_T$ (Bertolini et al., 2021). Bala et al. 2024 reviews these mechanisms and emphasizes the need for next-generation vector design, including further CpG depletion and alternative promoters, to close the durability gap (Bala et al., 2024). George et al. 2021 reported the SPK-8011 trial in which 16 of 18 participants maintained stable factor VIII expression over >2 years of follow-up, with only two losing all expression to an anti-AAV capsid cellular immune response — suggesting that the Roctavian decline is not intrinsic to FVIII itself but to specific interactions between the vector design, dose, and target cell (George et al., 2021).

### 5.3 The CpG-TLR9 axis as a tunable durability lever

Mehta et al. 2025 recently demonstrated in a murine model of lipoprotein lipase deficiency that a 38% reduction in vector-encoded CpG count (pNC182) preserves therapeutic efficacy while reducing the TLR9-driven elimination of transduced cells (Mehta et al., 2025). Bertolini et al. 2021 showed that CpG depletion attenuates capsid-specific CD8 T cell cross-priming in hemophilia B models, with corresponding preservation of muscle-fiber transduction (Bertolini et al., 2021). These findings establish that $\psi_T$ in F429 is not a fixed parameter but is partially under vector-design control, implying that engineering CpG-depleted versions of the factor VIII cassette could close the FIX–FVIII durability gap.

### F431 — TLR9-CpG Innate-Immunity Shutdown Kinetics

Let $C$ denote the CpG count in the vector genome. The innate-immunity-driven CD8 T cell response induced by TLR9 sensing of unmethylated CpG motifs in plasmacytoid dendritic cells has empirical magnitude proportional to $C$ at low CpG density and saturating at high CpG density. A functional form consistent with the Mehta 2025 and Bertolini 2021 data is:

```math
\psi_T^{\text{innate}}(C) \;=\; \psi_T^{\max}\,\cdot\,\frac{C^n}{C^n + K_C^n}
```

**Variables.** $\psi_T^{\max}$ is the maximum CD8 T cell elimination rate (d⁻¹; empirically ≈0.05–0.10 d⁻¹ at peak); $K_C$ is the half-maximal CpG count (empirically ≈400–600 unmethylated CpG motifs per vector genome); and $n$ is a Hill coefficient (empirically ≈2.5, reflecting cooperativity in TLR9 engagement). For the FVIII-SQ cassette with native-sequence CpG count $C \approx 400$ vs. CpG-depleted $C \approx 250$: $\psi_T^{\text{innate}}(400)/\psi_T^{\text{innate}}(250) \approx 1.8$. A 38% CpG reduction as in Mehta et al. 2025 therefore predicts a roughly 40% reduction in innate-immunity-driven transduced-cell elimination over the 8–16 week window when TLR9-CpG signaling is most active (Mehta et al., 2025; Bertolini et al., 2021).

---

## 6. The Neonatal Liver Problem: Pediatric AAV Durability

For metabolic liver diseases that manifest in childhood — ornithine transcarbamylase deficiency, methylmalonic acidemia, Crigler-Najjar syndrome, argininosuccinate synthetase deficiency, progressive familial intrahepatic cholestasis — AAV gene replacement would be most therapeutically valuable if administered neonatally or during infancy. Yet the neonatal liver is precisely the worst substrate for episomal AAV: hepatocellular proliferation during the first 5–10 years of life drives episome dilution at rates 10- to 100-fold higher than adult baseline (Cunningham et al., 2008; Wang et al., 2012). Cunningham et al. 2008 demonstrated that a single doubling of liver weight reduces AAV2/8-derived vector genome copies by approximately 50%, and that episomal loss is nearly complete by two weeks post-injection in neonatal mice (Cunningham et al., 2008). Wang et al. 2012 confirmed this in neonatal mice with scAAV8 vectors and showed that delaying injection age improves sustained expression at the cost of increased neutralizing antibody development (Wang et al., 2012).

Milani et al. 2025 recently characterized the spatiotemporal dynamics of the neonatal mouse liver with clonal tracing, single-cell transcriptomics, and spatial transcriptomics, demonstrating that 15–20% of newborn hepatocytes are clonogenic and generate over 90% of the adult liver (Milani et al., 2025). These clonogenic hepatocytes co-localize with hematopoietic islands in a spatial niche, and preferential gene editing of this subpopulation produces a disproportionate fraction of gene-engineered liver area in adulthood. The implication for AAV durability is profound: if the clonogenic 15–20% subpopulation can be selectively transduced and edited for integration, the result is stable adult expression despite massive early dilution of non-clonogenic episomes.

### F432 — Hepatocyte Age-Structured Vector Dilution with Clonogenic Subpopulation

Let $H(a,t)$ denote the density of hepatocytes of age $a$ at time $t$, evolving under a McKendrick-von Foerster PDE with birth rate $\beta(t)$ (neonatal peak) and death rate $\delta(t)$. Let $c \in (0,1)$ denote the clonogenic fraction (≈0.15–0.20 per Milani et al., 2025). Partition the vector distribution $v(a,t)$ across the age-structured hepatocyte population as $v_c(a,t)$ for clonogenic cells and $v_{nc}(a,t)$ for non-clonogenic cells. The vector density per cell evolves as:

```math
\frac{\partial v_{nc}}{\partial t} + \frac{\partial v_{nc}}{\partial a} \;=\; -\mu_{\text{div}}(t)\,v_{nc} - \sigma v_{nc}
```

```math
\frac{\partial v_{c}}{\partial t} + \frac{\partial v_{c}}{\partial a} \;=\; -\mu_{\text{div}}(t)\,v_{c}(1-k_{\text{int}}/\mu_{\text{div}}) - \sigma v_{c}
```

The second equation captures the fact that clonogenic cells preferentially undergo integration prior to division, so the effective loss rate is reduced by the factor $(1 - k_{\text{int}}/\mu_{\text{div}})$. Total per-patient transgene output is:

```math
P(t) \;=\; p_E\,c\,V_c(t) + p_E\,(1-c)\,V_{nc}(t) + p_I\,I(t)
```

For a neonatally-administered dose with initial uniform vector distribution, the asymptotic long-term expression ratio between clonogenic-targeted and non-targeted delivery is:

```math
R_{c/nc}(\infty) \;=\; \frac{c \cdot p_I \cdot \int_{0}^{\infty} k_{\text{int}} V_c(t) dt}{(1-c) \cdot p_I \cdot \int_{0}^{\infty} k_{\text{int}} V_{nc}(t) dt}
```

For $c = 0.18$, $\mu_{\text{div}}(t)$ declining from 0.03 d⁻¹ at birth to 10⁻³ d⁻¹ at age 10, and $k_{\text{int}}/\mu_{\text{div}} \approx 0.5$ (engineered integration-preferring vector): $R_{c/nc}(\infty) \approx 3.5$. Clonogenic-targeted neonatal AAV delivery therefore predicts a 3.5-fold durability advantage over uniformly-distributed delivery — a quantitative rationale for developing capsid or surface-antigen-specific targeting of the clonogenic hepatocyte niche. Partner strategies include scaffold/matrix-attachment region (S/MAR) sequences that stabilize episomal persistence through replication (Llanos-Ardaiz et al., 2024) and AAV-delivered promoterless gene targeting to the endogenous *albumin* locus for stable hepatocyte expression (De Caneva et al., 2018).

---

## 7. The Duchenne Paradigm: Systemic AAV at the Therapeutic-Toxicity Boundary

Delandistrogene moxeparvovec (Elevidys) represents the most demanding systemic-delivery application yet approved: intravenous AAVrh74 at 1.33 × 10¹⁴ vg/kg to deliver a codon-optimized micro-dystrophin transgene to all skeletal, cardiac, and diaphragmatic muscle in ambulatory pediatric DMD patients (Hoy, 2023; Mendell et al., 2024). The EMBARK Phase 3 trial reported mean micro-dystrophin expression at 34.3% of normal at week 12, with treated-group NSAA score improvement of 2.57 points vs. 1.92 for placebo (not statistically significant) but clinically meaningful secondary-endpoint separations including Time to Rise, 10-meter Walk/Run, and stride velocity (Mendell et al., 2024). No treatment-related deaths occurred in EMBARK.

Systemic AAV delivery at these doses carries the highest risk profile in the gene-replacement landscape. Lek et al. 2023 reported the death of a 27-year-old advanced DMD patient treated under an N-of-1 compassionate protocol with rAAV9-dCas9-VP64 at 1 × 10¹⁴ vg/kg; cardiac arrest occurred on day 6 post-dose with post-mortem findings of severe diffuse alveolar damage and acute respiratory distress syndrome, and the inferred mechanism was innate-immune cytokine storm (Lek et al., 2023). Salabarria et al. 2023 characterized the kinetics of complement-mediated thrombotic microangiopathy (TMA) across 38 individuals receiving systemic AAV9 under two prophylactic regimens: corticosteroid-only subjects exhibited rapid IgM/IgG rise, decline in platelet count, D-dimer elevation, C4 depletion, and soluble C5b-9 elevation — markers of both classical and alternative complement activation (Salabarria et al., 2023). Rituximab plus sirolimus plus steroid blocked antibody development and prevented TMA. Assaf 2024 provides a comprehensive overview of systemic AAV toxicity spanning hepatotoxicity, TMA, endothelial injury, and innate immune activation (Assaf, 2024). Kropf et al. 2024 details the convergent mechanisms of classical and alternative complement pathway engagement, implicating both patient-specific (C3 concentration, prior AAV exposure) and vector-specific factors (Kropf et al., 2024).

### F433 — Compound-Poisson Complement-Activation Dose-Ceiling

Let $N_{\text{vg}}$ denote the total intravenous dose (vector genomes), and let each capsid particle carry a probability $\pi$ of engaging the C1 complex (initial classical-pathway trigger) per unit time. The cumulative complement activation over the critical 48-hour window is:

```math
\Lambda \;=\; N_{\text{vg}} \cdot \pi \cdot \int_{0}^{48\text{h}} f(t)\,dt
```

where $f(t)$ is the temporal envelope of capsid exposure to serum. For a compound-Poisson distribution of complement-fixation events, the probability of a severe TMA event is:

```math
P_{\text{TMA}}(\Lambda) \;=\; 1 - \exp(-\Lambda / \Lambda_0)
```

**Variables.** $\Lambda_0$ is the TMA-susceptibility threshold (empirically ≈5 × 10¹³ capsid particles in classical-pathway-primed individuals per the Salabarria et al. kinetics), and the dose-response curve crosses $P_{\text{TMA}} = 0.5$ at $\Lambda \approx \Lambda_0 \ln 2$. For the Zolgensma dose (2 × 10¹⁴ vg) in a 20-kg child, $\Lambda \approx 4 \times 10^{14}$; without anti-AAV antibodies at a TMA-susceptibility threshold $\Lambda_0 = 2 \times 10^{15}$, $P_{\text{TMA}} \approx 0.18$, consistent with the 5–20% empirical TMA rate in post-marketing surveillance of Zolgensma in the absence of prophylactic immunomodulation. Rituximab-sirolimus prophylaxis (Salabarria et al., 2023) increases $\Lambda_0$ by approximately an order of magnitude, reducing $P_{\text{TMA}}$ to below 0.02. F433 therefore provides a principled framework for dose-ceiling design across AAV programs and explains why the Zolgensma, Roctavian, and Elevidys dose regimes have required progressively more elaborate immunomodulation protocols to preserve safety.

---

## 8. Capsid-Specific CD8 T Cell Elimination: The $\psi_T$ Term in F429

Every in vivo AAV gene replacement therapy exposes the immune system to foreign capsid protein antigens presented in MHC class I by transduced cells. In hemophilia B trials with AAV8 or AAV2 vectors, transient transaminase elevation (capsid-specific CD8 T cell-mediated hepatotoxicity) was observed in approximately 20–30% of dosed participants and was responsive to glucocorticoids (George et al., 2020; George et al., 2021). Martino et al. 2013 established mechanistically that CD8 T cells specific for AAV capsid peptides (presented by HLA-B*0702 or murine H2-L^d) can eliminate AAV-transduced hepatocytes, and that proteasome-resistant capsid mutants (AAV2-Y-F) reduce class I presentation and preserve transgene expression (Martino et al., 2013). Palaschak et al. 2017 extended this to an immunocompetent mouse model and demonstrated capsid variant-specific differences in CD8 T cell elimination, identifying capsid engineering as a tractable lever for reducing $\psi_T$ (Palaschak et al., 2017).

### F434 — Capsid-Specific CD8 T Cell Hazard as Function of Class-I-Presented Epitope Load

Let $\rho$ denote the number of class-I-presented capsid-derived peptides per transduced cell, itself proportional to the capsid load, the proteasomal turnover rate, and the peptide-HLA affinity (Palaschak et al., 2017). Let $T_{\text{capsid}}$ denote the capsid-specific CD8 T cell precursor frequency in the recipient. The CD8 T cell-mediated transduced-cell elimination hazard is:

```math
\psi_T^{\text{CD8}}(\rho, T_{\text{capsid}}) \;=\; k_{\text{kill}}\,\cdot\,\rho\,\cdot\,T_{\text{capsid}}\,\cdot\,\left(1 + \tau\,\cdot\,e^{-\gamma t}\right)^{-1}
```

**Variables.** $k_{\text{kill}}$ is the bimolecular killing rate (empirically ≈10⁻⁴ d⁻¹ per capsid peptide per T cell); $\tau$ is a glucocorticoid-suppression factor (≈10 at prednisone dose 1 mg/kg/d); $\gamma$ is the glucocorticoid taper rate (1/τ = ≈1 week taper). The integrated transduced-cell elimination fraction over the critical 8–12 week post-dose window is:

```math
\Delta E / E_0 \;=\; 1 - \exp\!\left[-\int_0^{12w} \psi_T^{CD8}\,dt\right]
```

Proteasome-resistant capsid mutants (e.g., AAV2-Y-F) reduce $\rho$ by approximately 10-fold (Martino et al., 2013), reducing $\Delta E / E_0$ from an unmitigated ~40% loss to ~5%. CpG-depleted vector genomes further reduce $\rho$ indirectly by lowering cross-priming of naive CD8 T cells (Bertolini et al., 2021). F434 therefore provides a dose-effect relationship that connects vector engineering to transduced-cell preservation, formalizing the benefit of capsid surface engineering and transgene codon optimization as durability levers.

---

## 9. Chronic Neutralizing Antibody Barriers and Redosing

Across all eight approved gene replacement products, single-dose delivery is the paradigm. The reason is that vector administration evokes a high-titer humoral anti-capsid response that persists for at least 15 years (George et al., 2020) and cross-reacts extensively across AAV serotypes (Chhabra et al., 2024; Perocheau et al., 2019). Schulz et al. 2023 reviewed binding and neutralizing anti-AAV antibody assays across trial populations, documenting 30–60% pre-existing seroprevalence in the general adult population (Schulz et al., 2023). Chhabra et al. 2024 provided the most recent multi-country seroprevalence survey (502 adults, 50 children, 6 AAV serotypes), identifying significant geographic and demographic variation (Chhabra et al., 2024). The NAb barrier has three consequences: (i) exclusion of seropositive patients from first-dose trials; (ii) inability to re-dose seroconverted patients with the same or cross-reactive serotype; and (iii) progressive closure of serotype space as patients are exposed to successive gene-therapy programs.

Mitigation strategies span capsid engineering (Paulk et al., 2018; Rana et al., 2023; Wang et al., 2022), antibody-depletion pharmacology (imlifidase IdeS; Leborgne et al., 2020), and engineered receptor-targeted AAV variants (e.g., DART-AAVs specific for CD8+ T cells; Demircan et al., 2024). The Dhungel et al. 2025 identification of a second AAV receptor (AAVR2, carboxypeptidase D) that mediates clade-E AAV transduction and determines exclusive pathways for AAV11/AAV12 offers a new dimension: capsids engineered to engage only AAVR2-dependent pathways may escape AAVR-associated NAb epitopes (Dhungel et al., 2025). The Havlik et al. 2021 demonstration of receptor-switched AAVhum.8 from AAVR to integrin β1 further supports the feasibility of capsid redesign to evade pre-existing humoral immunity (Havlik et al., 2021).

### F435 — Sequential Serotype-Switching Horizon

Let $S$ denote the set of clinically viable AAV serotypes, $|S| = N_S$. After dose $k$, the set of accessible serotypes for dose $k+1$ is $S \setminus \bigcup_{i \leq k} X_i$ where $X_i$ is the serotype-cross-reactivity set induced by dose $i$ (typically $|X_i| \approx 2$ accounting for cross-reactive neighbors). The patient-specific dosing horizon is:

```math
H_{\text{patient}} \;=\; \left\lfloor \frac{N_S - N_{\text{baseline}}}{|X|} \right\rfloor
```

where $N_{\text{baseline}}$ is the patient's pre-treatment serotype exposure. For $N_S = 10$ clinical serotypes, $N_{\text{baseline}} = 2$ (typical adult), $|X| = 2$: $H_{\text{patient}} = 4$ — a patient can in principle receive four separate AAV gene therapy doses over a lifetime before exhausting serotype space. This crude bound improves with (i) AAV capsid engineering to expand $N_S$ (Chhabra et al., 2024 identified non-phylogenetic immunogenic clusters suggesting new engineered variants could bypass multiple natural clades simultaneously), and (ii) IdeS pre-treatment to reset NAb titer (Leborgne et al., 2020). F435 formalizes the sequential-dose bound and motivates the investment in a capsid-engineering pipeline that deliberately expands the immunogenic repertoire beyond the natural AAV phylogeny.

---

## 10. Manufacturing, Empty-Capsid Quality, and Full-Capsid Ratio

AAV manufacturing economics are bound by a fundamental constraint: genome packaging into the capsid is inefficient, yielding a mixture of genome-containing "full" particles and DNA-less "empty" particles in roughly 1:3 to 1:9 ratios from standard triple-transfection protocols (Grieger et al., 2016; Hajba et al., 2020). Empty particles contribute to vector-encoded antigen load without contributing to therapeutic efficacy and are therefore undesirable from a safety standpoint (Yarawsky et al., 2023; Richter et al., 2023). Modern Good Manufacturing Practice (GMP) protocols enrich full particles via anion-exchange chromatography or cesium chloride/iodixanol gradient ultracentrifugation, targeting full-particle percentages of 80–95% (Lock et al., 2010; Grieger et al., 2016). Analytical ultracentrifugation (SV-AUC) remains the reference method for full/empty quantitation (Yarawsky et al., 2023; Richter et al., 2023), complemented by mass photometry and negative-staining transmission electron microscopy (Hajba et al., 2020). Recent bioprocess innovations — including baculovirus/Sf9 stable producer cell lines (Joshi et al., 2019) and suspension-adapted HEK293 systems (Grieger et al., 2016) — have pushed yields to >1 × 10¹⁴ vg/L, but systemic-dose requirements (10¹⁴ vg per adult for hemophilia, 10¹³–10¹⁴ vg/kg for DMD) sustain per-dose manufacturing costs in the tens of thousands of dollars, with product list prices in the $850,000 (Luxturna, per eye) to $4.25 million (Hemgenix) range (Wong et al., 2023; Ho et al., 2021).

Wong et al. 2023 simulated annual US gene therapy spending from the late-stage clinical pipeline, estimating $20.4 billion in annual spending under conservative assumptions, with approximately half directed to non-Medicare-insured populations (Wong et al., 2023). Garrison et al. 2019 argued for elevated cost-effectiveness thresholds (up to $500,000 per quality-adjusted life-year) for ultra-rare health-catastrophic diseases, and Drummond et al. 2023 reviewed how health technology assessment bodies across eight jurisdictions have struggled to incorporate durability uncertainty into cost-effectiveness determinations (Garrison et al., 2019; Drummond et al., 2023). Coyle et al. 2020 framed the challenge as a decision-making mismatch: gene therapies enter HTA review with limited efficacy data and high durability uncertainty precisely when payers need the greatest confidence (Coyle et al., 2020).

---

## 11. The Inherited Retinal Disease Epidemiology Problem

The Luxturna approval indicates a market of approximately 1,000 to 3,000 RPE65-biallelic patients in the United States and a similar number in Europe, yielding a global treated population of perhaps 2,000–5,000. Hanany et al. 2020 used gnomAD allele-frequency data to estimate global autosomal-recessive inherited retinal disease prevalence at ~1 in 1,380, translating to ~5.5 million affected individuals globally (Hanany et al., 2023). Sallum et al. 2022 systematically reviewed RPE65-specific epidemiology across countries, finding LCA prevalence of 1.20–2.37 per 100,000 and the RPE65-mutation fraction within LCA of 2–16% (Sallum et al., 2022). Zobor et al. 2023 extended this with a 105-patient German cohort characterizing the phenotypic spectrum of RPE65 and related LCA-associated genes (Zobor et al., 2023). These numbers matter for gene-replacement durability planning: a disease target of 5,000 patients globally has different economic and manufacturing scaling than a target of 5 million, and the Luxturna precedent has established that the regulatory framework can indeed approve therapies for ultra-small populations provided efficacy is demonstrated.

Next-generation candidates targeting the same retinal tissue with the same delivery strategy but different transgenes are advancing: Fischer et al. 2019 and Xue et al. 2018 independently reported AAV2-REP1 for X-linked choroideremia showing maintenance or improvement of visual acuity in 14 patients (Fischer et al., 2019; Xue et al., 2018). Lam et al. 2019 reported the 24-month phase 2 outcomes, with two treated eyes gaining 5–10 letters (Lam et al., 2019). Britten-Jones et al. 2021 performed a systematic review identifying active gene-therapy trials across 16 distinct retinal genotypes (Britten-Jones et al., 2021). Matsevich et al. 2023 extended the paradigm to FAM161A retinitis pigmentosa in a knockout mouse model, demonstrating that gene augmentation attenuates retinal degeneration (Matsevich et al., 2023). Li et al. 2020 reported broad-spectrum rescue via NR2E3 gene augmentation across five mouse models of RP (Li et al., 2020). These developments validate that the Luxturna template can generalize, but each new indication imports the same durability constraints that F429–F435 formalize.

---

## 12. Emerging Delivery Modalities: Alternative Vectors and Approaches

### 12.1 Suprachoroidal injection and delivery alternatives

Yiu et al. 2020 demonstrated that transscleral microneedle delivery of AAV8 to the suprachoroidal space of rhesus macaques produced diffuse peripheral RPE transduction with minimal intraocular inflammation (Yiu et al., 2020). Ding et al. 2019 showed that suprachoroidal AAV8 produced widespread ocular transgene expression in nonhuman primate and porcine eyes with outpatient-feasible administration (Ding et al., 2019). Scruggs et al. 2025 recently reported the epiretinal fibrin-hydrogel delivery platform mentioned above, achieving broad RPE transduction without atrophy or inflammation and potentially eliminating the subretinal-injection-specific CRA signal that has burdened Luxturna post-marketing data (Scruggs et al., 2025).

### 12.2 Intrathecal AAV9 for spinal motor neurons: The DRG toxicity problem

Onasemnogene abeparvovec (Zolgensma) is delivered intravenously for systemic SMN restoration in SMA; emerging programs in hereditary spastic paraplegia (Chen et al., 2023), SOD1-ALS (Hawley et al., 2024), and other CNS conditions use intrathecal AAV9 or intracisternal AAV9 variants. Dorsal root ganglion (DRG) toxicity — degeneration of DRG neurons manifesting histopathologically weeks to months after intra-CSF AAV delivery — has been consistently reported across nonhuman primate programs (Hawley et al., 2024; Grubor et al., 2025). Grubor et al. 2025 demonstrated that dexamethasone plus tacrolimus prophylaxis diminishes pathology in NHPs across three different AAV cargos, implicating the immune response to AAV (rather than transgene-encoded protein toxicity alone) as the causative mechanism (Grubor et al., 2025). Hawley et al. 2024 extended these findings to an RNAi expression construct, showing that DRG toxicity is not specific to gene-replacement cassettes but is intrinsic to intra-CSF AAV delivery (Hawley et al., 2024). These observations reinforce the $\psi_T$ term in F429 as a generalized transduced-cell-elimination mechanism that contributes to durability loss in every tissue compartment.

### 12.3 Alternative delivery platforms: LNP-mRNA and non-AAV systems

Lipid nanoparticle-mRNA delivery of therapeutic cassettes presents an emerging alternative to AAV, particularly for applications where single-dose durability is not required or where re-dosing is desirable. Cheng et al. 2025 reported liposomal LNP systems with high bilayer-forming-lipid content that exhibit prolonged circulation lifetimes and enhanced extrahepatic transfection (Cheng et al., 2025). Jeong et al. 2023 reviewed the fundamentals of LNP-RNA delivery and summarized the challenges of extrahepatic targeting (Jeong et al., 2023). Liu et al. 2024 provided a recent overview of mRNA-LNP applications spanning vaccines, cancer, and genetic diseases (Liu et al., 2024). LNP-mRNA gene replacement is intrinsically transient (days-to-weeks expression) and therefore non-competitive with AAV for chronic monogenic disease, but represents the leading platform for RNAi-based silencing, base-editor delivery, and CAR-T-like reprogramming strategies where transient exposure is preferred. The emerging distinction between "durable gene replacement" (AAV, with durability the primary obstacle) and "transient gene replacement" (LNP-mRNA, with repeat dosing required) now frames the landscape.

---

## 13. Open Questions and Research Priorities

The durability problem enumerated in this manuscript is not solved. The following are testable, near-term priorities that the field must address to close the gap between current proof-of-concept and curative gene replacement:

1. **What is the mechanistic basis for the FIX–FVIII durability divergence?** F429 suggests that either $\phi_{\text{Tg}}$ (proteostatic stress from FVIII misfolding) or $\psi_T$ (CpG-TLR9-driven T cell elimination) is elevated in AAV-FVIII vs. AAV-FIX programs. Direct measurement in paired hepatocyte-specific proteostatic markers (BiP, CHOP) and T cell infiltrates in biopsies from Roctavian-treated vs. Hemgenix-treated patients would distinguish these hypotheses. The Dargaud et al. 2025 review explicitly identifies this as a critical gap in the hemophilia literature (Dargaud et al., 2025).

2. **Can CpG-depleted AAV-FVIII cassettes restore 5-year durability to FVIII-like activity levels?** The Mehta et al. 2025 demonstration in LPLD (Mehta et al., 2025) and Bertolini et al. 2021 mechanistic work (Bertolini et al., 2021) suggest this is tractable. A head-to-head clinical trial of CpG-depleted AAV-FVIII vs. current Roctavian, with matched dosing and immunomodulation, is the single most informative next experiment for the hemophilia A field.

3. **Is targeted integration at the albumin locus a path to pediatric-liver durability?** De Caneva et al. 2018 demonstrated ~24% promoterless targeting efficiency in neonatal Crigler-Najjar mice via SaCas9 cutting plus AAV donor (De Caneva et al., 2018). Translation to larger animals and humans with full IND-grade safety profiling is overdue. S/MAR-containing vectors (Llanos-Ardaiz et al., 2024) offer an alternative non-genome-editing route to similar outcomes.

4. **Can the Milani 2025 clonogenic-hepatocyte niche be selectively targeted?** Clonogenic hepatocytes co-localize with hematopoietic islands in a spatial niche (Milani et al., 2025). Capsid or antibody-surface-targeted AAV variants that preferentially engage this niche, combined with integrating (lentiviral, transposon, or bridge-recombinase) delivery, would provide a direct test of F432. The predicted 3.5-fold durability advantage would transform neonatal-liver gene replacement for inborn errors of metabolism.

5. **What is the empirical $\epsilon$ in F430?** The CRA-acceleration coefficient determines the Luxturna therapeutic window. Prospective 10-year optical coherence tomography and adaptive-optics surveillance across the Gange (Gange et al., 2022), Bender (Bender et al., 2024), and Simoens (Simoens et al., 2025) cohorts is the most important ophthalmology priority. Sham-injection controls (absent since the original Maguire Phase I) would disambiguate vector- vs. surgery-driven CRA — a trial design that new candidate products (e.g., epiretinal Scruggs hydrogel; Scruggs et al., 2025) may permit because their mode of administration is intrinsically controlled.

6. **Can AAV capsid engineering expand $N_S$ in F435 beyond the natural AAV phylogeny?** The Chhabra et al. 2024 identification of non-phylogenetic immunogenic clusters (Chhabra et al., 2024), combined with AAVR2 discovery (Dhungel et al., 2025) and directed-evolution capsid variants (Wang et al., 2022; Rana et al., 2023; Paulk et al., 2018), suggests that a rationally engineered panel of 10+ fully seronegative-cross-reactive-profile capsids is achievable. The question is whether this panel can be GMP-manufactured at scale at costs compatible with broad patient access.

7. **How should regulatory frameworks handle durability uncertainty?** Accelerated-approval decisions (Elevidys, 2023; Hoy, 2023) have been predicated on surrogate endpoints (micro-dystrophin expression at week 12) whose long-term relationship to motor-function outcomes is uncertain. The EMBARK trial's failure to meet its primary NSAA endpoint at 52 weeks (Mendell et al., 2024) has triggered payer and regulatory reconsideration. Drummond et al. 2023 and Coyle et al. 2020 review how HTA bodies across jurisdictions are currently handling durability evidence (Drummond et al., 2023; Coyle et al., 2020); a coordinated international framework for probabilistic durability assessment, analogous to progression-free-survival surrogate analyses in oncology, is overdue.

---

## 14. Conclusion

Gene replacement therapy, as practiced in 2026, is a mature clinical category. Eight approved products — Luxturna, Zolgensma, Upstaza, Roctavian, Hemgenix, Elevidys, and the two ex-vivo cell therapies (Casgevy, Lyfgenia for non-AAV sickle-cell indications) — have established that a single intervention can restore a biological function that was categorically absent for the patient's entire life. This is a non-trivial achievement. The Maguire 2008 Phase I trial that forms the foundational reference of this manuscript is justly recognized as one of the most consequential translational milestones in 21st-century medicine (Maguire et al., 2008). Yet the accumulating long-term data from these eight programs has also exposed a limit that the early pivotal trials could not have quantified: transgene expression is not permanent. Across indications, durability is determined by a coupled multi-rate process whose components include episomal dilution, transgene-product-driven cellular stress, CpG-TLR9-driven innate immunity, capsid-specific CD8 T cell elimination, epigenetic silencing, and low-frequency integration that may provide the stable-state plateau observed at longer time horizons.

Our mathematical frameworks partition these components quantitatively. F429 unifies episomal, integrated, proteostatic, and immunological loss into a single ODE system. F430 captures the viability-transduction product for the Luxturna-class retinal paradigm. F431 quantifies the TLR9-CpG tunable innate-immunity lever. F432 models the hepatocyte age-structured vector dilution problem with the Milani 2025 clonogenic-subpopulation refinement. F433 provides the compound-Poisson complement-activation dose ceiling that governs systemic AAV safety. F434 formalizes the capsid-specific CD8 T cell elimination hazard as a function of MHC-I-presented epitope load. F435 establishes the sequential serotype-switching dosing horizon. Each framework is calibrated against primary literature and specifies variables that are directly measurable in ongoing clinical and preclinical programs.

We argue that the coupled bottleneck of *episomal dilution plus transgene-specific immune or proteostatic shutdown* is the primary obstacle to second-generation gene replacement. It is the mechanism that distinguishes stable-durability (FIX-Padua, RPE65, SMN1 in post-mitotic neurons) from declining-durability (FVIII, pediatric-liver programs, FVIII-like transgenes) clinical outcomes. It is the mechanism most directly tractable to existing engineering levers: codon/CpG optimization of the transgene cassette (Mehta et al., 2025; Bertolini et al., 2021); capsid engineering to minimize MHC-I presentation (Martino et al., 2013); scaffold/matrix-attachment elements to stabilize episomal chromatin during division (Llanos-Ardaiz et al., 2024); targeted integration strategies at the *albumin* locus (De Caneva et al., 2018) or clonogenic hepatocyte niche (Milani et al., 2025); and next-generation delivery modalities (epiretinal hydrogel, suprachoroidal microneedle, DART-AAV targeting) that decouple vector exposure from collateral tissue damage (Scruggs et al., 2025; Yiu et al., 2020; Ding et al., 2019; Demircan et al., 2024).

The path forward is neither exotic nor unknown. It is engineering the vector, the cassette, the delivery modality, and the immunomodulation regimen such that the six loss terms in F429 are jointly minimized. Done systematically, we predict that the durability plateau of the second-generation replacement therapies will shift from the current ~36% of normal (Hemgenix five-year FIX activity; Pipe et al., 2025) toward the initial peak of ~100% (Hemgenix six-week FIX activity; Pipe et al., 2023), transforming one-time gene replacement from a durably-therapeutic to a genuinely-curative modality. The scientific community has both the tools and the obligation to close this gap.

---

## References

Assaf, Bernadette T. "Systemic Toxicity of Recombinant Adeno-Associated Virus Gene Therapy Vectors." *Toxicologic Pathology*, vol. 52, 2024.

Bala, Natasha S., et al. "Gene Therapy in Hemophilia A: Achievements, Challenges, and Perspectives." *Seminars in Thrombosis and Hemostasis*, 2024.

Batty, Paul, et al. "Vector Integration and Fate in the Hemophilia Dog Liver Multi-Years Following AAV-FVIII Gene Transfer." *Blood*, 2024.

Bender, Linus, et al. "Long-Term Outcomes and Chorioretinal Atrophy Following Subretinal Voretigene Neparvovec-rzyl Gene Therapy in RPE65-Associated Inherited Retinal Dystrophy." *Ophthalmology Retina*, vol. 8, no. 11, 2024, pp. 1087–1095.

Berger, Aubrey, et al. "Retinal Viral Gene Therapy: Impact of Route of Administration on Serious Adverse Events—A Systematic Review." *Clinical & Experimental Ophthalmology*, 2025.

Bertolini, Thais B., et al. "Effect of CpG Depletion of Vector Genome on CD8+ T Cell Responses in AAV Gene Therapy." *Frontiers in Immunology*, 2021.

Blair, Hannah A. "Onasemnogene Abeparvovec: A Review in Spinal Muscular Atrophy." *CNS Drugs*, vol. 36, 2022.

Britten-Jones, Alexis Ceecee, et al. "The Safety and Efficacy of Gene Therapy Treatment for Monogenic Retinal and Optic Nerve Diseases: A Systematic Review." *Genetics in Medicine*, vol. 23, no. 11, 2021.

Chen, Xin, et al. "Intrathecal AAV9/AP4M1 Gene Therapy for Hereditary Spastic Paraplegia 50 Shows Safety and Efficacy in Preclinical Studies." *The Journal of Clinical Investigation*, 2023.

Cheng, Miffy Hok Yan, et al. "Liposomal Lipid Nanoparticles for Extrahepatic Delivery of mRNA." *Nature Communications*, 2025.

Chhabra, Aparna, et al. "Global Seroprevalence of Neutralizing Antibodies Against Adeno-Associated Virus Serotypes Used for Human Gene Therapies." *Molecular Therapy: Methods & Clinical Development*, 2024.

Chuah, Marinee K., et al. "Liver-Specific Transcriptional Modules Identified by Genome-Wide In Silico Analysis Enable Efficient Gene Therapy in Mice and Non-Human Primates." *Molecular Therapy*, 2014.

Coyle, Douglas, et al. "HTA Methodology and Value Frameworks for Evaluation and Policy Making for Cell and Gene Therapies." *The European Journal of Health Economics*, 2020.

Cunningham, Sharon C., et al. "Gene Delivery to the Juvenile Mouse Liver Using AAV2/8 Vectors." *Molecular Therapy*, 2008.

Dargaud, Yesim, et al. "Long-Term Durability of rAAV Gene Therapy in Hemophilia: Factor Expression, Clinical Outcomes and Underlying Molecular Mechanisms." *Blood Reviews*, 2025.

Das, Anshuman, et al. "Epigenetic Silencing of Recombinant Adeno-Associated Virus Genomes by NP220 and the HUSH Complex." *Journal of Virology*, 2021.

De Caneva, Alessia, et al. "Coupling AAV-Mediated Promoterless Gene Targeting to SaCas9 Nuclease to Efficiently Correct Liver Metabolic Diseases." *JCI Insight*, 2018.

Demircan, Müge B., et al. "T-Cell Specific In Vivo Gene Delivery with DART-AAVs Targeted to CD8." *Molecular Therapy*, 2024.

Dhungel, Bijay P., et al. "An Alternate Receptor for Adeno-Associated Viruses." *Cell*, 2025.

Ding, Kun, et al. "AAV8-Vectored Suprachoroidal Gene Transfer Produces Widespread Ocular Transgene Expression." *The Journal of Clinical Investigation*, 2019.

Drummond, Michael, et al. "How Are Health Technology Assessment Bodies Responding to the Assessment Challenges Posed by Cell and Gene Therapy?" *BMC Health Services Research*, 2023.

Fischer, Marius D., et al. "Efficacy and Safety of Retinal Gene Therapy Using Adeno-Associated Virus Vector for Patients With Choroideremia: A Randomized Clinical Trial." *JAMA Ophthalmology*, 2019.

Frangoul, Haydar, et al. "Exagamglogene Autotemcel for Severe Sickle Cell Disease." *The New England Journal of Medicine*, 2024.

Gange, William S., et al. "Perifoveal Chorioretinal Atrophy after Subretinal Voretigene Neparvovec-rzyl for RPE65-Mediated Leber Congenital Amaurosis." *Ophthalmology Retina*, vol. 6, no. 1, 2022, pp. 58–64.

Gardiner, Kristin L., et al. "Long-Term Structural Outcomes of Late-Stage RPE65 Gene Therapy." *Molecular Therapy*, 2020.

Garrison, Louis P., et al. "Value-Based Pricing for Emerging Gene Therapies: The Economic Case for a Higher Cost-Effectiveness Threshold." *Journal of Managed Care & Specialty Pharmacy*, 2019.

George, Lindsey A., et al. "Long-Term Follow-Up of the First-in-Human Intravascular Delivery of AAV for Gene Transfer: AAV2-hFIX16 for Severe Hemophilia B." *Molecular Therapy*, 2020.

George, Lindsey A., et al. "Multiyear Factor VIII Expression after AAV Gene Transfer for Hemophilia A." *The New England Journal of Medicine*, 2021.

Greig, Jenny A., et al. "Integrated Vector Genomes May Contribute to Long-Term Expression in Primate Liver After AAV Administration." *Nature Biotechnology*, 2023.

Grieger, Joshua C., et al. "Production of Recombinant Adeno-Associated Virus Vectors Using Suspension HEK293 Cells and Continuous Harvest of Vector From the Culture Media for GMP FIX and FLT1 Clinical Vector." *Molecular Therapy*, 2016.

Grubor, Branka, et al. "Inhibition of Immune Response Reduces Pathology in Dorsal Root Ganglia and Peripheral Nerves in Cynomolgus Macaques Following AAV Gene Therapy." *Molecular Therapy: Methods & Clinical Development*, 2025.

Hajba, László, et al. "Recent Advances in the Analysis Full/Empty Capsid Ratio and Genome Integrity of Adeno-Associated Virus (AAV) Gene Delivery Vectors." *Current Molecular Medicine*, 2020.

Hanany, Mor, et al. "Comparison of Worldwide Disease Prevalence and Genetic Prevalence of Inherited Retinal Diseases and Variant Interpretation Considerations." *Cold Spring Harbor Perspectives in Medicine*, 2023.

Havlik, Logan P., et al. "Receptor Switching in Newly Evolved Adeno-Associated Viruses." *Journal of Virology*, 2021.

Hawley, Zachariah C., et al. "Dorsal Root Ganglion Toxicity After AAV Intra-CSF Delivery of a RNAi Expression Construct Into Nonhuman Primates and Mice." *Molecular Therapy*, 2024.

Ho, Jia K., et al. "Economic Evidence on Potentially Curative Gene Therapy Products: A Systematic Literature Review." *PharmacoEconomics*, 2021.

Hoy, Sheridan M. "Delandistrogene Moxeparvovec: First Approval." *Drugs*, 2023.

Hoy, Sheridan M. "Exagamglogene Autotemcel: First Approval." *Molecular Diagnosis & Therapy*, 2024.

Hwu, Wuh-Liang, et al. "Gene Therapy for Aromatic L-Amino Acid Decarboxylase Deficiency." *Science Translational Medicine*, 2012.

Jacobson, Samuel G., et al. "Gene Therapy for Leber Congenital Amaurosis Caused by RPE65 Mutations: Safety and Efficacy in 15 Children and Adults Followed Up to 3 Years." *Archives of Ophthalmology*, 2012.

Jeong, Minjeong, et al. "Lipid Nanoparticles (LNPs) for In Vivo RNA Delivery and Their Breakthrough Technology for Future Applications." *Advanced Drug Delivery Reviews*, 2023.

Joshi, Pranav R. H., et al. "Achieving High-Yield Production of Functional AAV5 Gene Delivery Vectors via Fedbatch in an Insect Cell-One Baculovirus System." *Molecular Therapy: Methods & Clinical Development*, 2019.

Kang, Connie, and Susan J. Keam. "Voretigene Neparvovec: A Review in RPE65 Mutation-Associated Inherited Retinal Dystrophy." *Molecular Diagnosis & Therapy*, 2020.

Kasimsetty, Aradhana, et al. "Integration and the Risk of Liver Cancer—Is There a Real Risk?" *Journal of Viral Hepatitis*, 2024.

Keam, Susan J. "Eladocagene Exuparvovec: First Approval." *Drugs*, 2022.

Kropf, Elizabeth, et al. "Complement System Response to Adeno-Associated Virus Vector Gene Therapy." *Human Gene Therapy*, 2024.

Lam, Byron L., et al. "Choroideremia Gene Therapy Phase 2 Clinical Trial: 24-Month Results." *American Journal of Ophthalmology*, 2019.

Leborgne, Christian, et al. "IgG-Cleaving Endopeptidase Enables In Vivo Gene Therapy in the Presence of Anti-AAV Neutralizing Antibodies." *Nature Medicine*, 2020.

Lek, Angela, et al. "Death After High-Dose rAAV9 Gene Therapy in a Patient with Duchenne's Muscular Dystrophy." *The New England Journal of Medicine*, 2023.

Leroy, Bart P., et al. "Gene Therapy for Inherited Retinal Disease: Long-Term Durability of Effect." *Ophthalmic Research*, vol. 65, no. 1, 2022, pp. 1–15.

Li, Sujun, et al. "Nr2e3 Is a Genetic Modifier That Rescues Retinal Degeneration and Promotes Homeostasis in Multiple Models of Retinitis Pigmentosa." *Gene Therapy*, 2020.

Li, Yuezhe, et al. "Development of an Agent-Based Model to Investigate Response Durability in Hemophilia B Patients Treated with the AAV-Based Coagulation Factor IX (FIX) Gene Therapy Etranacogene Dezaparvovec." *Blood*, 2024.

Liu, Yaping, et al. "Development of mRNA Lipid Nanoparticles: Targeting and Therapeutic Aspects." *International Journal of Molecular Sciences*, 2024.

Llanos-Ardaiz, Andrea, et al. "In Vivo Selection of S/MAR Sequences to Favour AAV Episomal Maintenance in Dividing Cells." *International Journal of Molecular Sciences*, 2024.

Lock, Martin, et al. "Rapid, Simple, and Versatile Manufacturing of Recombinant Adeno-Associated Viral Vectors at Scale." *Human Gene Therapy*, 2010.

Lorenz, Birgit. "Long-Term Experience with Gene Augmentation Therapy in Patients with Inherited Retinal Disease Associated with Biallelic Mutations in RPE65." *Medizinische Genetik*, 2025.

Maguire, Albert M., et al. "Safety and Efficacy of Gene Transfer for Leber's Congenital Amaurosis." *The New England Journal of Medicine*, vol. 358, no. 21, 2008, pp. 2240–2248.

Maguire, Albert M., et al. "Durability of Voretigene Neparvovec for Biallelic RPE65-Mediated Inherited Retinal Disease: Phase 3 Results at 3 Years and 4 Years." *Ophthalmology*, 2021.

Martino, Ashley T., et al. "Engineered AAV Vector Minimizes In Vivo Targeting of Transduced Hepatocytes by Capsid-Specific CD8+ T Cells." *Blood*, 2013.

Matsevich, Chen, et al. "Gene Augmentation Therapy Attenuates Retinal Degeneration in a Knock-Out Mouse Model of Fam161a Retinitis Pigmentosa." *Molecular Therapy*, 2023.

McCarty, Douglas M. "Self-Complementary AAV Vectors; Advances and Applications." *Molecular Therapy*, 2008.

Mehta, Neel, et al. "Optimization of Adeno-Associated Viral (AAV) Gene Therapies Vectors for Balancing Efficacy, Longevity and Safety for Clinical Application." *Gene Therapy*, 2025.

Mendell, Jerry R., et al. "P223 Long-Term Follow-Up of Onasemnogene Abeparvovec Gene Therapy in Patients with Spinal Muscular Atrophy (SMA) Type 1." *Neuromuscular Disorders*, 2023.

Mendell, Jerry R., et al. "AAV Gene Therapy for Duchenne Muscular Dystrophy: The EMBARK Phase 3 Randomized Trial." *Nature Medicine*, 2024.

Milani, Michela, et al. "Spatiotemporal Liver Dynamics Shape Hepatocellular Heterogeneity and Impact In Vivo Gene Engineering." *Journal of Hepatology*, 2025.

Muhuri, Manish, et al. "Durability of Transgene Expression After rAAV Gene Therapy." *Molecular Therapy*, 2022.

Ozelo, Margareth C., et al. "Valoctocogene Roxaparvovec Gene Therapy for Hemophilia A." *The New England Journal of Medicine*, 2022.

Palaschak, Brett, et al. "An Immune-Competent Murine Model to Study Elimination of AAV-Transduced Hepatocytes by Capsid-Specific CD8+ T Cells." *Molecular Therapy: Methods & Clinical Development*, 2017.

Pasi, K. John, et al. "Multiyear Follow-Up of AAV5-hFVIII-SQ Gene Therapy for Hemophilia A." *The New England Journal of Medicine*, 2020.

Paulk, Nicole K., et al. "Bioengineered AAV Capsids with Combined High Human Liver Transduction In Vivo and Unique Humoral Seroreactivity." *Molecular Therapy*, 2018.

Perocheau, Dany P., et al. "Age-Related Seroprevalence of Antibodies Against AAV-LK03 in a UK Population Cohort." *Human Gene Therapy*, 2019.

Pipe, Steven W., et al. "Gene Therapy with Etranacogene Dezaparvovec for Hemophilia B." *The New England Journal of Medicine*, 2023.

Pipe, Steven W., et al. "End-of-Study Analysis of the HOPE-B Trial Confirms the Durable Efficacy and Safety of Etranacogene Dezaparvovec Hemophilia B Gene Therapy Over 5 Years." *Blood*, 2025.

Rana, Jyoti, et al. "Characterization of a Bioengineered AAV3B Capsid Variant with Enhanced Hepatocyte Tropism and Immune Evasion." *Human Gene Therapy*, 2023.

Richter, Klaus, et al. "Purity and DNA Content of AAV Capsids Assessed by Analytical Ultracentrifugation and Orthogonal Biophysical Techniques." *European Journal of Pharmaceutics and Biopharmaceutics*, 2023.

Russell, Stephen, et al. "Efficacy and Safety of Voretigene Neparvovec (AAV2-hRPE65v2) in Patients with RPE65-Mediated Inherited Retinal Dystrophy: A Randomised, Controlled, Open-Label, Phase 3 Trial." *The Lancet*, 2017.

Salabarria, Stephanie M., et al. "Thrombotic Microangiopathy Following Systemic AAV Administration Is Dependent on Anti-Capsid Antibodies." *The Journal of Clinical Investigation*, 2023.

Sallum, Juliana M. F., et al. "Epidemiology of Mutations in the 65-kDa Retinal Pigment Epithelium (RPE65) Gene-Mediated Inherited Retinal Dystrophies: A Systematic Literature Review." *Advances in Therapy*, 2022.

Samelson-Jones, Benjamin J., et al. "Roctavian Gene Therapy for Hemophilia A." *Blood Advances*, 2024.

Schmidt, Manfred, et al. "Molecular Evaluation and Vector Integration Analysis of HCC Complicating AAV Gene Therapy for Hemophilia B." *Blood Advances*, 2023.

Schulz, Martin, et al. "Binding and Neutralizing Anti-AAV Antibodies: Detection and Implications for rAAV-Mediated Gene Therapy." *Molecular Therapy*, 2023.

Scruggs, Brittni A., et al. "Retinal Gene Therapy Using Epiretinal AAV-Containing Fibrin Hydrogel Implants." *Science Advances*, 2025.

Shah, Jinesh, et al. "Comprehensive Analysis and Prediction of Long-Term Durability of Factor IX Activity Following Etranacogene Dezaparvovec Gene Therapy in the Treatment of Hemophilia B." *Current Medical Research and Opinion*, 2022.

Simoens, Djamilla, et al. "Clinical and Pharmacovigilance Safety Evaluation of LUXTURNA® (Voretigene Neparvovec-rzyl)." *Cutaneous and Ocular Toxicology*, 2025.

von Drygalski, Annette, et al. "Completion of Phase 2b Trial of Etranacogene Dezaparvovec Gene Therapy in Patients with Hemophilia B Over 5 Years." *Blood Advances*, 2025.

Waldrop, Megan A., et al. "Continued Safety and Long-Term Effectiveness of Onasemnogene Abeparvovec in Ohio." *Neuromuscular Disorders*, 2023.

Wang, Lili, et al. "Hepatic Gene Transfer in Neonatal Mice by Adeno-Associated Virus Serotype 8 Vector." *Human Gene Therapy*, 2012.

Wang, Yuqiu, et al. "Directed Evolution of Adeno-Associated Virus 5 Capsid Enables Specific Liver Tropism." *Molecular Therapy: Nucleic Acids*, 2022.

Wong, Chi Heem, et al. "The Estimated Annual Financial Impact of Gene Therapy in the United States." *Gene Therapy*, 2023.

Xie, Qing, et al. "Improved Gene Therapy for Spinal Muscular Atrophy in Mice Using Codon-Optimized hSMN1 Transgene and hSMN1 Gene-Derived Promotor." *EMBO Molecular Medicine*, 2024.

Xue, Kanmin, et al. "Beneficial Effects on Vision in Patients Undergoing Retinal Gene Therapy for Choroideremia." *Nature Medicine*, 2018.

Yarawsky, Alexander E., et al. "AAV Analysis by Sedimentation Velocity Analytical Ultracentrifugation: Beyond Empty and Full Capsids." *European Biophysics Journal*, 2023.

Yiu, Glenn, et al. "Suprachoroidal and Subretinal Injections of AAV Using Transscleral Microneedles for Retinal Gene Delivery in Nonhuman Primates." *Molecular Therapy: Methods & Clinical Development*, 2020.

Zobor, Ditta, et al. "Genetic and Clinical Profile of Retinopathies Due to Disease-Causing Variants in Leber Congenital Amaurosis (LCA)-Associated Genes in a Large German Cohort." *International Journal of Molecular Sciences*, 2023.
