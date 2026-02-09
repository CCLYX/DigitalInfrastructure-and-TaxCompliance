# Impact Evaluation of Digital Infrastructure on Tax Compliance 

![Status](https://img.shields.io/badge/Status-Completed-success) ![Method](https://img.shields.io/badge/Method-Causal_Inference-blue) ![Tech](https://img.shields.io/badge/Tools-Stata_%7C_Econometrics-red)

## Executive Summary
This project utilizes **Causal Inference techniques (PSM-DID)** to evaluate whether the expansion of mobile financial infrastructure (a proxy for digitalization) effectively drives corporate tax compliance.

[cite_start]Using a quasi-natural experiment in Nigeria (2009-2014) [cite: 10][cite_start], the analysis reveals a **Null Effect** (p=0.970)[cite: 28, 215]. [cite_start]The findings challenge the techno-optimist assumption that "digital tools automatically lead to compliance," suggesting that without enforcement mechanisms, infrastructure alone provides zero ROI for tax authorities[cite: 11, 229].

## Key Data Science Challenges & Solutions
[cite_start]Evaluating policy impact in real-world settings is difficult due to **Selection Bias**: regions with high mobile growth are often economically different from low-growth regions initially[cite: 111].

| Challenge | Solution Implemented |
| :--- | :--- |
| **Non-Random Assignment** | [cite_start]Constructed a quasi-natural experiment using uneven infrastructure rollout[cite: 10]. |
| **Selection Bias** | [cite_start]Applied **Propensity Score Matching (PSM)** (Nearest Neighbor) to create a balanced synthetic control group[cite: 164]. |
| **Confounding Trends** | [cite_start]Combined PSM with **Difference-in-Differences (DID)** to isolate the treatment effect from time-invariant factors[cite: 119]. |
| **Robustness** | [cite_start]Validated results using **Placebo Tests** (on Managerial Experience) and Kernel Matching[cite: 175, 181]. |

## Methodology

### 1. Data Engineering
* [cite_start]**Sources**: Merged firm-level panel data (World Bank Enterprise Surveys) with state-level infrastructure data (EFInA)[cite: 27].
* **Feature Engineering**:
    * [cite_start]Constructed a "Treatment" variable based on the top 30th percentile of mobile growth[cite: 94].
    * [cite_start]Log-transformed skewed features (Sales, Employees) to normalize distribution[cite: 103].

### 2. Causal Model (PSM-DID)
[cite_start]The model estimates the Average Treatment Effect on the Treated (ATT) using the following specification[cite: 133]:

$$TaxCompliance_{it} = \beta_0 + \beta_1 Treat_i + \beta_2 Post_t + \delta (Treat_i \times Post_t) + \Gamma X_{it} + \epsilon_{it}$$

Where $\delta$ captures the causal impact.

### 3. Validation
* [cite_start]**Covariate Balance**: Reduced mean bias from **25.2%** (Unmatched) to **5.1%** (Matched)[cite: 275].
* [cite_start]**Parallel Trends**: Validated via placebo tests showing no significant pre-existing divergence in unrelated outcomes[cite: 186].

## Key Results
Contrary to macroeconomic correlations, micro-level analysis shows **no statistically significant impact**:

* [cite_start]**Coefficient**: -0.249 (Standard Error: 6.533)[cite: 280].
* [cite_start]**P-value**: 0.970[cite: 28].
* [cite_start]**Interpretation**: Digital trails exist but are not utilized due to weak enforcement capacity[cite: 33].

*(Optional: Insert the Balance Table screenshot or the Regression Result Table here)*

## Business/Policy Implications
For stakeholders (e.g., GovTech PMs or Policymakers):
1.  [cite_start]**Technology $\neq$ Adoption**: Infrastructure availability does not guarantee business usage (the "Inertia" problem)[cite: 197].
2.  [cite_start]**Product Strategy**: Launching digital payment tools without integrating them into the regulatory enforcement loop yields minimal compliance returns[cite: 222].

## Repository Structure
```text
├── data/
│   ├── raw/             # Raw World Bank & EFInA datasets
│   └── processed/       # Merged and cleaned panel data
├── src/
│   ├── 01_cleaning.do   # Data cleaning and feature engineering
│   ├── 02_psm.do        # Propensity Score Matching calculation
│   └── 03_analysis.do   # DID regression and robustness checks
├── paper/
│   └── Final_Research_Paper.pdf  # Full academic paper
└── README.md
