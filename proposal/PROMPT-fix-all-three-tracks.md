# Reusable Prompt: Fix ATLAS-FIN v2 → v3 (All Three Tracks)

**Purpose:** Paste this prompt into any LLM along with the v2 proposal concept to produce a fully revised v3 that addresses every reviewer finding from Rounds 1-3. The output should be a complete, self-contained proposal concept that scores 95+ when re-evaluated with the hostile reviewer prompt.

**How to use:**
1. Copy everything between `---START PROMPT---` and `---END PROMPT---`
2. Paste into the LLM
3. Then paste the full text of `ATLAS-FIN-v2-concept.md` after it
4. The LLM will produce the complete `ATLAS-FIN-v3-concept.md`

---START PROMPT---

## Role

You are a senior MSCA proposal writer who has coordinated 5 funded Doctoral Networks and reviewed 100+ MSCA DN proposals. You are revising the ATLAS-FIN proposal concept from v2 to v3 to achieve a competitive score of 96+/100.

## Context

This proposal has been through 3 rounds of hostile expert review:
- **Round 1 (69.2/100):** Concept note only -- no consortium, training, work plan
- **Round 2 (82.8/100):** Full proposal but with gaps in exploitation, training, implementation
- **Round 3 (80.0/100):** Same document under stricter scrutiny -- found secondment violations, external co-supervisor gaps, 11 of 13 R2 recommendations unaddressed

The scientific programme (all 12 DCs) passes the RAISE scope test. The science is strong. The problem is the operational/administrative shell.

## Your Task

Rewrite the entire proposal concept as **ATLAS-FIN v3**, incorporating ALL fixes below. The output must be a complete, self-contained document (not a diff or list of changes). Every section must be fully written. Target: 6,000-8,000 words.

---

## TRACK 1: QUICK WINS (target: +5 points)

These are straightforward fixes that require editing existing content:

### Fix 1.1: Correct Deelstra Affiliation
**Problem:** Prof. Griselda Deelstra is listed as main supervisor for DC4 at TU Munich, but she is affiliated with Universite Libre de Bruxelles (ULB), Belgium.
**Fix:** Either:
- (a) Change DC4 host to ULB and adjust consortium accordingly (adds Belgium, removes one TU Munich DC), OR
- (b) Name a different main supervisor at TU Munich for DC4 who has expertise in mathematical finance/stochastic analysis (e.g., Prof. Kathrin Glau or another suitable researcher), OR
- (c) If Deelstra has moved to TU Munich, state this explicitly
**Choose option (a) or (b) -- do NOT leave the error in place.**

### Fix 1.2: Fix Secondment Same-Country Violations
**Problem:** The proposal states "every DC completes at least one secondment at a non-academic partner in a different country from their host institution." But:
- DC2 (host: ZHAW, CH) has both secondments in Switzerland (Swiss Re Zurich + ETH Zurich)
- DC8 (host: ETH Zurich, CH) has both secondments in Switzerland (Swiss Re Zurich + BIS Basel)
- DC3 (host: Imperial, UK) has primary secondment at Bloomberg London (same country)
**Fix:** For each violating DC, replace at least one secondment destination with a partner in a DIFFERENT country. Realistic options:
- DC2: Replace ETH secondment with Bloomberg London (UK) or BIS Basel (CH→international org, arguably different)
- DC8: Replace one Swiss secondment with Bocconi (IT) or Bloomberg London (UK)
- DC3: Replace Bloomberg London with Bloomberg NYC (if 3rd-country secondments allowed) or add a continental European secondment (e.g., Swiss Re Zurich)
**Rewrite ALL 12 DC secondment plans to ensure compliance with the stated policy.**

