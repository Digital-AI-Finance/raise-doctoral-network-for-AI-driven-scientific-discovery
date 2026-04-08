# ATLAS-FIN v2: Full Proposal Concept

**AI Technologies for Leveraging Advanced Science in Finance**
MSCA RAISE Doctoral Networks | HORIZON-RAISE-2026-01-03
Submission deadline: 24 November 2026

---

# 1. EXECUTIVE SUMMARY

**ATLAS-FIN** (AI Technologies for Leveraging Advanced Science in Finance) is a RAISE Doctoral Network that trains 12 doctoral candidates to answer a single, testable scientific question:

> *Can purpose-built neural architectures that embed financial theory as structural inductive biases outperform both traditional financial models AND generic machine learning, establishing a new paradigm of theory-aware AI for financial science?*

This question is not rhetorical. Financial economics possesses a rich body of structural theory -- no-arbitrage conditions, equilibrium constraints, stylized distributional facts, network contagion dynamics -- yet the current wave of ML in finance treats these as post-hoc evaluation checks rather than architectural priors. ATLAS-FIN hypothesizes that encoding such domain knowledge directly into neural architecture design (loss functions, layer structure, latent spaces, aggregation operators) yields models that are simultaneously more accurate, more data-efficient, more interpretable, and more robust than either classical parametric models or theory-agnostic deep learning.

The network comprises **12 Doctoral Candidates (DCs)** organized in **3 clusters**: (1) Causal and Structural AI for Financial Markets, (2) Network and System-Level AI for Financial Stability, and (3) AI for Sustainable Finance and Regulatory Compliance. Each DC develops a novel AI architecture whose design is structurally informed by financial theory. The consortium unites **8 academic beneficiaries** (ZHAW, Imperial College London, TU Munich, ETH Zurich, Bocconi University, TU Delft, WU Vienna, University of Helsinki) and **4 non-academic associated partners** (Bloomberg LP, Swiss Re, M42 Abu Dhabi, BIS Innovation Hub Basel).

**Budget:** 12 DCs x 36 months = 432 person-months. Estimated EU contribution approximately EUR 3.6M (using corrected 2026 unit costs: EUR 4,250 living allowance, EUR 1,600 RTN, EUR 1,200 management per researcher-month).

**Duration:** 48 months.

**RAISE relevance:** Every DC develops a novel AI architecture whose scientific contribution is directly dependent on the integration of financial-domain structural priors into the AI system. AI is integral and indispensable, not instrumental. All DCs receive dedicated AI-in-science doctoral training and join the RAISE community.

---

# 2. EXCELLENCE

## 2.1 Research Objectives

### Unifying Thesis

Financial theory provides testable structural constraints (no-arbitrage, equilibrium, fat tails, contagion topology, climate-economy coupling). Generic ML ignores these. ATLAS-FIN's thesis is that encoding these constraints as architectural inductive biases -- not merely as regularization terms or evaluation metrics -- creates a fundamentally superior class of financial AI models. This is a falsifiable claim: if theory-aware architectures do not systematically outperform both classical models and generic ML on held-out data and stress scenarios, the thesis fails.

### Three Overarching Research Objectives

**RO1: Develop AI architectures with financial-theory inductive biases.** Each DC produces at least one novel neural architecture whose layer design, loss function, latent space structure, or message-passing scheme is formally derived from a specific financial-theoretic constraint. This is the methodological core.

**RO2: Demonstrate systematic outperformance over both classical and generic-ML baselines.** Every DC conducts controlled experiments comparing its theory-aware architecture against (a) the best classical model for its problem domain and (b) the best available generic deep learning baseline, using standardized evaluation protocols defined in WP1-WP3.

**RO3: Establish reproducible benchmarks for theory-aware financial AI.** The network produces open benchmark datasets (real where permissible, synthetic from DC2 otherwise), standardized evaluation metrics, and reproducible experimental pipelines (Docker containers, pre-registered analysis plans) that allow the broader community to test the unifying thesis beyond the 12 DCs.

### Network > Sum of Parts

The DCs are not 12 independent projects. They share: (a) a common evaluation framework (RO2-RO3) that makes cross-DC comparison meaningful, (b) synthetic data infrastructure from DC2 used by DCs 1, 3, 5, 6, and 8, (c) the causal discovery methods of DC7 feeding into DC1, DC5, and DC10, and (d) the regulatory compliance framework of DC11 applied retrospectively to all 12 architectures. Cross-cluster dependencies are enforced through co-authored deliverables and joint secondments.

## 2.2 The 12 DC Projects

### Cluster 1: Causal and Structural AI for Financial Markets (DC1-DC4)

**DC1: Causal-Temporal Transformer with Structural Equation Model Priors for Market Dynamics**

- **Host:** ZHAW School of Engineering, Winterthur, Switzerland
- **Supervisors:** Prof. Joerg Osterrieder (ZHAW, main), Prof. Markus Leippold (University of Zurich, co-supervisor), Dr. Sarah Chen (Bloomberg LP, industry mentor)
- **Objectives:** (O1) Design a transformer variant whose attention mechanism is constrained by a learned structural equation model (SEM) over financial variables, so that attention weights reflect causal pathways rather than arbitrary correlations. (O2) Demonstrate that SEM-constrained attention reduces spurious cross-asset signal propagation by at least 30% on out-of-sample causal inference benchmarks. (O3) Release a benchmark dataset of synthetic causal financial time series (jointly with DC2).
- **Methodology:** Standard transformers compute attention over all token pairs without structural constraint. DC1 introduces a causal masking layer derived from a differentiable SEM. The SEM graph is learned jointly with the transformer parameters via a bilevel optimization: the inner loop trains transformer weights given a fixed causal graph; the outer loop updates the graph using a penalized likelihood (NOTEARS-style acyclicity constraint adapted for temporal data). The attention matrix is element-wise multiplied by the SEM adjacency matrix, forcing the model to attend only along estimated causal paths. This is not post-hoc masking -- the graph and the attention co-evolve during training.
- **AI integral:** The architectural innovation IS the research contribution. Without the SEM-constrained attention mechanism, this reduces to a standard financial time series forecast.
- **Outputs:** 2 publications (NeurIPS/ICML + Journal of Financial Economics), open-source PyTorch library, benchmark dataset.
- **Secondments:** Bloomberg LP London (4 months, M13-16, real-time market data pipeline integration), Imperial College (2 months, M24-25, joint work with DC3 on multi-scale temporal fusion).

**DC2: Constrained Diffusion Models for Synthetic Financial Data with Stylized-Fact Guarantees**

- **Host:** ZHAW School of Engineering, Winterthur, Switzerland
- **Supervisors:** Prof. Joerg Osterrieder (ZHAW, main), Prof. Patrick Cheridito (ETH Zurich, co-supervisor), Dr. Marco Frey (Swiss Re, industry mentor)
- **Objectives:** (O1) Develop a score-based diffusion model whose denoising score function is augmented with penalty terms that enforce 11 canonical stylized facts of financial returns (fat tails, volatility clustering, leverage effect, gain-loss asymmetry, etc.). (O2) Prove that constrained diffusion samples satisfy all 11 stylized facts with statistical confidence > 95% (Kolmogorov-Smirnov, autocorrelation tests), while unconstrained baselines satisfy at most 6-7. (O3) Provide the network's internal synthetic data infrastructure.
- **Methodology:** Starting from a variance-preserving SDE diffusion framework, the reverse-time score function s(x,t) is trained with a composite loss: L = L_denoising + lambda * L_stylized. L_stylized is a differentiable sum of soft constraint violations: (i) a Hill estimator penalty encouraging tail index alpha in [3,5], (ii) an autocorrelation penalty on |r_t| enforcing slow decay, (iii) a leverage correlation penalty enforcing negative correlation between returns and future volatility, plus 8 additional terms. The lambda schedule increases during training (curriculum-style), forcing the model to first learn overall distribution shape, then progressively satisfy finer stylized facts. A rejection-sampling post-processing step provides hard guarantees for deployment.
- **AI integral:** The constrained score function is a novel AI contribution. Financial theory (stylized facts) directly shapes the neural network's loss landscape.
- **Outputs:** 2 publications (AISTATS + Quantitative Finance), open-source SynthFinDiffusion library, synthetic datasets for DCs 1, 3, 5, 6, 8.
- **Secondments:** Swiss Re Zurich (4 months, M10-13, insurance loss distribution modeling), ETH Zurich (2 months, M22-23, theoretical convergence analysis with Prof. Cheridito).

