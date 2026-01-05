# 🌍 Economic Impact of COVID-19 Prevention Policies: US vs. China

![R](https://img.shields.io/badge/R-276DC3?style=flat&logo=r&logoColor=white)![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Focus](https://img.shields.io/badge/Focus-Regression%20%26%20Spatial%20Analysis-orange)
![Institution](https://img.shields.io/badge/Institution-UC%20Riverside-green)

> **Capstone Project by Xiaohui Ma** > *Approved by University Honors, University of California, Riverside (Spring 2025)*

---

## 📖 Project Overview
This project investigates how differing quarantine policies (2019-2023) influenced economic stability in two distinct governance systems: the **United States** (decentralized) and **China** (centralized).

Using **Multiple Linear Regression** and **Spatial Autocorrelation Diagnostics**, the study quantifies the relationship between the **Quarantine Policy Index** (from Oxford OxCGRT) and two key economic indicators:
1.  **Unemployment Rate** (Regional analysis for US & China)
2.  **Housing Price Index (HPI)** (US only, with spatial dependency checks)

**[👉 Click here to read the full Capstone Paper](https://escholarship.org/uc/item/9127r4wm)**

---

## 📊 Key Findings & Insights

### 1. 🇺🇸 US Unemployment Model (Adjusted $R^2 = 86.07\%$)
The US economy showed **high sensitivity** to specific policy measures. The final log-linear regression model revealed:
* **Significant Predictors:** Workplace closing, International travel control, and School closing were statistically significant.
* **Interaction Effects:** We found a significant interaction between **School Closing** and **Workplace Closing**.
    * *Insight:* The combined impact of closing both schools and workplaces amplifies unemployment more than the sum of their individual effects (likely due to childcare constraints on the workforce).
* **Non-linear Relationships:** "Stay-at-home requirements" showed a **U-shaped** relationship with unemployment (Quadratic term significant).

### 2. 🇨🇳 China Unemployment Model
In contrast to the US, China's model showed marked resilience to specific policy variables:
* **Policy Resilience:** Only **"Restriction on gathering"** and provincial dummy variables were statistically significant.
* **Interpretation:** The centralized enforcement and uniform policies likely mitigated regional variations in economic disruption compared to the decentralized US approach.

### 3. 🏠 US Housing Price Index (HPI) & Spatial Analysis
* **Policy Impact:** "Restriction on gathering" had a negative coefficient, estimating a **9.23 point decrease** in HPI for every unit increase in strictness.
* **Spatial Diagnostics (Moran's I):**
    * We constructed a **Spatial Weight Matrix** based on state contiguity.
    * **Result:** Moran's I statistic was **0.0053** (p-value > 0.05), indicating **no significant spatial autocorrelation** in the residuals. This validated that the linear regression model sufficiently captured the data structure without needing SAR/CAR spatial models.

---

## 🛠️ Methodology & Statistical Approach

The analysis followed a rigorous statistical framework (detailed in Section 3 of the report):

1.  **Data Preparation:** Aggregated daily OxCGRT policy data to match monthly/yearly economic indicators.
2.  **Variable Selection:**
    * Calculated **VIF (Variance Inflation Factor)** to remove multicollinearity.
    * Stepwise selection for interaction and quadratic terms.
3.  **Model Diagnostics:**
    * Checked Homoscedasticity, Normality (Shapiro-Wilk), and Independence (Durbin-Watson).
    * Applied **Log-transformation** to the US Unemployment rate to satisfy variance assumptions.
4.  **Spatial Analysis:**
    * Used `spdep` package in R to calculate **Moran’s I** for HPI residuals to detect geographic clustering.

---

## 📂 Repository Structure

```text
├── data/
│   ├── us_unemployment_combine.csv  # US Unemployment & Policy Data
│   ├── us_hpi_combine.csv           # US Housing Price Index Data
│   └── china_unemployment.csv       # China Regional Data
├── code/
│   ├── 01_us_unemployment_model.R   # Regression, VIF, & Interaction plots (Appendix A)
│   ├── 02_china_unemployment_model.R# Comparative analysis code
│   └── 03_us_hpi_spatial_analysis.R # Spatial weights & Moran's I test (Appendix B)
├── visuals/                         # Figures export (Scatter plots, Maps)
├── Xiaohui Ma - Final Written Capstone.pdf  # Full Report
└── README.md
