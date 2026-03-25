# Card-Krueger-DID-Replication

**Course:** ECON 5200: Applied Econometrics

**Environment:** Python (Pandas, Statsmodels)

**Track:** Track A (Difference-in-Differences) 

---
**Bottom Line Up Front (BLUF)**

The minimum wage increase in New Jersey did not lead to a statistically significant decline in employment in the fast-food sector relative to Pennsylvania. Even when examining heterogeneous effects across store types and chains, we find no consistent evidence of negative employment impacts, reinforcing the robustness of the original findings.

---
**Project Overview**

This project replicates and extends the analysis of David Card and Alan Krueger (1994), which investigates the impact of a minimum wage increase on employment in the fast-food industry. The original study compares fast-food restaurants in New Jersey (treatment group) and Pennsylvania (control group) before and after the 1992 policy change.

**Research Question**

Does the increase in minimum wage in New Jersey affect employment in fast-food restaurants, and does this effect vary when accounting for store-level characteristics (heterogeneous treatment effects)?

Using the 1992 New Jersey minimum wage increase as a natural experiment, I compare employment changes in New Jersey (Treatment Group) against Eastern Pennsylvania (Control Group) where the wage remained constant.

---

**Methodology**

Baseline Difference-in-Differences (DID)
The baseline model estimates the causal impact of the policy using a Difference-in-Differences (DID) framework:

Y = β₀ + β₁ treated + β₂ post + β₃ (treated × post) + ε

Where:
* treated = 1 if the store is in New Jersey (treatment group)
* post = 1 for observations after the minimum wage increase
* treated × post (DID) = captures the causal treatment effect
* The dependent variable is full-time equivalent employment (fte):

**fte = EMPFT + 0.5 × EMPPT + NMGRS**

---

**Data**

The dataset contains store-level observations from fast-food restaurants in New Jersey and Pennsylvania. Key variables include:

* Treatment indicators: Treated, Post, DID
* Employment: EMPFT, EMPPT, NMGRS
* Prices: PSODA, PFRY, PENTREE
* Store characteristics: CHAIN, CO_OWNED

---
**Phase 1: Data Preparation**

* Loaded and inspected the raw dataset
* Cleaned variables and handled missing values
* Constructed the fte variable
* Exported cleaned dataset:
```
data/processed/card_krueger_full_cleaned.csv
```
---
**Phase 2: Replication**
1. Descriptive Statistics
Generated summary statistics for all key variables.
2. Difference-in-Means
Compared employment across treatment and control groups before and after the policy.
3. DID Estimation
Estimated the baseline DID model using OLS with robust standard errors.
4. Clustered Standard Errors
Improved inference by clustering standard errors at the store level.
---
**Phase 3: Extension (Heterogeneous Treatment Effects)**

**Extension Strategy**

The standard DID framework assumes homogeneous treatment effects across all stores. However, in reality, the impact of minimum wage policies may differ depending on store characteristics.

This project extends the analysis by incorporating **heterogeneous treatment effects (HTE)** through store-level controls.

**Extended Model**

fte = β₀ + β₁ treated + β₂ post + β₃ did + β₄ controls + ε

**Control Variables**
* CHAIN (restaurant chain differences)
* CO_OWNED (corporate vs franchise ownership)
* NREGS (proxy for store size)
---
**Results**
* The DID coefficient remains positive and statistically insignificant
* No evidence that the minimum wage increase reduced employment
* Results are robust to inclusion of control variables
* Evidence suggests no negative employment effects, even after accounting for heterogeneity across stores
---
**Visualization**

A coefficient plot with 95% confidence intervals was created to clearly communicate the estimated effects:
```
data/processed/extension_coefficient_plot.png
```
---
**Key Findings**

* The minimum wage increase in New Jersey did not reduce employment in fast-food restaurants
* Results are consistent across baseline and extended models
* Accounting for store-level heterogeneity does not change the core conclusion
* Findings support the original conclusions of Card and Krueger (1994)
---
**Repository Structure**
```
Card-Krueger-DID-Replication/
├── DATA/
│   ├── Raw/
│   └── processed/
│       ├── card_krueger_full_cleaned.csv
│       └── extension_coefficient_plot.png
└── notebooks/
    ├── 01_Data_Cleaning.ipynb
    ├── 02_Replication.ipynb
    └── 03_Extension_and_Results.ipynb
└── README.md
```
---