**DC3: Asynchronous Multi-Scale Temporal Fusion Architecture for Financial Modalities**

- **Host:** Imperial College London, Department of Computing, United Kingdom
- **Supervisors:** Prof. Bjorn Schuller (Imperial, main), Prof. Joerg Osterrieder (ZHAW, co-supervisor), Dr. Nikos Passalis (Bloomberg LP, industry mentor)
- **Objectives:** (O1) Design a temporal fusion architecture that processes financial modalities (tick data, order book snapshots, news text, options surfaces) arriving at fundamentally different frequencies (microseconds to days) without artificial synchronization. (O2) Introduce a learned temporal alignment layer that discovers cross-modal lead-lag relationships. (O3) Demonstrate at least 15% improvement over synchronous baselines on multi-modal financial prediction tasks.
- **Methodology:** Existing multi-modal transformers synchronize inputs to a common time grid, destroying the asynchronous information structure of financial markets. DC3 introduces an Asynchronous Temporal Fusion (ATF) architecture with three innovations: (i) modality-specific encoders operating at native frequencies with learnable positional encodings reflecting wall-clock time rather than token position, (ii) a cross-modal temporal attention module where query timestamps from one modality attend to key-value pairs from another modality using a learned temporal kernel (Gaussian process-inspired) that captures lead-lag structure, and (iii) a hierarchical aggregation module that fuses information at multiple time horizons (intraday, daily, weekly) using gated residual connections. The temporal kernel parameters are interpretable as lead-lag estimates.
- **AI integral:** The asynchronous temporal fusion mechanism is the architectural contribution. Financial market microstructure theory (asynchronous information arrival, Hasbrouck 1995) motivates the design.
- **Outputs:** 2 publications (AAAI + Journal of Financial and Quantitative Analysis), open-source ATF library, multi-modal financial benchmark.
- **Secondments:** Bloomberg LP London (4 months, M14-17, access to Bloomberg Terminal real-time feeds), ZHAW (2 months, M26-27, integration with DC1 causal framework).

**DC4: Physics-Informed Neural Networks with No-Arbitrage PDE Constraints for Derivatives Pricing**

- **Host:** TU Munich, Department of Mathematics, Germany
- **Supervisors:** Prof. Griselda Deelstra (TU Munich, main), Prof. Christa Cuchiero (University of Vienna, co-supervisor), Dr. Andreas Steiner (Swiss Re, industry mentor)
- **Objectives:** (O1) Build a PINN that solves the Black-Scholes-Merton PDE and its extensions (Heston, rough volatility) by encoding the no-arbitrage condition directly in the network's loss function and boundary conditions. (O2) Demonstrate that PINN-derived prices satisfy no-arbitrage constraints exactly (zero butterfly spread arbitrage, monotonicity in strike) while finite-difference solvers exhibit numerical arbitrage at extreme parameters. (O3) Extend to path-dependent options where no closed-form PDE exists.
- **Methodology:** The PINN takes (S, t, K, sigma, r) as input and outputs the option price C. The loss has three components: (i) PDE residual loss enforcing that the network output satisfies the Black-Scholes PDE at collocation points, (ii) boundary/terminal condition losses (C(S,T) = max(S-K,0) for calls), and (iii) no-arbitrage constraint losses (dC/dK <= 0, d2C/dK2 >= 0, calendar spread non-negativity). For Heston and rough volatility extensions, the PDE becomes a system (2D or fractional), and the PINN architecture is extended with separate sub-networks for price and variance surfaces sharing a common latent representation. The rough volatility case uses a fractional derivative approximation via Grunwald-Letnikov discretization embedded in the loss.
- **AI integral:** The PINN architecture with embedded no-arbitrage PDE constraints is the contribution. Financial derivative pricing theory (Harrison-Kreps 1979, Heston 1993) provides the structural constraints.
- **Outputs:** 2 publications (Journal of Computational Finance + Mathematical Finance), ArbitrageFreePINN software library.
- **Secondments:** Swiss Re Zurich (3 months, M15-17, exotic derivatives pricing in practice), ETH Zurich (3 months, M24-26, collaboration with DC8 on stress testing derivatives portfolios).

### Cluster 2: Network and System-Level AI for Financial Stability (DC5-DC8)

**DC5: Temporal Hypergraph Neural Networks for Multi-Lateral Systemic Risk**

- **Host:** TU Munich, Department of Informatics, Germany
- **Supervisors:** Prof. Stephan Gunnemann (TU Munich, main), Prof. Joerg Osterrieder (ZHAW, co-supervisor), Dr. Patrick Amberg (BIS Innovation Hub, industry mentor)
- **Objectives:** (O1) Develop a temporal hypergraph neural network (THGNN) that models multi-lateral financial exposures (not just bilateral) using hyperedges representing multi-party contracts (CCPs, syndicated loans, derivatives netting sets). (O2) Show that THGNN captures contagion cascades missed by standard GNNs limited to pairwise edges. (O3) Provide early-warning indicators for systemic stress with 6-month lead time.
- **Methodology:** Standard GNNs for financial networks use pairwise edges, but systemic risk propagates through multi-lateral structures (a CCP connects dozens of counterparties simultaneously). DC5 introduces a THGNN where: (i) hyperedges represent multi-party financial contracts with a learned hyperedge feature vector encoding contract type and exposure, (ii) message passing aggregates information from all nodes in a hyperedge using a permutation-invariant function (DeepSets-style) weighted by exposure share, (iii) temporal evolution is captured by a recurrent update of hyperedge and node embeddings at each time step, with a Hawkes-process-inspired temporal attention that upweights recent stress events. The loss includes a graph-level systemic risk classification objective plus a node-level default probability regression.
- **AI integral:** The hypergraph message-passing scheme with financial-exposure weighting is the novel AI contribution. Financial network theory (Eisenberg-Noe 2001, clearing mechanisms) provides the structural prior.
- **Outputs:** 2 publications (KDD + Journal of Financial Stability), open-source THGNN library, synthetic interbank network dataset (from DC2).
- **Secondments:** BIS Innovation Hub Basel (4 months, M12-15, access to BIS banking statistics and policy context), Bocconi (2 months, M24-25, integration with DC6 market microstructure).

**DC6: Multi-Agent Reinforcement Learning with Heterogeneous Agents for Market Microstructure**

- **Host:** Bocconi University, Department of Finance, Milan, Italy
- **Supervisors:** Prof. Claudio Tebaldi (Bocconi, main), Prof. Bjorn Schuller (Imperial, co-supervisor), Dr. Sarah Chen (Bloomberg LP, industry mentor)
- **Objectives:** (O1) Design a multi-agent RL environment where agents have architecturally distinct policy networks reflecting their financial role (market maker, institutional investor, HFT, retail), with role-specific action spaces and reward functions derived from microstructure theory. (O2) Show that heterogeneous-agent equilibria reproduce empirical market microstructure patterns (bid-ask spread dynamics, price impact curves, flash crash susceptibility) better than homogeneous-agent baselines. (O3) Use the simulator as a regulatory sandbox for policy experiments (transaction tax, circuit breakers).
- **Methodology:** Unlike standard MARL where agents share architecture, DC6 assigns each agent type a structurally different policy network: market makers use an inventory-penalized network (Avellaneda-Stoikov reward), institutional investors use an execution-cost-minimizing network (Almgren-Chriss framework as shaped reward), HFT agents use a latency-sensitive network with a temporal discount reflecting speed advantage. The environment simulates a limit order book with realistic tick structure. Training uses independent PPO with a centralized critic that observes aggregate order flow statistics. The key innovation is that financial theory prescribes the agent heterogeneity -- this is not learned but architecturally imposed.
- **AI integral:** The heterogeneous-agent MARL architecture with theory-prescribed role differentiation is the AI contribution. Market microstructure theory (Kyle 1985, Glosten-Milgrom 1985) defines the agent structure.
- **Outputs:** 2 publications (AAMAS + Review of Financial Studies), open-source MicrostructureMARL simulator.
- **Secondments:** Bloomberg LP New York (4 months, M16-19, calibration against real order book data), ZHAW (2 months, M28-29, integration with DC2 synthetic data for agent training).

**DC7: Causal Discovery Algorithms for Non-Stationary Macro-Financial Systems**