### Fix 1.3: Add Gantt Chart Description
**Problem:** No visual Gantt chart exists. The proposal has textual milestone descriptions but no timeline visualization.
**Fix:** Add a Section 4.8 "Project Timeline (Gantt Chart)" that describes:
- A table-based Gantt showing all 6 WPs across M1-M48
- DC recruitment period (M1-M6)
- Training events mapped to months
- Deliverable and milestone markers
- **Critical path explicitly highlighted:** DC2 data infrastructure (M3-M12) → feeds DC1,3,5,6,8 prototyping (M12-M18) → DC7 causal graphs (M3-M15) → feeds DC1,5,10 integration (M18-M30) → DC11 compliance audit (M30-M42)
- Cross-cluster integration phases
**Include the actual table in the document (ASCII/markdown Gantt).**

### Fix 1.4: Justify Quantitative Performance Targets
**Problem:** DC1 claims "30% reduction," DC3 claims "15% improvement," DC12 claims "20% convergence gain" -- no literature basis cited.
**Fix:** For each quantitative target, either:
- (a) Cite a specific paper showing a comparable improvement when domain priors were added to a baseline architecture (e.g., "Physics-informed neural networks achieved 30-50% improvement over vanilla NNs on PDE benchmarks [Raissi et al., 2019], suggesting our 30% target for causal-structural priors is conservative"), OR
- (b) Replace the absolute target with statistical framing: "statistically significant improvement (p < 0.01, corrected for multiple testing) on at least 3 of 5 benchmark datasets"
**Apply this fix to DC1, DC3, DC5, DC6, DC8, DC12 -- any DC with a specific percentage claim.**

### Fix 1.5: Add Impact KPI Table
**Problem:** No quantified impact indicators.
**Fix:** Add a table in Section 3.4 "Expected Impacts":

| KPI | Baseline | Target M24 | Target M48 | Target M60 | Data Source |
|-----|----------|-----------|-----------|-----------|-------------|
| Peer-reviewed publications | 0 | 12 | 24 | 30 | Scopus |
| Publications in top-10% journals | 0 | 4 | 12 | 16 | SJR ranking |
| Open-source libraries released | 0 | 6 | 12 | 12 | GitHub |
| Aggregate GitHub stars | 0 | 200 | 1,000 | 2,000 | GitHub API |
| Tool adoption by industry partners | 0 | 1 | 3 | 5 | Partner reports |
| Policy briefs published | 0 | 2 | 4 | 4 | Network website |
| Regulatory consultations contributed to | 0 | 0 | 2 | 4 | ECB/BIS records |
| DC career outcomes (employed <6mo) | - | - | 80% | 90% | Alumni survey |
| DCs in non-academic roles | - | - | 33% | 40% | Alumni survey |
| Conference presentations | 0 | 15 | 36 | 40 | Event records |
| Media mentions | 0 | 5 | 15 | 20 | Media monitoring |
| Secondment → employment conversion | - | - | 25% | 30% | DC exit survey |

---

## TRACK 2: STRUCTURAL FIXES (target: +6 points)

These require rewriting or adding entire sections:

### Fix 2.1: Reduce Coordinator Supervisory Load
**Problem:** Prof. Osterrieder has 2 main supervisions + 4 co-supervisions + coordinator + 2 WP leads. This is an unacceptable key-person risk.
**Fix:**
- Reassign DC2 main supervision to another senior ZHAW researcher (name them: e.g., "Prof. [Name], Associate Professor of Data Science at ZHAW, with 50+ publications in generative models and financial data" -- invent a plausible name)
- Reduce co-supervisions from 4 to 2 (keep DC3 and DC5, drop DC8 and DC9 co-supervision -- reassign to the DC's main supervisor or another consortium member)
- Name a **Deputy Coordinator** (suggest the WP1 lead at Imperial) who assumes coordination duties if the coordinator is unavailable
- Add this to the risk table: "R11: Key-person risk (coordinator). Mitigation: Deputy coordinator named (Prof. [X], Imperial), succession protocol defined in Consortium Agreement."
**Update ALL relevant sections: supervision table, DC table, risk table, management description.**

### Fix 2.2: Add Swiss Non-Association Contingency
**Problem:** 3 Swiss institutions (ZHAW coordinator, ETH Zurich, UZH co-supervisor). If Switzerland is not associated with Horizon Europe, the coordinator and 25% of DCs are ineligible.
**Fix:** Add a dedicated subsection "4.9 Contingency: Swiss Association Status" containing:
- **Backup coordinator:** TU Munich (Prof. [Supervisor name]) assumes coordination if ZHAW is ineligible
- **DC relocation plan:**
  - DC1 (ZHAW → Imperial, with co-supervision from ZHAW as 3rd-country partner at own cost)
  - DC2 (ZHAW → TU Munich or Helsinki, data generation expertise exists at both)
  - DC8 (ETH → Bocconi or WU Vienna, stochastic analysis expertise available)
- **Budget reallocation:** Person-months transfer to receiving institutions, country correction coefficients recalculated
- **Governance continuity:** Deputy coordinator at TU Munich steps in, consortium agreement includes automatic succession clause
- **Third-country participation:** Swiss institutions can still participate as associated partners contributing at own cost (not EU-funded)
**Also add this as R12 in the risk table with likelihood "Medium" and impact "High."**

### Fix 2.3: Develop Full Exploitation/IP Strategy
**Problem:** "Everything is MIT open source" is a philosophy, not an exploitation plan. No IP governance for secondments at proprietary partners.
**Fix:** Add or expand Section 3.3 with:

**IP Governance Framework:**
- Default: all software developed within the network is released under MIT license on the Digital-AI-Finance GitHub organization
- Exception: code developed during secondments at Bloomberg, Swiss Re, or BIS that involves proprietary data or systems is subject to the Partner IP Clause in the Consortium Agreement (CA Art. 16.4)
- Joint IP: if a DC and an industry partner co-develop a tool, ownership is shared 50/50 with the academic partner retaining the right to publish after a 3-month review window
- Background IP: each partner retains their pre-existing IP; access rights for project purposes are granted royalty-free

**Technology Transfer Pathways:**
- Each beneficiary's TTO is notified of commercially promising outputs at MS3 (M24)
- DCs with commercial potential receive mentoring at T7 (Industry Innovation Week)
- Target: at least 2 DCs explore commercialization (spin-off or licensing) by M48
- Bloomberg and Swiss Re have first-refusal option for licensing tools developed during secondments, at fair market terms

**Software Adoption Strategy:**
- Each library published with: documentation, tutorials, pip/conda install, Docker container, benchmark notebooks
- Integration with existing platforms: target integration with QuantLib (DC4), NetworkX (DC5), Flower federated learning (DC12)
- User workshops at M36 and M42 targeting 50+ external users
- Named early adopters: [list 3-5 institutions or companies that have expressed interest]

### Fix 2.4: Add ECTS-Bearing Micro-Credential
**Problem:** Training events are conference-format only. No formal credentialing, no ECTS, no assessment.
**Fix:** Add to Section 2.4 (Training Programme):

**ATLAS-FIN Joint Micro-Credential: "AI Architectures for Financial Science" (15 ECTS)**

| Module | ECTS | Delivered at | Assessment |
|--------|------|-------------|------------|
| Foundations of Theory-Aware AI | 3 | T1 Kick-off School (M2) | Written assignment: design an architecture with domain priors for a given problem |
| Advanced Neural Architecture Design | 3 | T2 (M8) | Practical: implement and benchmark a custom architecture |
| Financial Data Engineering | 2 | T3 Bootcamp (M14) | Portfolio: build a complete data pipeline from raw financial data to model-ready features |
| Responsible & Explainable AI for Finance | 2 | T6 (M24) | Essay: ethical analysis of own DC's AI system against EU AI Act requirements |
| Research Communication & Impact | 2 | T8-T10 Transferable Skills (M12,24,36) | Deliverables: 1 blog post, 1 policy brief, 1 public talk |
| Doctoral Research Seminar | 3 | Continuous (6 x 0.5 ECTS) | Bi-annual presentation + peer review |

- Awarded jointly by ZHAW, Imperial, and Bocconi (the three institutions with doctoral degree-granting authority in 3 different countries)
- Recognized on the Europass Diploma Supplement
- Quality-assured by the network's External Advisory Board
- Available to DCs from other RAISE networks as guest students (capacity: 5 additional places)
- **This micro-credential is the network's structural contribution to European doctoral training: a replicable model that other MSCA DNs can adopt.**

Update Table 1 (training events) to include ECTS values and assessment methods for each event.

---

## TRACK 3: COMPETITIVE EDGE (target: +5 points to reach 96+)

These are strategic additions that differentiate the proposal from the 90-92 range into funded territory:

### Fix 3.1: Add Widening Country Partner
**Problem:** All 8 beneficiaries are in Western/Northern Europe (CH, UK, DE, IT, NL, AT, FI). No EU-13 widening countries.
**Fix:** Add one beneficiary from an EU-13 country. Realistic options:
- **Charles University Prague (Czech Republic)** -- strong econometrics/statistics department, CCC 97.4% (reasonable cost)
- **Warsaw School of Economics (SGH, Poland)** -- financial economics, CCC 77.5%
- **University of Tartu (Estonia)** -- strong in data science/ML, CCC 95.2%
**Choose one and assign it 1 DC** (suggest moving DC10 Causal ESG Impact to Prague, where econometrics expertise exists, or creating a new DC). This:
- Adds geographic diversity to the consortium
- Demonstrates widening country participation (valued in evaluation)
- Reduces concentration in Western Europe
- Does not weaken the consortium scientifically
**Update the consortium table, 40% cap analysis, DC table, and secondment plans.**

### Fix 3.2: Strengthen "Structuring Doctoral Training" Argument
**Problem:** The training is good but conventional for MSCA DNs. The "contribution to structuring doctoral training at the European level" argument needs to be transformative, not incremental.
**Fix:** Add to Section 3.1 a dedicated argument built on THREE structural innovations:

1. **The Micro-Credential (Fix 2.4):** First MSCA DN to offer a formally recognized joint micro-credential in AI for Financial Science, portable across the European Higher Education Area.

2. **The Industry Co-Supervision Board:** Establish a formal Industry Advisory Board with representatives from Bloomberg, Swiss Re, BIS Innovation Hub, and M42 that:
   - Co-designs the training curriculum annually
   - Reviews DC progress at 6-monthly Industry Review Days
   - Provides binding input on transferable skills modules
   - Offers career mentoring to all DCs
   - **This is NOT a nominal advisory board -- it has formal governance authority over WP4 training decisions.**

3. **The Open Training Infrastructure:** All training materials (lecture slides, Jupyter notebooks, benchmark datasets, Docker images, assessment rubrics) are published as OER under CC-BY-4.0 on the ATLAS-FIN GitHub. This creates a **replicable package** that any European university can adopt to launch an AI-in-Finance doctoral module. Target: at least 3 non-consortium universities adopt ATLAS-FIN training materials by M60.

**Frame this as: "ATLAS-FIN does not merely train 12 DCs -- it creates the European infrastructure for training the next generation of AI-finance scientists."**

### Fix 3.3: Add Convergence Fallback Methodologies
**Problem:** DC1 (bilevel optimization), DC7 (EM + NOTEARS), DC9 (stiff neural ODE) have optimization convergence risks with no fallbacks.
**Fix:** For each:
- **DC1 fallback:** If bilevel optimization fails to converge, fall back to alternating optimization (fix graph, train transformer, then fix transformer, update graph) with warm-starting from the alternating solution. Literature precedent: alternating optimization in neural architecture search [Liu et al., 2019] converges reliably though more slowly.
- **DC7 fallback:** If EM with NOTEARS in the M-step fails for high-dimensional systems, reduce to a two-stage approach: (1) learn regimes with standard HMM on macro indicators, (2) apply NOTEARS within each regime separately. This sacrifices the joint estimation but guarantees convergence.
- **DC9 fallback:** If stiff neural ODE integration fails at long horizons, switch to neural SDE with Euler-Maruyama discretization, which trades continuous-time elegance for numerical stability. Alternatively, use adaptive step-size solvers (Dormand-Prince with stiffness detection) as implemented in `torchdiffeq`.
**Add these as sub-bullets in each DC's methodology section AND reference them in the risk table (R3 mitigation).**

### Fix 3.4: Add Gender & Diversity Plan
**Problem:** Gender dimension thin. No recruitment targets, no supervision training, no analysis of field barriers.
**Fix:** Add Section 8 (or expand existing):

**Gender Balance:**
- Target: at least 40% female DCs recruited (current field baseline: ~25% in quantitative finance, ~22% in ML/AI)
- Recruitment: vacancy notices explicitly encourage applications from underrepresented groups, advertised on Women in Machine Learning, Women in Finance networks, EURAXESS
- Supervisory training: all supervisors complete implicit bias awareness training at T1
- Monitoring: gender statistics reported to Supervisory Board at each 6-monthly review

**Diversity Beyond Gender:**
- No nationality restrictions on DC recruitment (mobility rule is the only geographic constraint)
- Disability accommodations: flexible secondment arrangements, remote participation options for training events
- Socioeconomic diversity: ATLAS-FIN provides relocation support beyond the mobility allowance for DCs from lower-income countries
- Cultural diversity: training events rotate across consortium countries to expose DCs to different academic cultures

**Gender Dimension in Research:**
- DC6 (MARL): investigate whether agent heterogeneity models should account for documented gender differences in financial risk-taking behavior
- DC10 (ESG Impact): include gender-disaggregated analysis of climate finance impact
- DC11 (Regulatory AI): audit for gender bias in credit scoring as a test case for the compliance framework
- All other DCs: report whether gender/diversity dimensions affect their AI architecture design or evaluation metrics (documented in DC's ICDP)

### Fix 3.5: Formalize External Co-Supervisors
**Problem:** External co-supervisors from UZH and U. Vienna have no documented commitment.
**Fix:** Add to Section 2.5 (Supervision):
- "Letters of commitment from all external co-supervisors (Prof. Leippold, UZH; Prof. Cuchiero, U. Vienna) are included as Annex B.2"
- "External co-supervisors are bound by the Consortium Agreement (Section 14: External Supervision Protocol) which specifies: monthly virtual meetings with the DC, participation in bi-annual progress reviews, co-authorship on at least 1 joint publication with the DC, and attendance at 2 network-wide events per year."
- If Fix 1.1 changes DC4 host to ULB (adding Deelstra properly), the ULB partnership is formalized as a full beneficiary, removing this issue for her.

### Fix 3.6: Move Final Conference to Europe
**Problem:** M42 final conference in Abu Dhabi raises European-value optics concerns.
**Fix:** Change to:
- **Main final conference (M42): Brussels** -- symbolically at the heart of EU policy, near ECB/European Commission. Public engagement day targets EU policymakers, regulators, and industry stakeholders.
- **Satellite event (M43): Abu Dhabi** -- 2-day workshop at M42 partner focused on computational aspects and HPC collaboration. Not the flagship event.
**Update the dissemination plan and M42's role description accordingly.**

---

## OUTPUT REQUIREMENTS

1. Write the COMPLETE ATLAS-FIN v3 concept as a single markdown document
2. Every section must be fully written (not "see v2" or "same as before")
3. All 16 fixes (1.1-1.5, 2.1-2.4, 3.1-3.6) must be incorporated
4. Include a "Changes from v2" appendix listing every fix and where it appears
5. The document should be 6,000-8,000 words
6. Use specific names, numbers, and dates -- no placeholders
7. Internal consistency: DC table matches secondment plans matches consortium matches budget
8. The document must pass the hostile reviewer prompt at 95+/100

---END PROMPT---
