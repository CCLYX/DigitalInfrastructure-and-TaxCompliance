# Impact Evaluation of Digital Infrastructure on Tax Compliance 

![Status](https://img.shields.io/badge/Status-Completed-success) ![Method](https://img.shields.io/badge/Method-Causal_Inference-blue) ![Tech](https://img.shields.io/badge/Tools-Stata_%7C_Econometrics-red)

## Executive Summary
This project utilizes **Causal Inference techniques (PSM-DID)** to evaluate whether the expansion of mobile financial infrastructure (a proxy for digitalization) effectively drives corporate tax compliance.

Using a quasi-natural experiment in Nigeria (2009-2014), the analysis reveals a **Null Effect** (p=0.970). The findings challenge the techno-optimist assumption that "digital tools automatically lead to compliance," suggesting that without enforcement mechanisms, infrastructure alone provides zero ROI for tax authorities.

## Key Data Science Challenges & Solutions
Evaluating policy impact in real-world settings is difficult due to **Selection Bias**: regions with high mobile growth are often economically different from low-growth regions initially.

| Challenge | Solution Implemented |
| :--- | :--- |
| **Non-Random Assignment** |Constructed a quasi-natural experiment using uneven infrastructure rollout. |
| **Selection Bias** |Applied **Propensity Score Matching (PSM)** (Nearest Neighbor) to create a balanced synthetic control group. |
| **Confounding Trends** |Combined PSM with **Difference-in-Differences (DID)** to isolate the treatment effect from time-invariant factors. |
| **Robustness** |Validated results using **Placebo Tests** (on Managerial Experience) and Kernel Matching. |

## Methodology

### 1. Data Engineering
* **Sources**: Merged firm-level panel data (World Bank Enterprise Surveys) with state-level infrastructure data (EFInA).
* **Feature Engineering**:
    * Constructed a "Treatment" variable based on the top 30th percentile of mobile growth.
    * Log-transformed skewed features (Sales, Employees) to normalize distribution.

### 2. Causal Model (PSM-DID)
The model estimates the Average Treatment Effect on the Treated (ATT) using the following specification:

$$TaxCompliance_{it} = \beta_0 + \beta_1 Treat_i + \beta_2 Post_t + \delta (Treat_i \times Post_t) + \Gamma X_{it} + \epsilon_{it}$$

Where $\delta$ captures the causal impact.

### 3. Validation
* **Covariate Balance**: Reduced mean bias from **25.2%** (Unmatched) to **5.1%** (Matched).
* **Parallel Trends**: Validated via placebo tests showing no significant pre-existing divergence in unrelated outcomes.

## Key Results
Contrary to macroeconomic correlations, micro-level analysis shows **no statistically significant impact**:

* **Coefficient**: -0.249 (Standard Error: 6.533).
* **P-value**: 0.970.
* **Interpretation**: Digital trails exist but are not utilized due to weak enforcement capacity.

*(Optional: Insert the Balance Table screenshot or the Regression Result Table here)*

## Business/Policy Implications
For stakeholders (e.g., GovTech PMs or Policymakers):
1.  **Technology $\neq$ Adoption**: Infrastructure availability does not guarantee business usage (the "Inertia" problem).
2.  **Product Strategy**: Launching digital payment tools without integrating them into the regulatory enforcement loop yields minimal compliance returns.

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