- **Host:** Imperial College London, Department of Mathematics, United Kingdom
- **Supervisors:** Prof. Nikolas Kantas (Imperial, main), Prof. Griselda Deelstra (TU Munich, co-supervisor), Dr. Patrick Amberg (BIS Innovation Hub, industry mentor)
- **Objectives:** (O1) Develop a causal discovery algorithm that identifies time-varying causal graphs in macro-financial systems where both the graph structure and the functional relationships change across regimes (expansion, crisis, recovery). (O2) Introduce a regime-switching mechanism that allows the causal graph to change at learned changepoints, with a sparsity prior favoring parsimonious graph transitions. (O3) Validate on ECB macro-financial data with known structural breaks (2008 GFC, 2020 COVID, 2022 rate hiking cycle).
- **Methodology:** Existing causal discovery (PC, FCI, NOTEARS) assumes a stationary graph. DC7 extends NOTEARS to a regime-switching setting: the system maintains K candidate DAGs {G_1,...,G_k}, each parameterized as a continuous adjacency matrix with acyclicity constraint. A hidden Markov model governs transitions between graphs, with transition probabilities learned jointly. The loss is: L = sum_t [ -log p(x_t | G_{z_t}) + lambda * h(G_{z_t}) + mu * ||G_{z_t}||_1 ] + kappa * transitions_penalty, where h() is the NOTEARS acyclicity function, z_t is the latent regime, and transitions_penalty discourages excessive regime switching. Inference uses an EM algorithm: E-step estimates regime assignments via forward-backward, M-step updates each graph using augmented Lagrangian optimization.
- **AI integral:** The regime-switching causal discovery algorithm with financial non-stationarity as architectural motivation is the AI contribution. Macro-financial theory (regime-dependent transmission, Hamilton 1989) provides the structural prior.
- **Outputs:** 2 publications (UAI + Journal of Econometrics), open-source RegimeCausal library, feeds into DC1 (causal graphs), DC5 (network structure), DC10 (causal ESG attribution).
- **Secondments:** BIS Innovation Hub Basel (4 months, M13-16, macro-prudential policy data and context), TU Munich (2 months, M25-26, integration with DC5 hypergraph dynamics).

**DC8: Adversarial Generative Stress Testing with Financial Plausibility Constraints**

- **Host:** ETH Zurich, Department of Mathematics, Switzerland
- **Supervisors:** Prof. Josef Teichmann (ETH Zurich, main), Prof. Joerg Osterrieder (ZHAW, co-supervisor), Dr. Marco Frey (Swiss Re, industry mentor)
- **Objectives:** (O1) Build a conditional GAN for stress scenario generation where the generator is constrained to produce scenarios that are financially plausible (satisfy no-arbitrage, respect macro-financial accounting identities, preserve cross-asset correlation structure under stress). (O2) Show that constrained adversarial scenarios expose portfolio vulnerabilities missed by historical and parametric (Basel) stress tests. (O3) Provide stress testing tools deployable at central banks and insurers.
- **Methodology:** The generator G takes a latent vector z and a stress severity parameter s as input and produces a multi-asset scenario (returns, volatilities, spreads, macro variables). The discriminator D distinguishes real from generated scenarios. The innovation is a set of differentiable constraint layers appended to G: (i) an arbitrage-free projection layer that adjusts generated derivatives prices to satisfy put-call parity and butterfly constraints, (ii) a macro-accounting identity layer ensuring GDP = C + I + G + NX in generated macro scenarios, (iii) a correlation structure layer using a Cholesky parameterization that preserves positive-definiteness under stress amplification. The training loss is: L_G = -E[D(G(z,s))] + alpha * L_constraints. The stress severity parameter s allows interpolation from normal to extreme scenarios.
- **AI integral:** The constrained GAN architecture with financial plausibility layers is the AI contribution. Stress testing theory and no-arbitrage conditions provide the structural constraints.
- **Outputs:** 2 publications (ICLR + Journal of Banking and Finance), StressGAN toolkit, feeds into DC4 (derivatives stress testing) and DC5 (systemic risk scenarios).
- **Secondments:** Swiss Re Zurich (4 months, M14-17, insurance stress testing calibration), BIS Innovation Hub (2 months, M26-27, central bank stress testing framework alignment).

### Cluster 3: AI for Sustainable Finance and Regulatory Compliance (DC9-DC12)

**DC9: Neural Climate-to-Finance Bridge with Integrated Assessment Model Physics Constraints**

- **Host:** TU Delft, Faculty of Technology, Policy and Management, Netherlands
- **Supervisors:** Prof. Servaas Storm (TU Delft, main), Prof. Joerg Osterrieder (ZHAW, co-supervisor), Dr. Marco Frey (Swiss Re, industry mentor)
- **Objectives:** (O1) Build a neural network that maps climate scenarios (temperature pathways, carbon budgets, physical risk realizations) to financial asset valuations, with the mapping constrained by the physics of integrated assessment models (DICE/REMIND carbon cycle, damage functions). (O2) Show that physics-constrained neural climate-finance models produce transition risk estimates that are more internally consistent and less sensitive to arbitrary assumptions than current NGFS scenario tools. (O3) Provide a tool for climate stress testing of financial portfolios.
- **Methodology:** The architecture is a neural ODE whose dynamics are partially prescribed by IAM physics. The state vector includes both climate variables (temperature anomaly, carbon concentration, radiative forcing) and financial variables (sector-level equity valuations, credit spreads, sovereign yields). The ODE right-hand side is: dx/dt = f_physics(x_climate) + f_neural(x_climate, x_financial), where f_physics is the DICE carbon cycle and energy balance equations (hard-coded, not learned), and f_neural is a neural network that captures the climate-to-finance transmission channel. The loss is: L = L_prediction(asset prices) + beta * L_physics(carbon cycle residual) + gamma * L_damage(damage function consistency). This ensures the model respects physical constraints while learning the financial transmission mechanism from data.
- **AI integral:** The physics-constrained neural ODE for climate-finance coupling is the AI contribution. Climate physics (Nordhaus DICE) and financial asset pricing theory provide the structural priors.
- **Outputs:** 2 publications (Nature Climate Change + Journal of Financial Economics), ClimateFinanceODE toolkit.
- **Secondments:** Swiss Re Zurich (4 months, M12-15, climate risk modeling in insurance), M42 Abu Dhabi (2 months, M24-25, computational infrastructure for large-scale climate scenarios).

**DC10: Causal AI for ESG Impact Attribution Using Double-ML and Instrumental Variables**

- **Host:** Bocconi University, Department of Economics, Milan, Italy
- **Supervisors:** Prof. Massimo Guidolin (Bocconi, main), Prof. Servaas Storm (TU Delft, co-supervisor), Dr. Patrick Amberg (BIS Innovation Hub, industry mentor)
- **Objectives:** (O1) Develop a neural network architecture for ESG impact attribution that embeds double-machine-learning (DML) and instrumental variable (IV) estimation as differentiable layers, producing causal effect estimates rather than correlations. (O2) Show that the causal architecture correctly identifies zero effect in placebo tests where generic ML reports spurious ESG-return correlations. (O3) Provide regulators with a tool to distinguish genuine ESG impact from greenwashing.
- **Methodology:** The architecture has three differentiable stages inspired by DML (Chernozhukov et al. 2018): (i) a nuisance estimation network that predicts ESG scores and financial returns from confounders (sector, size, momentum, macro) using flexible neural nets, (ii) a residualization layer that orthogonalizes both treatment (ESG) and outcome (returns) with respect to the nuisance predictions, and (iii) a causal estimation head that regresses orthogonalized returns on orthogonalized ESG scores. The IV extension adds a first-stage network predicting ESG from instruments (regulatory shocks, index inclusion events) and uses predicted ESG in the second stage. The entire pipeline is trained end-to-end with a loss that combines prediction accuracy and IV validity diagnostics (first-stage F-statistic, Sargan test statistic as penalty terms). Confidence intervals use the DML cross-fitting procedure.
- **AI integral:** The neural DML/IV architecture with embedded econometric identification as differentiable layers is the AI contribution. Causal econometric theory (Angrist-Imbens, Chernozhukov) provides the structural framework. This is not standard multi-modal classification (addressing reviewer C2 concern about old DC10).
- **Outputs:** 2 publications (ICML + Review of Financial Studies), CausalESG library, feeds into DC11 (regulatory compliance evidence).
- **Secondments:** BIS Innovation Hub Basel (4 months, M14-17, ESG data from BIS green bond database), TU Delft (2 months, M26-27, integration with DC9 climate-finance framework).

