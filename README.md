# pfas-biosphere-model
Open-source computational framework and mathematical architecture for modeling PFAS-driven cross-trophic biosphere collapse.

This repository contains the conceptual framework and mathematical architecture for a non-steady-state multimedia fate, transport, and multi-species bioamplification model. The core objective of this project is to simulate the long-term ecotoxicological tipping points driven by the continuous transgression of the "novel entities" planetary boundary by Per- and Polyfluoroalkyl Substances (PFAS).

---

## 🔗 References & Scientific Background

This repository serves as the official computational implementation bridge for the theoretical pre-print:

*   **Direct Repository Access:** [View Paper on Zenodo](https://zenodo.org/records/20376702)
*   **Persistent DOI:** [10.5281/zenodo.20376702](https://doi.org/10.5281/zenodo.20376702)

### Citation

If you use this conceptual framework, mathematical architecture, or future code simulations in your research, please cite the pre-print as follows:

```bibtex
@misc{pfas_tipping_points_2026,
  author       = {Sergei Pushkin},
  title        = {Global Transgression of the Novel Entities Planetary Boundary by PFAS: A Dynamic Multimedia Modeling of Irreversible Biosphere Collapse and Cross-Trophic Ecological Regression},
  month        = may,
  year         = 2026,
  publisher    = {Zenodo},
  doi          = {10.5281/zenodo.20376702},
  url          = {https://zenodo.org/records/20376702}
}

---

## 🧠 System Architecture & Compartments

To translate the abstract mass-balance equations into a functional computational script (e.g., Python via SciPy/NumPy), the global biosphere is discretized into **five interconnected dynamic compartments (_i_)**:

1.  **Compartment 1: Atmosphere ($i=1$)** – Governs long-range atmospheric transport (LRAT), advection-dispersion parameters, and temperature-dependent volatilization via the van 't Hoff equation.
2.  **Compartment 2: Surface Ocean ($i=2$)** – Focuses on the photic zone, global conveyor currents, marine microlayer enrichment, and sea spray aerosol (SSA) interfacial mass transfer kinetics.
3.  **Compartment 3: Deep Ocean ($i=3$)** – Represents the permanent terminal sink ($F_{sink}$) driven by deep-sea sedimentation and particulate organic carbon (POC) scavenging.
4.  **Compartment 4: Soil & Terrestrial Matrix ($i=4$)** – Models runoff kinetics, organic carbon partitioning (`K_oc`), and groundwater infiltration pathways.
5.  **Compartment 5: Cryosphere ($i=5$)** – Simulates polar ice and glacier accumulation acting as a historical reservoir, capturing the "Arctic Trap" flushing events driven by planetary warming.

---
## 🎛️ Comprehensive System Parameters & Forcing Factors (Version 6.0)

To achieve a holistic representation of the Earth System, the simulator maps the dynamic interactions across four fundamental axes of the modern Anthropocene:

### 1. Chemical & Abiotic Dynamics (Core Fate & Transport)
*   **P_global(t):** Dynamic global and regional annual production/consumption volumes of PFAS (Time Series input).
*   **\epsilon_i,z:** Compartment-specific anthropogenic emission loss factors (fractional leakage during manufacturing, use, and disposal).
*   **M_i,z / C_i,z:** Transient mass [kg] and derived concentration [$kg/m^3$] fields across 5 environments linked via compartment volumes ($V_i$).
*   **k_deg,i:** Pseudo-first-order environmental precursor transformation and chemical degradation kinetics.
*   **K_ia / K_aw / K_oc:** Physicochemical partition coefficients (air-water interfacial, Henry's law, and organic carbon matrices).
*   **F_sink,i:** Permanent terminal sink velocity parameterization (e.g., deep-sea particulate sedimentation and POC scavenging).

### 2. Spatio-Temporal & Geophysical Transport Channels
*   **Geospatial Latitudinal Zoning (z):** Spatial discretization into distinct Tropical, Temperate, and Polar macro-regions.
*   **Flux_advection,z:** Directional mass transport driven by global atmospheric cell circulation and oceanic conveyor currents.
*   **Q_river,z:** Dynamic seasonal volumetric river discharge exporting concentrated industrial chemical burdens through coastal deltas.
*   **Sinusoidal Meteorological Forcing:** Time-dependent sinusoidal loops mapping seasonal precipitation, ambient temperature variations, and planetary ice-melting rates.
*   **The "Spring Flush" Effect:** Pulse-multipliers resolving rapid, non-linear spring contaminant flushes from winter snowpacks.
*   **J_biotech,z:** Biotic vector translocation matrices mapping mass transport via migratory fauna (anadromous fish, whales, waterfowl) across boundaries.

### 3. Eco-Toxicological & Trophic Resilience Feedbacks
*   **P_primary(C_water):** Net primary marine carbon fixation and phytoplankton productivity response function.
*   **EC_50,plankton:** Critical median effective concentration driving non-linear inhibition of micro-algal photosynthesis.
*   **D:** An $N \times N$ column-stochastic dietary preference matrix mapping realistic multi-species food web adjacency networks.
*   **C_tissue,n:** Species-specific steady-state tissue concentration vectors derived directly through matrix inversion.
*   **\alpha(C_tissue,n):** Non-linear Hill-regulatory population fecundity response function tracking top-down multi-species demographic collapse.
*   **EC_50,n:** Species-specific critical thresholds for endocrine disruption, systemic metabolic strain, and reproductive failure.
*   **Cascading Trophic Resonance:** Structural node-deletion trigger executing automated prey-to-predator dietary weight redistribution when single-species biomass falls below a critical threshold ($M_{min}$).

### 4. Technosphere, Multi-Sector Energy, & Geopolitical Shocks
*   **d[O_3]/dt & UV-B Forcing:** Stratospheric ozone depletion rates and subsequent ultraviolet surface irradiance surges driven by high-frequency heavy aerospace launch regimes ( SpaceX Starship / Chinese Long March fleets > 1 launch/hour).
*   **S_nuclear:** Stochastic radionuclide contamination risk multipliers tracking spent nuclear fuel (SNF) storage vulnerability under climate-driven extreme weather.
*   **S_heavy_metals:** Cumulative body burdens of mercury, lead, and acid-precipitation compounds originating from Thermal Power Plants (TPPs).
*   **Hydro-Fragmentation:** Geopolitical and infrastructural fragmentation constants altering regional river networks and trapping toxins.
*   **Albedo Alteration (Dry-Land & Marine):** Regional surface albedo degradation driven by macro-scale photovoltaic solar fields, onshore/offshore wind clusters, and dark-water microbial/invasive algal blooms.
*   **E_pathogen(t):** Exponential global pathogen pressure function tracking PFAS-induced mass immunosuppression-driven pan-zootics, epizootics, and epiphytoties.
*   **Geopolitical Conflict Forcing (S_conflict):** Kinetic conflict impulse functions accelerating chemical emission leakages ($\epsilon$) via unregulated military surfactant usage (AFFF), infrastructure sabotage, and the complete collapse of international environmental treaty compliance.

## 📐 Key Mathematical Modules for Coders

### 1. Multimedia Mass Balance (Ordinary Differential Equations)
The dynamic mass shifts across all five environments must be resolved simultaneously using an explicit 4th/5th order Runge-Kutta integration method (`scipy.integrate.solve_ivp` with `method='RK45'`). The anthropogenic input is dynamically driven by the global annual production volume of PFAS ($P_{global}(t)$) multiplied by a compartment-specific emission loss factor ($\epsilon_i$). Note that concentration is derived as $C_i = M_i / V_i$, where $V_i$ is the compartment volume:

$$\frac{dM_i}{dt} = \left( P_{global}(t) \cdot \epsilon_i \right) + \sum_{j \neq i} (F_{ji} \cdot C_j) - \sum_{j \neq i} (F_{ij} \cdot C_i) - k_{deg,i} \cdot M_i - F_{sink,i}$$

where $P_{global}(t)$ is the dynamic global annual production volume of PFAS, and $\epsilon_i$ is the compartment-specific anthropogenic emission loss factor.
where $M_i$ is the mass of the PFAS species in compartment $i$ [kg], ($I_i$ represents the anthropogenic emissions input [kg/year]), $F_{ij}$ and $F_{ji}$ denote the volumetric bulk inter-compartment transfer flows [m3/year], $k_{deg,i}$ is the pseudo-first-order transformation rate [1/year], and $F_{sink,i}$ represents the permanent loss to terminal sinks (e.g., deep-sea sedimentation) [kg/year]. Crucially, the dynamic concentration forcing parameter $C_i$ [kg/m3] is coupled to the state variable via compartment volume ($V_i$):

$$C_i = \frac{M_i}{V_i}$$

### 2. Interfacial Sea Spray Aerosol (SSA) Flux & Thermal Cryospheric Outflux
The feedback mechanism from ocean to atmosphere is parameterized as a mass flux generated by wind-driven wave breaking, coupled with a temperature-dependent exponential polar flushing function $F_{cryo \rightarrow ocean}(\Delta T)$:

$$J_{SSA} = E_{SSA}(U_{10}) \cdot F_{enrich} \cdot C_{water}$$

where $E_{SSA}$ is the sea spray aerosol emission volume rate driven by the 10-meter baseline wind speed ($U_{10}$), and $F_{enrich}$ is the chemical-specific surface enrichment factor governed by surfactant air-water interfacial partitioning ($K_{ia}$). The global distillation effect is modeled by making the air-water partition coefficient temperature-dependent via the van 't Hoff equation, driving continuous accumulation toward polar zones.

To close the macro-environmental feedback loop between the chemical biosphere and climate change, the cryospheric terminal sink behavior is shifted from a static loss parameter to a dynamic temperature-dependent secondary emission flux. The outflux of accumulated PFAS from the polar cryosphere back into the surface ocean compartment ($F_{cryo \rightarrow ocean}$, [m3/year]) is modeled as an exponential function of global forcing temperature anomalies:

$$F_{cryo \rightarrow ocean}(\Delta T) = F_{base} \cdot \exp\left( \theta \cdot \frac{\Delta T}{T_{ref}} \right)$$

where $F_{base}$ represents the baseline background flushing rate under pre-industrial climatic conditions [m3/year], $\Delta T$ is the dynamic global temperature anomaly over time [°C], $T_{ref}$ is the critical international climate policy reference threshold (e.g., 1.5°C), and $\theta$ is a dimensionless cryospheric thermal sensitivity coefficient. Under accelerating warming scenarios, this formulation simulates the abrupt thermodynamic breakdown of the "Arctic Trap," transforming historical ice reservoirs into major secondary emission sources.

### 3. Bottom-Up Phytoplankton Photosynthetic Inhibition
Rather than treating primary marine productivity as a static boundary condition, the ocean's net primary carbon fixation rate ($P_{primary}$) is coupled non-linearly to the transient PFAS concentration in surface waters:

$$P_{primary}(C_{water}) = P_0 \cdot \left(1 - \frac{C_{water}^{\gamma}}{EC_{50, plankton}^{\gamma} + C_{water}^{\gamma}}\right)$$

where $P_0$ is the pristine, undisturbed global primary productivity [kg C/year], $EC_{50, plankton}$ is the median effective concentration driving a 50% inhibition of phytoplankton photosynthetic electron transport and carbon assimilation [kg/m3], and $\gamma$ is the Hill cooperativity coefficient for the micro-algal matrix. As $C_{water}$ approaches the $EC_{50, plankton}$ threshold, the systemic energy supply fueling the upper food web collapses non-linearly, rendering higher trophic tiers highly vulnerable to energetic starvation.

### 4. Multi-Species Trophic Bioamplification Matrix
To simulate realistic bioamplification across branched ecological networks, the steady-state tissue concentration vector $C_{tissue}$ is resolved simultaneously using an adjacency-weighted, column-stochastic dietary preference matrix $D$:

$$\mathbf{C_{tissue}} = \left( \mathbf{K_2} + \mathbf{K_{repro}} - \mathbf{D} \odot \mathbf{K_1} \right)^{-1} \times \left( \mathbf{k_{env}} \odot \mathbf{C_{env}} \right)$$

### 5. Non-Linear Fecundity Tipping Point (The Hill Function)
To simulate dynamic demographic collapse, the reproduction rate of each individual species ($\alpha_n$) responds non-linearly to its specific tissue concentration component derived from the matrix solver:

$$\alpha(C_{tissue,n}) = \alpha_0 \cdot \left(1 - \frac{C_{tissue,n}^\eta}{EC_{50,n}^\eta + C_{tissue,n}^\eta}\right)$$

### 6. Coupled Climate-Carbon-Acidification Feedbacks
When net primary productivity ($P_{primary}$) drops, the biological carbon pump fails, driving accelerated global warming trajectories ($d(\Delta T)/dt$) and intense ocean acidification ($dpH/dt$):

$$\frac{d(\Delta T)}{dt} = R_{forcing} \cdot \left( 1 + \psi \cdot \left[ 1 - \frac{P_{primary}(C_{water})}{P_0} \right] \right) - \lambda \cdot \Delta T$$

$$\frac{dpH}{dt} = -\xi \cdot \left[ 1 - \frac{P_{primary}(C_{water})}{P_0} \right] \cdot C_{atm, CO2}$$

### 7. Dynamic Multi-Stressor Toxicity Synergy
The critical toxicity thresholds ($EC_{50,n}$) respond dynamically and non-linearly to ocean acidification ($pH$) and a vector of co-occurring global anthropogenic stressors $\mathbf{S}$ (microplastics, heavy metals, surfactants, pathogens):

$$EC_{50,n}(pH, \mathbf{S}) = EC_{50,n}^{baseline} \cdot \exp\left( -\delta_n \cdot (pH_{baseline} - pH) \right) \cdot \prod_{k} (1 - S_k)$$

---

## 🛠️ Call for Code: How to Contribute

This is an **unfunded, independent open-source initiative**. We invite data scientists, Python developers, system dynamicists, and computational ecologists to leverage this framework and translate these equations into ready-to-use Python (SciPy/NumPy) simulations. 

Our goal is to empower the community to model these critical ecotoxicological tipping points and bring this conceptual architecture into practical, actionable research.

### Development Priorities:
*   [ ] Write the core ODE system (`core_solver.py`) mapping the 5 compartments and coupling mass to concentration ($C_i = M_i / V_i$).
*   [ ] Implement parameter matrices for short-chain alternatives (GenX, ADONA) utilizing available $K_{ia}$ interfacial data, accounting for empirical gaps.
*   [ ] Integrate climate-driven thermal forcing ($\Delta T$) to model exponential cryosphere flushing outflux and planetary albedo feedback.
*   [ ] Design the multi-species trophic network matrix solver (`matrix_solver.py`) using column-stochastic dietary preference weights ($D_{nm}$).
*   [ ] Code the coupled multi-boundary solver integrating dynamic ocean acidification ($dpH/dt$) and carbon feedback loops ($d(\Delta T)/dt$).
*   [ ] Implement dynamic $EC_{50,n}(pH, \mathbf{S})$ response functions mapping synergistic cocktail effects (microplastics, heavy metals, surfactants, pathogens).
*   [ ] Develop the geospatial multi-scale core (`spatial_core.py`) to resolve advective transport across latitudinal zones and localized urban hotspots.
*   [ ] Code seasonal sinusoidal forcing loops (Spring Flush) and biotic vector transport matrices ($J_{biotech,z}$) for migratory bioindicators.
*   [ ] Integrate an upper-atmosphere aerospace forcing module to simulate ozone depletion ($d[O_3]/dt$) and ultraviolet stress from high-frequency rocket launches.
*   [ ] Implement a multi-sector energy infrastructure matrix mapping regional albedo shifts (solar/wind fields) and stochastic radionuclide stress ($S_{nuclear}$).
*   [ ] Code the endogenous geopolitical conflict loop to dynamically accelerate emission loss factors ($\epsilon_{i,z}$) during resource scarcity and military shocks.
*   [ ] Build a visualization dashboard (Matplotlib/Dash) to plot global trophic downgrading trajectories against cascading food web node collapses.

If you are a student, researcher, or developer who understands the gravity of planetary boundaries degradation, feel free to fork this repository, submit pull requests, or use this structure for your own peer-reviewed publications.

**The relay baton is passed.**

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