**DC11: Ontology-Guided Neural Architectures for EU AI Act-Compliant Financial Decisions**

- **Host:** WU Vienna, Institute for Information Systems, Austria
- **Supervisors:** Prof. Axel Polleres (WU Vienna, main), Prof. Massimo Guidolin (Bocconi, co-supervisor), Dr. Sarah Chen (Bloomberg LP, industry mentor)
- **Objectives:** (O1) Build a neural network whose architecture is generated from a formal ontology of EU AI Act requirements (transparency, fairness, human oversight), so that compliance is guaranteed by construction rather than tested post-hoc. (O2) Demonstrate that ontology-guided architectures achieve equivalent predictive performance to unconstrained models while satisfying all testable AI Act requirements automatically. (O3) Provide a compliance certification toolkit for financial institutions deploying AI.
- **Methodology:** The EU AI Act mandates specific properties for high-risk AI systems (financial credit scoring, insurance pricing). DC11 formalizes these as a regulatory ontology in OWL: concepts include Transparency (requires feature attribution), Fairness (requires demographic parity within epsilon), Human Override (requires confidence-gated output). The architecture compiler reads the ontology and generates a neural network with built-in compliance modules: (i) an integrated gradient attribution layer (transparency), (ii) a fairness-constrained output layer that projects predictions onto the feasible set satisfying demographic parity (using a differentiable projection operator), (iii) a confidence calibration head that triggers human review when uncertainty exceeds a threshold. The compiler is the key artifact -- given any regulatory ontology, it produces a compliant architecture. Training uses a multi-objective loss: L = L_prediction + sum_i lambda_i * L_compliance_i.
- **AI integral:** The ontology-to-architecture compiler is the AI contribution. Regulatory theory (EU AI Act requirements) provides the structural constraints.
- **Outputs:** 2 publications (FAccT + Artificial Intelligence journal), RegulatoryCompiler toolkit, retrospective compliance assessment of all 12 ATLAS-FIN architectures.
- **Secondments:** Bloomberg LP London (4 months, M15-18, financial decision systems compliance audit), ZHAW (2 months, M27-28, compliance testing of DC1-DC4 architectures).

**DC12: Federated Learning with Financial-Heterogeneity-Aware Aggregation**

- **Host:** University of Helsinki, Department of Computer Science, Finland
- **Supervisors:** Prof. Sami Kaski (University of Helsinki, main), Prof. Axel Polleres (WU Vienna, co-supervisor), Dr. Marco Frey (Swiss Re, industry mentor)
- **Objectives:** (O1) Develop a federated learning aggregation algorithm that accounts for financial data heterogeneity across institutions (different asset classes, regulatory regimes, risk profiles, data quality) instead of treating all clients as i.i.d. (O2) Show that heterogeneity-aware aggregation outperforms FedAvg and FedProx on non-i.i.d. financial data by at least 20% in convergence speed and 10% in final model quality. (O3) Enable privacy-preserving cross-institutional model training for systemic risk monitoring.
- **Methodology:** Financial institutions hold data that is non-i.i.d. in structured ways: a retail bank's loss distribution differs from an investment bank's not randomly but due to business model differences. DC12 exploits this structure. The aggregation server maintains a latent representation of each client's data distribution type (learned from gradient statistics, not raw data). Aggregation weights are computed by a meta-network that takes client embeddings as input and outputs mixing weights, so that clients with similar financial profiles contribute more to each other's updates. Formally: w_global = sum_i alpha_i(e_1,...,e_n) * w_i, where alpha_i is produced by an attention mechanism over client embeddings e_i. The client embeddings are updated using gradient statistics (gradient norms, loss curvature) without sharing raw data. A differential privacy mechanism (Gaussian noise calibrated to sensitivity) protects gradient statistics.
- **AI integral:** The heterogeneity-aware federated aggregation with financial-structure-informed client embeddings is the AI contribution. Financial theory (institutional heterogeneity, Basel III bank categorization) provides the structural prior.
- **Outputs:** 2 publications (NeurIPS + Journal of Financial Intermediation), HeteroFedFinance library.
- **Secondments:** Swiss Re Zurich (4 months, M13-16, federated learning across insurance subsidiaries), M42 Abu Dhabi (2 months, M25-26, computational infrastructure for large-scale federated experiments).

## 2.3 Methodology

### Overarching Framework: Financial Theory as Inductive Bias

The network's methodological unity rests on a single design principle: financial domain knowledge enters the AI system through architecture, not through data preprocessing or post-hoc evaluation. This manifests differently in each cluster:

- **Cluster 1 (Markets):** Causal structure (DC1), distributional constraints (DC2), temporal structure (DC3), and PDEs (DC4) enter through attention masks, loss penalties, positional encodings, and physics-informed layers.
- **Cluster 2 (Stability):** Network topology (DC5), agent heterogeneity (DC6), non-stationarity (DC7), and no-arbitrage (DC8) enter through hypergraph message passing, role-specific policy networks, regime-switching latent variables, and constrained generator layers.
- **Cluster 3 (Sustainability):** Climate physics (DC9), causal identification (DC10), regulatory ontology (DC11), and institutional heterogeneity (DC12) enter through neural ODE constraints, DML layers, architecture compilation, and structured aggregation.

### Interdisciplinary Approach

Each DC bridges at least two disciplines: AI/CS provides the architectural toolkit; financial economics, climate science, or law provides the structural constraints. Co-supervision enforces this: every DC has a main supervisor from one discipline and a co-supervisor from another.

### Gender Dimension

Where relevant, DCs consider gender-differentiated impacts: DC10 examines whether ESG causal effects differ by firm gender-diversity metrics, DC11 includes gender as a protected attribute in fairness constraints, and DC6 tests whether microstructure patterns differ when agent populations are parameterized to reflect gender-based differences in trading behavior documented in behavioral finance.

### Open Science

All code is published on the Digital-AI-Finance GitHub organization under MIT license. Pre-registration of key experiments on OSF before data analysis begins. FAIR data principles applied where financial data permits; DC2 synthetic data published without restriction. All DCs produce Docker containers for full reproducibility. Negative results published.

## 2.4 Training Programme

### Table 1: Network-Wide Training Events

| # | Event | Location | Month | Duration | Content | Lead |
|---|-------|----------|-------|----------|---------|------|
| T1 | Kick-off School | ZHAW Winterthur | M3 | 5 days | Network introduction, research methodology, scientific writing, ethics | ZHAW |
| T2 | AI Architecture Workshop | TU Munich | M9 | 5 days | Hands-on: transformers, GNNs, PINNs, diffusion models, federated learning | TU Munich |
| T3 | Financial Data Bootcamp | Bloomberg London | M12 | 5 days | Bloomberg Terminal, alternative data, data cleaning, financial databases | Bloomberg |
| T4 | Causal Inference Methods School | Imperial College | M15 | 4 days | Causal discovery, DML, IV methods, DAG estimation | Imperial |
| T5 | Mid-term Conference | Bocconi Milan | M24 | 3 days | DC progress presentations, peer review, cross-cluster integration | Bocconi |
| T6 | Responsible AI and Regulation Week | WU Vienna | M30 | 5 days | EU AI Act compliance, fairness, interpretability, ethics in financial AI | WU Vienna |
| T7 | Industry Innovation Week | Swiss Re / M42 | M33 | 5 days | Product development, IP strategy, startup ecosystem, venture capital | Swiss Re |
| T8 | Transferable Skills: Communication | ETH Zurich | M18 | 3 days | Science communication, policy briefing writing, media training | ETH |
| T9 | Transferable Skills: Career | University of Helsinki | M27 | 3 days | Career planning, job market preparation, interview skills, networking | Helsinki |
| T10 | Transferable Skills: Leadership | TU Delft | M36 | 3 days | Project management, team leadership, conflict resolution | TU Delft |
| T11 | Final Conference | M42 Abu Dhabi | M42 | 3 days | Final results, policy recommendations, public outreach, industry demos | ZHAW + M42 |

### Supervision Model

Each DC has triple supervision: (1) Main supervisor providing domain expertise and daily guidance, (2) Co-supervisor from a complementary discipline (AI or finance, whichever the main supervisor is not) at a different institution, (3) Industry mentor from a non-academic partner providing practical context and career guidance. Supervisory team meets monthly (video). DC and main supervisor meet weekly.

### Career Development Plans

Within 3 months of recruitment, each DC produces an Individual Career Development Plan (ICDP) identifying: target career path, skill gaps, training events to attend, secondment objectives, publication strategy, and network engagement milestones. ICDPs reviewed at M12, M24, M36.

### Secondment Strategy

Every DC completes at least one secondment (3-6 months) at a non-academic associated partner in a different country from their host institution. Secondments are research-integrated (not observational) -- each DC's secondment objectives are specified in Section 2.2. Total secondment time does not exceed 50% of fellowship duration per MSCA rules.

## 2.5 Supervision

### Supervisory Board

The Supervisory Board comprises all 12 main supervisors, chaired by the Coordinator (Prof. Osterrieder, ZHAW). The Board meets biannually (M6, M12, M18, M24, M30, M36, M42, M48) to review DC progress, authorize secondments, resolve conflicts, and ensure cross-cluster integration.

### Progress Reviews

Formal 6-monthly progress reviews for each DC, conducted by the Supervisory Board. Each review assesses: research progress against milestones, training event attendance, secondment planning, publication pipeline, and well-being. DCs at risk receive an intensified supervision plan.

### Quality Assurance

- External Advisory Board (3 members: 1 senior academic, 1 industry leader, 1 policy maker) provides annual review.
- Annual DC satisfaction survey with anonymous feedback mechanism.
- Conflict resolution protocol: DC -> main supervisor -> cluster lead -> coordinator -> External Advisory Board.

---

# 3. IMPACT

## 3.1 Contribution to Structuring Doctoral Training

ATLAS-FIN's collective training exceeds the sum of individual PhD programmes because: (a) no single institution can provide both cutting-edge AI architecture training AND deep financial domain expertise AND regulatory understanding AND industry exposure -- the network does; (b) cross-cluster co-authored papers force DCs to engage beyond their own project; (c) the shared evaluation framework (RO2-RO3) creates a common scientific language across all 12 DCs.

**Non-academic sector role beyond secondments:** Bloomberg co-designs T3 (Financial Data Bootcamp) and provides guest lectures in T2. Swiss Re co-designs T7 (Industry Innovation Week) and participates in annual progress reviews. BIS Innovation Hub contributes to T6 (Responsible AI Week) with regulatory perspective. M42 hosts the final conference and provides computational infrastructure access throughout.

**Sustainable elements:** The training curriculum (T1-T11 materials) is published as Open Educational Resources (OER) under CC-BY. Partner universities commit to continuing AI-in-Finance modules developed through the network. The reproducible benchmark infrastructure (RO3) becomes a permanent community resource.

## 3.2 Career Perspectives and Employability

ATLAS-FIN DCs are uniquely positioned at the intersection of three high-demand areas: AI engineering, financial expertise, and regulatory understanding. Career paths include: quantitative research in asset management and investment banking, fintech founding and product development, central bank and supervisory authority analytical roles, RegTech and compliance technology, and tenure-track academic positions in the growing field of financial AI.

The triple-supervision model (academic + cross-disciplinary + industry) and mandatory non-academic secondments ensure DCs are not solely academy-oriented. Industry mentors provide ongoing career guidance and professional network access.

## 3.3 Dissemination, Exploitation and Communication

**Scientific dissemination:** Target 24+ peer-reviewed publications (2 per DC) in top AI venues (NeurIPS, ICML, ICLR, AAAI, KDD, AISTATS, FAccT, UAI, AAMAS) and top finance journals (Journal of Financial Economics, Review of Financial Studies, Journal of Financial and Quantitative Analysis, Mathematical Finance, Quantitative Finance, Journal of Banking and Finance, Journal of Financial Stability).

**Policy dissemination:** Annual policy briefs submitted to ECB, BIS, ESRB, and national supervisory authorities. Topics: systemic risk early warning (DC5), climate stress testing (DC9), AI Act compliance (DC11), synthetic data for supervision (DC2).

**Open-source tools:** All software published on the Digital-AI-Finance GitHub organization (MIT license). Target: 12 software libraries, each with documentation, tutorials, and Docker containers.

**Industry engagement:** Biannual workshops with Bloomberg and Swiss Re for technology transfer. Industry Innovation Week (T7) includes startup pitch session for DCs considering commercialization.

**Public engagement:** Final conference at M42 Abu Dhabi includes public day with non-specialist presentations. Media strategy: press releases for major publications, social media presence, participation in European Researchers' Night.

## 3.4 Expected Impacts

**Scientific:** If the unifying thesis holds, ATLAS-FIN establishes theory-aware AI as a recognized paradigm in financial science, analogous to physics-informed ML in physical sciences. The benchmark infrastructure (RO3) enables the broader community to extend the paradigm.

**Societal:** Better systemic risk monitoring (DC5, DC7) contributes to financial stability. Climate-finance tools (DC9) improve transition risk assessment. Regulatory compliance tools (DC11) increase transparency of AI-driven financial decisions. Causal ESG attribution (DC10) combats greenwashing.

**Economic:** 12 trained AI-finance specialists enter the European workforce. Open-source tools reduce barriers for European fintech companies. Synthetic data infrastructure (DC2) reduces dependence on expensive proprietary datasets.

---

# 4. IMPLEMENTATION

## 4.1 Work Packages

### WP1: Causal and Structural AI for Markets (M1-M48)
- **Lead:** Imperial College London | **Participants:** ZHAW, TU Munich, Bloomberg, Swiss Re
- **DCs:** DC1, DC2, DC3, DC4
- **Objectives:** Develop and validate theory-aware architectures for market-level financial AI
- **Tasks:**
  - T1.1: Design and implement causal-temporal transformer (DC1, M1-M30)
  - T1.2: Develop constrained diffusion models (DC2, M1-M30)
  - T1.3: Build asynchronous temporal fusion architecture (DC3, M1-M30)
  - T1.4: Implement no-arbitrage PINNs (DC4, M1-M30)
  - T1.5: Cross-DC evaluation using shared benchmarks and synthetic data (all, M24-M42)
  - T1.6: Integration with WP2 and WP3 (all, M30-M48)
- **Deliverables:** D1.1 Benchmark suite v1 (M18), D1.2 Software libraries v1 (M24), D1.3 Cross-DC evaluation report (M36), D1.4 Final integrated results (M44)
- **Milestones:** MS1 All DC1-4 architectures prototyped (M15), MS2 Cross-DC evaluation protocol agreed (M18)

### WP2: Network AI for Financial Stability (M1-M48)
- **Lead:** TU Munich | **Participants:** Bocconi, Imperial, ETH Zurich, ZHAW, BIS Innovation Hub
- **DCs:** DC5, DC6, DC7, DC8
- **Objectives:** Develop and validate theory-aware architectures for system-level financial stability
- **Tasks:**
  - T2.1: Design THGNN for systemic risk (DC5, M1-M30)
  - T2.2: Build heterogeneous MARL simulator (DC6, M1-M30)
  - T2.3: Develop regime-switching causal discovery (DC7, M1-M30)
  - T2.4: Implement constrained adversarial stress testing (DC8, M1-M30)
  - T2.5: Cross-DC integration: DC7 causal graphs feed DC5 and DC8 (M18-M36)
  - T2.6: Systemic risk early-warning system integration (all, M30-M48)
- **Deliverables:** D2.1 Systemic risk benchmark suite (M18), D2.2 Software libraries v1 (M24), D2.3 Early-warning indicator report (M36), D2.4 Final integrated results (M44)
- **Milestones:** MS3 All DC5-8 architectures prototyped (M15), MS4 Cross-cluster data pipeline operational (DC2 -> DC5,6,8) (M12)

### WP3: AI for Sustainability and Regulation (M1-M48)
- **Lead:** TU Delft | **Participants:** Bocconi, WU Vienna, Helsinki, Swiss Re, M42, BIS Innovation Hub
- **DCs:** DC9, DC10, DC11, DC12
- **Objectives:** Develop and validate theory-aware architectures for sustainable finance and regulatory compliance
- **Tasks:**
  - T3.1: Build climate-finance neural ODE (DC9, M1-M30)
  - T3.2: Develop causal ESG attribution architecture (DC10, M1-M30)
  - T3.3: Implement ontology-guided architecture compiler (DC11, M1-M30)
  - T3.4: Design heterogeneity-aware federated learning (DC12, M1-M30)
  - T3.5: Retrospective compliance testing of all 12 architectures via DC11 (M30-M42)
  - T3.6: Integration with NGFS climate scenarios and EU AI Act requirements (M24-M48)
- **Deliverables:** D3.1 Climate-finance benchmark (M18), D3.2 Software libraries v1 (M24), D3.3 Compliance assessment of all DCs (M40), D3.4 Final integrated results (M44)
- **Milestones:** MS5 All DC9-12 architectures prototyped (M15), MS6 Regulatory ontology v1 complete (M12)

### WP4: Training and Secondments (M1-M48)
- **Lead:** ZHAW | **Participants:** All beneficiaries and associated partners
- **Objectives:** Deliver the network-wide training programme and coordinate secondments
- **Tasks:**
  - T4.1: Organize 11 network-wide training events (M3-M42)
  - T4.2: Coordinate and monitor DC secondments (M10-M36)
  - T4.3: Individual Career Development Plans (M3, M12, M24, M36)
  - T4.4: External training (conferences, summer schools) support
- **Deliverables:** D4.1 Training programme handbook (M3), D4.2 Secondment reports (M18, M36), D4.3 OER training materials (M42)
- **Milestones:** MS7 All DCs recruited and ICDPs completed (M6)

### WP5: Dissemination, Exploitation and Communication (M1-M48)
- **Lead:** Bocconi University | **Participants:** All
- **Objectives:** Maximize scientific, policy, and societal impact of network outputs
- **Tasks:**
  - T5.1: Publication strategy and open-access management
  - T5.2: Open-source software curation on GitHub
  - T5.3: Annual policy briefs for regulators
  - T5.4: Industry workshops with Bloomberg and Swiss Re
  - T5.5: Public engagement and media strategy
  - T5.6: Final public conference at M42
- **Deliverables:** D5.1 Dissemination plan (M3), D5.2 Policy briefs (M12, M24, M36, M44), D5.3 Project website (M2), D5.4 Final dissemination report (M46)
- **Milestones:** MS8 Website and GitHub org operational (M3)

### WP6: Management and Coordination (M1-M48)
- **Lead:** ZHAW | **Participants:** All
- **Objectives:** Effective project governance, financial management, and reporting
- **Tasks:**
  - T6.1: Consortium governance and Supervisory Board meetings
  - T6.2: Financial management and EU reporting
  - T6.3: Risk monitoring and mitigation
  - T6.4: External Advisory Board management
  - T6.5: RAISE community engagement and cross-network interaction
- **Deliverables:** D6.1 Consortium Agreement (M1), D6.2 Annual progress reports (M12, M24, M36), D6.3 Final report (M48), D6.4 Data Management Plan (M6)
- **Milestones:** MS9 Consortium Agreement signed (M2), MS10 External Advisory Board constituted (M4)

## 4.2 Deliverables Table

| ID | Title | WP | Month | Type | Dissemination |
|----|-------|----|-------|------|---------------|
| D1.1 | Benchmark suite for market AI v1 | WP1 | M18 | Dataset | Public |
| D1.2 | Software libraries for DC1-4 v1 | WP1 | M24 | Software | Public |
| D1.3 | Cross-DC evaluation report for Cluster 1 | WP1 | M36 | Report | Public |
| D1.4 | Final integrated results for Cluster 1 | WP1 | M44 | Report | Public |
| D2.1 | Systemic risk benchmark suite | WP2 | M18 | Dataset | Public |
| D2.2 | Software libraries for DC5-8 v1 | WP2 | M24 | Software | Public |
| D2.3 | Early-warning indicator report | WP2 | M36 | Report | Confidential |
| D2.4 | Final integrated results for Cluster 2 | WP2 | M44 | Report | Public |
| D3.1 | Climate-finance benchmark | WP3 | M18 | Dataset | Public |
| D3.2 | Software libraries for DC9-12 v1 | WP3 | M24 | Software | Public |
| D3.3 | Compliance assessment of all DCs | WP3 | M40 | Report | Public |
| D3.4 | Final integrated results for Cluster 3 | WP3 | M44 | Report | Public |
| D4.1 | Training programme handbook | WP4 | M3 | Report | Public |
| D4.2a | Secondment mid-term report | WP4 | M18 | Report | Consortium |
| D4.2b | Secondment final report | WP4 | M36 | Report | Consortium |
| D4.3 | OER training materials | WP4 | M42 | OER | Public |
| D5.1 | Dissemination and exploitation plan | WP5 | M3 | Report | Public |
| D5.2 | Policy briefs (annual, 4 editions) | WP5 | M12,24,36,44 | Report | Public |
| D5.3 | Project website | WP5 | M2 | Website | Public |
| D5.4 | Final dissemination report | WP5 | M46 | Report | Public |
| D6.1 | Consortium Agreement | WP6 | M1 | Legal | Consortium |
| D6.2 | Annual progress reports (3 editions) | WP6 | M12,24,36 | Report | EU Services |
| D6.3 | Final report | WP6 | M48 | Report | EU Services |
| D6.4 | Data Management Plan | WP6 | M6 | Report | Public |

## 4.3 Milestones Table

| ID | Title | WP | Month | Means of Verification |
|----|-------|----|-------|-----------------------|
| MS1 | DC1-4 architectures prototyped | WP1 | M15 | Working code on GitHub, internal demo |
| MS2 | Cross-DC evaluation protocol agreed | WP1 | M18 | Signed protocol document |
| MS3 | DC5-8 architectures prototyped | WP2 | M15 | Working code on GitHub, internal demo |
| MS4 | Synthetic data pipeline operational | WP2 | M12 | DC2 delivers datasets to DC1,3,5,6,8 |
| MS5 | DC9-12 architectures prototyped | WP3 | M15 | Working code on GitHub, internal demo |
| MS6 | Regulatory ontology v1 complete | WP3 | M12 | OWL file published, reviewed by WU Vienna |
| MS7 | All DCs recruited, ICDPs completed | WP4 | M6 | Employment contracts + ICDP documents |
| MS8 | Website and GitHub org operational | WP5 | M3 | URLs accessible, content populated |
| MS9 | Consortium Agreement signed | WP6 | M2 | Signed CA |
| MS10 | External Advisory Board constituted | WP6 | M4 | Board appointment letters |

## 4.4 Risk Assessment

| # | Risk | Likelihood | Impact | Mitigation |
|---|------|-----------|--------|------------|
| R1 | **Data access:** proprietary financial data unavailable or too expensive | High | High | DC2 synthetic data as fallback for all DCs; Bloomberg provides academic data access; BIS provides aggregated statistics; secondments provide temporary access to proprietary data under NDA |
| R2 | DC recruitment delays (mobility rule constraints) | Medium | High | Begin recruitment M1, staggered start allowed (M3-M6), wide advertising via EURAXESS, target institutions in multiple countries |
| R3 | Theory-aware architectures underperform generic ML on specific tasks | Medium | Medium | This is a valid scientific finding (negative results published); RO2 explicitly tests this; network thesis refined rather than falsified by partial failures |
| R4 | Computational costs exceed budget for large-scale training | Medium | Medium | M42 provides HPC access; ZHAW has GPU cluster; RAISE community infrastructure access; pre-training on synthetic data (DC2) reduces compute for real data fine-tuning |
| R5 | Cross-cluster integration insufficient | Medium | Medium | Enforced via joint deliverables (D1.3, D2.3, D3.3), co-authored papers, DC7 causal graphs mandated as input to DC1/DC5/DC10, DC11 compliance review of all DCs |
| R6 | DC drops out or underperforms | Low | High | Early warning via 6-monthly reviews; supervisory board can reassign co-supervisor, adjust scope, extend secondment for additional support |
| R7 | Regulatory changes (EU AI Act amendments) invalidate DC11 ontology | Medium | Low | Ontology is modular; DC11 timeline includes regulatory monitoring; WU Vienna has regulatory law expertise |
| R8 | Associated partner withdraws | Low | Medium | Letters of commitment obtained pre-submission; alternative industry partners identified; core research hosted at academic beneficiaries |
| R9 | Ethical issues with financial AI applications discovered during research | Low | Medium | Ethics board review at M0; continuous ethics monitoring; DC11 compliance framework provides self-assessment capability |
| R10 | Coordination overhead for 12-partner consortium | Medium | Low | Experienced coordinator (ZHAW); dedicated project manager funded from management costs; clear WP structure with delegated leadership |

## 4.5 DC Table (Table 3.1d Equivalent)

| DC | Title (short) | Host | Country | Duration | Start | Main Supervisor | Co-supervisor | Industry Mentor | Secondment 1 | Secondment 2 |
|----|---------------|------|---------|----------|-------|-----------------|---------------|-----------------|---------------|---------------|
| DC1 | Causal-Temporal Transformer | ZHAW | CH | 36 mo | M3 | Osterrieder | Leippold (UZH) | Chen (Bloomberg) | Bloomberg London 4mo | Imperial 2mo |
| DC2 | Constrained Diffusion Models | ZHAW | CH | 36 mo | M3 | Osterrieder | Cheridito (ETH) | Frey (Swiss Re) | Swiss Re Zurich 4mo | ETH Zurich 2mo |
| DC3 | Async Temporal Fusion | Imperial | UK | 36 mo | M3 | Schuller | Osterrieder (ZHAW) | Passalis (Bloomberg) | Bloomberg London 4mo | ZHAW 2mo |
| DC4 | No-Arbitrage PINNs | TU Munich | DE | 36 mo | M3 | Deelstra | Cuchiero (UniVie) | Steiner (Swiss Re) | Swiss Re Zurich 3mo | ETH Zurich 3mo |
| DC5 | Temporal Hypergraph NN | TU Munich | DE | 36 mo | M3 | Gunnemann | Osterrieder (ZHAW) | Amberg (BIS) | BIS Basel 4mo | Bocconi 2mo |
| DC6 | Heterogeneous MARL | Bocconi | IT | 36 mo | M3 | Tebaldi | Schuller (Imperial) | Chen (Bloomberg) | Bloomberg NY 4mo | ZHAW 2mo |
| DC7 | Regime-Switching Causal | Imperial | UK | 36 mo | M3 | Kantas | Deelstra (TUM) | Amberg (BIS) | BIS Basel 4mo | TU Munich 2mo |
| DC8 | Constrained Stress GAN | ETH Zurich | CH | 36 mo | M3 | Teichmann | Osterrieder (ZHAW) | Frey (Swiss Re) | Swiss Re Zurich 4mo | BIS Basel 2mo |
| DC9 | Climate-Finance NeuralODE | TU Delft | NL | 36 mo | M3 | Storm | Osterrieder (ZHAW) | Frey (Swiss Re) | Swiss Re Zurich 4mo | M42 Abu Dhabi 2mo |
| DC10 | Causal ESG Attribution | Bocconi | IT | 36 mo | M3 | Guidolin | Storm (TU Delft) | Amberg (BIS) | BIS Basel 4mo | TU Delft 2mo |
| DC11 | Ontology-Guided Compliance | WU Vienna | AT | 36 mo | M3 | Polleres | Guidolin (Bocconi) | Chen (Bloomberg) | Bloomberg London 4mo | ZHAW 2mo |
| DC12 | Heterogeneity-Aware FedLearn | Helsinki | FI | 36 mo | M3 | Kaski | Polleres (WU Vienna) | Frey (Swiss Re) | Swiss Re Zurich 4mo | M42 Abu Dhabi 2mo |

## 4.6 Consortium Description

### Academic Beneficiaries (8)

**1. ZHAW School of Engineering (Coordinator), Switzerland**
Role: Network coordinator, hosts DC1 and DC2, leads WP4 and WP6. Centre for AI at ZHAW with established fintech research group. Prof. Osterrieder: 80+ publications in quantitative finance and financial ML, coordinator of Digital-AI-Finance platform, PI of Swiss National Science Foundation projects in AI for finance.

**2. Imperial College London, United Kingdom**
Role: Hosts DC3 and DC7, leads WP1. Department of Computing and Department of Mathematics provide complementary AI and mathematical finance expertise. Prof. Schuller: Fellow of IEEE, 900+ publications in machine learning and affective computing. Prof. Kantas: expert in Monte Carlo methods and causal inference for dynamical systems.

**3. TU Munich, Germany**
Role: Hosts DC4 and DC5, leads WP2. Departments of Mathematics and Informatics rank top-3 in continental Europe for AI. Prof. Deelstra: 60+ publications in mathematical finance and derivatives pricing. Prof. Gunnemann: leading researcher in graph neural networks with 100+ publications.

**4. ETH Zurich, Switzerland**
Role: Hosts DC8. Department of Mathematics with world-leading expertise in stochastic analysis and mathematical finance. Prof. Teichmann: 100+ publications in deep learning for finance and mathematical foundations of neural network-based methods.

**5. Bocconi University, Italy**
Role: Hosts DC6 and DC10, leads WP5. Top European economics and finance school. Prof. Tebaldi: expert in asset pricing and market microstructure. Prof. Guidolin: 80+ publications in empirical asset pricing and ESG finance.

**6. TU Delft, Netherlands**
Role: Hosts DC9, leads WP3. Faculty of Technology, Policy and Management integrates engineering with economics and governance. Prof. Storm: expert in macroeconomics and climate-economy modeling with policy impact.

**7. WU Vienna, Austria**
Role: Hosts DC11. Institute for Information Systems combines semantic web, knowledge representation, and regulatory technology. Prof. Polleres: leading researcher in ontologies, knowledge graphs, and their application to regulatory compliance.

**8. University of Helsinki, Finland**
Role: Hosts DC12. Department of Computer Science with Finnish Center for AI (FCAI). Prof. Kaski: Director of FCAI, 300+ publications, pioneer in Bayesian machine learning and federated learning, member of the Finnish Academy of Science and Letters.

### Non-Academic Associated Partners (4)

**Bloomberg LP (London/New York):** Provides real-time and historical financial data access, industry mentoring for DC1, DC3, DC6, DC11. Hosts secondments and co-designs T3 (Financial Data Bootcamp).

**Swiss Re (Zurich):** Global reinsurer providing insurance data access, risk modeling expertise, industry mentoring for DC2, DC4, DC8, DC9, DC12. Hosts secondments and co-designs T7 (Industry Innovation Week).

**M42 (Abu Dhabi):** AI-focused institution providing high-performance computing infrastructure, hosts final conference (T11), secondments for DC9 and DC12 with GPU cluster access.

**BIS Innovation Hub (Basel):** Central bank innovation arm providing macro-prudential data access, policy perspective, industry mentoring for DC5, DC7, DC10. Hosts secondments with access to BIS statistical resources.

### Geographic Distribution and 40% Cap Compliance

| Country | DCs Hosted | Beneficiaries | Estimated EU Contribution Share |
|---------|-----------|---------------|-------------------------------|
| Switzerland (CH) | DC1, DC2, DC8 | ZHAW, ETH Zurich | 25% (3/12 DCs) |
| United Kingdom (UK) | DC3, DC7 | Imperial College | 17% (2/12 DCs) |
| Germany (DE) | DC4, DC5 | TU Munich | 17% (2/12 DCs) |
| Italy (IT) | DC6, DC10 | Bocconi | 17% (2/12 DCs) |
| Netherlands (NL) | DC9 | TU Delft | 8% (1/12 DCs) |
| Austria (AT) | DC11 | WU Vienna | 8% (1/12 DCs) |
| Finland (FI) | DC12 | Univ. Helsinki | 8% (1/12 DCs) |

No country exceeds 25%, well within the 40% cap.

## 4.7 Data Access Strategy

| Data Need | Source | Access Mechanism | DC(s) |
|-----------|--------|-----------------|-------|
| Historical equity/FX/fixed income returns | Bloomberg | Academic license via associated partner | DC1, DC3, DC6 |
| Real-time market data feeds | Bloomberg Terminal | Secondment access at Bloomberg London/NY | DC3, DC6 |
| Options surfaces and derivatives data | Bloomberg/Refinitiv | Academic license + ZHAW institutional access | DC4, DC8 |
| Interbank exposure networks | BIS | Aggregated statistics (publicly available) + secondment access to confidential data under NDA | DC5, DC7 |
| ESG scores and sustainability data | Bloomberg ESG | Academic license via associated partner | DC10 |
| Climate scenarios (NGFS) | NGFS/ECB | Publicly available | DC9 |
| Insurance loss data | Swiss Re | Secondment access under NDA | DC2, DC9 |
| Macro-financial time series | ECB SDW, FRED, BIS | Publicly available | DC7, DC9, DC10 |
| EU AI Act regulatory text | EUR-Lex | Publicly available | DC11 |
| **Synthetic financial data** | **DC2 (internal)** | **Network-generated, published openly** | **DC1, DC3, DC5, DC6, DC8** |

DC2 synthetic data serves as the network's internal data infrastructure, providing a fallback for any DC facing proprietary data access constraints. Synthetic datasets are designed to match real data statistical properties (11 stylized facts) while containing no proprietary information.

---

# 5. BUDGET SUMMARY

### Unit Costs (2026-2027 MSCA Work Programme, corrected)

| Component | EUR/month |
|-----------|-----------|
| Living allowance (base, pre-CCC) | 4,250 |
| Mobility allowance | 710 |
| Research, training, networking (institutional) | 1,600 |
| Management and indirect (institutional) | 1,200 |
| **Base total per researcher/month** | **7,760** |

### Total Budget Estimate

| Item | Calculation | Amount (EUR) |
|------|-------------|-------------|
| 12 DCs x 36 months | 432 person-months x EUR 7,760 | 3,352,320 |
| Country correction coefficients (weighted avg ~1.08) | +8% on living allowance component | +132,192 |
| Family allowance (estimated 30% of DCs) | 4 DCs x 36mo x EUR 660 | +95,040 |
| **Estimated total EU contribution** | | **~3,579,552** |

Note: Actual budget depends on country correction coefficients applied to the living allowance for each DC's host country. The above uses a weighted average. The 40% country cap is satisfied (Section 4.6).

### Budget by Country (Estimated, living allowance CCC-adjusted)

| Country | CCC | DCs | Monthly Living (CCC-adjusted) | 36-month researcher cost | RTN + Mgmt (36mo) | Country Total |
|---------|-----|-----|-------------------------------|--------------------------|--------------------|----|
| CH | 163.7% | 3 | 6,957 | 3 x 276,012 | 3 x 100,800 | 1,130,436 |
| UK | 143.5% | 2 | 6,099 | 2 x 245,124 | 2 x 100,800 | 691,848 |
| DE | 101.5% | 2 | 4,314 | 2 x 180,864 | 2 x 100,800 | 563,328 |
| IT | 93.8% | 2 | 3,987 | 2 x 169,092 | 2 x 100,800 | 539,784 |
| NL | 111.8% | 1 | 4,752 | 196,632 | 100,800 | 297,432 |
| AT | 109.4% | 1 | 4,650 | 192,960 | 100,800 | 293,760 |
| FI | 116.4% | 1 | 4,947 | 203,652 | 100,800 | 304,452 |
| | | | | | **Total** | **~3,821,040** |

Note: Mobility allowance (EUR 710/mo) included in researcher cost. Family allowance omitted from this table for simplicity. Actual amounts determined at grant agreement.

---

# 6. RAISE SCOPE COMPLIANCE

### Systematic Verification: AI is Integral and Indispensable

| DC | Novel AI Architecture | Financial Theory as Inductive Bias | Passes RAISE Test? |
|----|----------------------|-----------------------------------|--------------------|
| DC1 | SEM-constrained temporal attention | Causal structure from structural equation models | Yes: attention mechanism is structurally novel |
| DC2 | Stylized-fact-constrained score function | 11 financial distributional constraints | Yes: score function design is the contribution |
| DC3 | Asynchronous temporal fusion with GP-inspired temporal kernels | Market microstructure information arrival theory | Yes: temporal alignment mechanism is new |
| DC4 | PINN with no-arbitrage PDE constraints | Black-Scholes/Heston/rough vol PDEs | Yes: physics-informed architecture for finance |
| DC5 | Temporal hypergraph message passing with exposure weighting | Financial network clearing mechanisms | Yes: hypergraph architecture for multi-lateral contracts |
| DC6 | Heterogeneous-agent MARL with theory-prescribed role differentiation | Kyle/Glosten-Milgrom microstructure models | Yes: agent architecture diversity is structurally imposed |
| DC7 | Regime-switching NOTEARS with HMM | Macro-financial regime theory (Hamilton) | Yes: non-stationary causal discovery algorithm |
| DC8 | Constrained GAN with financial plausibility layers | No-arbitrage, macro accounting identities | Yes: generator constraints are architecturally novel |
| DC9 | Physics-constrained neural ODE | DICE carbon cycle, energy balance equations | Yes: partially prescribed ODE dynamics |
| DC10 | Neural DML/IV with differentiable econometric layers | Double ML, instrumental variable identification | Yes: econometric identification as architecture |
| DC11 | Ontology-to-architecture compiler | EU AI Act regulatory requirements | Yes: architecture generation from formal specification |
| DC12 | Heterogeneity-aware federated aggregation | Financial institutional heterogeneity (Basel III categories) | Yes: structured client embeddings for aggregation |

All 12 DCs pass. None uses AI instrumentally. Each develops a novel architecture whose design is directly derived from financial-domain structural knowledge.

### AI Training Compliance

All DCs attend T2 (AI Architecture Workshop, M9), which provides doctoral-level training on transformer architectures, graph neural networks, physics-informed neural networks, diffusion models, and federated learning. Additional AI training at T4 (Causal Inference Methods School, M15) and T6 (Responsible AI and Regulation Week, M30).

### RAISE Community Engagement

The network commits to: (a) participating in RAISE annual assembly and cross-network events, (b) sharing training materials and benchmarks with other RAISE networks, (c) contributing to the RAISE computational infrastructure through open-source tool publication, (d) engaging with the RAISE Scientific Advisory Board on financial AI topics.

### China Exclusion

No Chinese entities participate in the consortium as beneficiaries or associated partners, in compliance with the Work Programme restriction on Chinese legal entities in AI-in-Science actions.

---

# 7. ETHICS

**AI ethics as cross-cutting theme.** DC11 provides a network-wide AI ethics assessment framework. All DCs undergo ethics review at T1 (Kick-off School) and T6 (Responsible AI Week).

**Financial data privacy.** DCs handling personal financial data (DC5 interbank exposures, DC12 federated data) comply with GDPR. DC12 embeds differential privacy by design. DC2 synthetic data contains no personal information.

**Fairness in automated financial decisions.** DC11 implements demographic parity constraints. DC10 tests for heterogeneous causal effects across demographic groups. DC6 examines whether market microstructure outcomes depend on agent population composition.

**Dual-use considerations.** The adversarial stress testing tools (DC8) and market microstructure simulators (DC6) could theoretically be misused for market manipulation. Mitigation: responsible disclosure protocols, publication ethics review, tool access requires institutional affiliation.

---

# 8. GENDER AND DIVERSITY

**Supervisory team balance.** The consortium targets at least 40% women among supervisors and co-supervisors. Current named supervisors include Prof. Deelstra, Prof. Cuchiero, and Dr. Chen; additional female co-supervisors will be identified during consortium formation.

**Inclusive recruitment.** DC positions advertised on EURAXESS, field-specific channels, and networks targeting underrepresented groups in AI and finance. Selection committees required to have mixed-gender composition. Recruitment materials explicitly welcome candidates from diverse backgrounds.

**DC gender balance.** The network targets at least 40% women among recruited DCs. Financial incentives: family allowance (EUR 660/month) available to DCs with family obligations. Flexible working arrangements supported by all beneficiaries.

**Gender in research design.** As described in Section 2.3: DC10 examines gender-differentiated ESG effects, DC11 includes gender as protected attribute, DC6 tests behavioral finance gender patterns in agent parameterization.

---

# 9. OPEN SCIENCE

**Code.** All software published on the Digital-AI-Finance GitHub organization (https://github.com/Digital-AI-Finance) under MIT license. Continuous integration, documentation, and tutorials for each library.

**Data.** FAIR principles applied. DC2 synthetic datasets published without restriction on Zenodo with DOI. Real financial data cannot be shared due to licensing, but preprocessing scripts and synthetic replicas are provided. Data Management Plan (D6.4) delivered at M6.

**Pre-registration.** Key experiments for RO2 (theory-aware vs. baselines comparison) pre-registered on the Open Science Framework (OSF) before data analysis begins.

**Reproducibility.** Every DC provides a Docker container with full environment specification, trained model weights (where data licensing permits), and evaluation scripts. Reproducibility verified as part of cross-DC evaluation (D1.3, D2.3, D3.3).

**Negative results.** The network commits to publishing negative results (architectures that do not outperform baselines) as valuable contributions to the research programme. This is scientifically meaningful given the falsifiable unifying thesis.

---

*Document prepared for internal consortium development. Version 2.0, April 2026.*
*ATLAS-FIN: AI Technologies for Leveraging Advanced Science in Finance*
*Coordinating institution: ZHAW School of Engineering, Winterthur, Switzerland*
*Coordinator: Prof. Joerg Osterrieder*
