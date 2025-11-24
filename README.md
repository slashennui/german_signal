# **A Signal – Excess Mortality Analysis for Germany (2020–2023)**

**Notebook, figures, and data for the analysis published in *A Signal***
**Notebook:** `notebooks/signal.ipynb`
**Article: *A Signal* on fool_me_once Substack**
[https://substack.com/@memanu/posts](https://substack.com/@memanu/posts)
**Repo:** [https://github.com/slashennui/german_signal](https://github.com/slashennui/german_signal)

---

## **Overview**

This repository contains the full Python workflow, dataset, and generated figures for an exploratory analysis of **state-level excess mortality in Germany** across the first three pandemic years:

* **Year 1:** Apr 2020 → Mar 2021
* **Year 2:** Apr 2021 → Mar 2022
* **Year 3:** Apr 2022 → Mar 2023

The analysis revisits the state-level dataset released by **Kuhbandner & Reitzner (2025)** and examines correlations between excess mortality and:

* vaccination metrics (first, second, and booster doses)
* COVID-19 deaths and cases
* demographic factors
* socio-economic indicators
* policy stringency and trust indices

All computations are fully reproducible via the supplied notebook and dataset.

---

## **Key Result (Summary)**

Across ~25 predictors and 5 mortality outcomes (~125 correlations total), one pattern consistently survived stringent robustness checks:

> **States with higher booster uptake experienced larger increases in excess mortality from Year 2 to Year 3.**

This association was:

* **very strong:** Pearson r ≈ **0.93**, R² ≈ **0.87**
* **statistically robust:** permutation p ≈ **2×10⁻⁴**
* **not driven by any single state:** jackknife correlations ≈ **0.92–0.95**

Other commonly proposed explanations—COVID-19 deaths, infections, age structure, GDP per capita, poverty rate, or East/West history—showed only **weak and statistically non-significant** alignment with the Year-3 excess-mortality increase once multiple-testing corrections were applied.

**Important:**
This is an **ecological analysis** using **state-level aggregates**. It **does not establish individual-level causality**, nor does it quantify vaccine benefit–risk.
The signal is hypothesis-generating, not a mechanistic conclusion.

---

## **What the Analysis Does *Not* Claim**

The analysis:

* **does not** prove vaccines caused the rise in excess mortality
* **does not** imply vaccines had no benefits
* **does not** rule out contributions from COVID itself, delayed care, heatwaves, influenza, or health-system factors
* **cannot** determine individual-level risks or causal pathways

What it **does** show:
Given the available variables, the **strongest and most consistent statistical alignment** with the Year-3 excess-mortality jump is found in the **Year-3 vaccination metrics**, not in the usual alternative predictors.

---

## **Dataset**

The analysis uses the publicly released dataset from:

**Kuhbandner & Reitzner (2025)**
Data archive: [https://osf.io/xg8eu/](https://osf.io/xg8eu/)
Paper: [https://royalsocietypublishing.org/doi/10.1098/rsos.250790](https://royalsocietypublishing.org/doi/10.1098/rsos.250790)

Dataset included in this repo:
`data/Data Excess Mortality Germany Federal States Kubhandner Reitzner RSOS 2025.csv`

Variables include:

* observed & expected deaths
* excess mortality (%) for Years 1–3
* vaccination coverage (1st, 2nd, booster)
* COVID-19 cases & deaths
* mean age, care-needs share
* GDP per capita, poverty rate
* policy strictness indices

---

## **Methods**

### **1. Correlation analysis**

* Pearson correlations for ~125 predictor–outcome combinations
* FDR corrections (Benjamini–Hochberg, Benjamini–Yekutieli)
* Holm & Bonferroni family-wise corrections

### **2. Robustness tests**

* **Permutation testing (5000 iterations)**
* **Leave-one-out jackknife analysis**

### **3. Visualizations**

Figures are saved to:

```
notebooks/figures_germany_em_analysis/
notebooks/figures_germany_em_analysis_v2/
```

Includes:

* Booster vs Δ excess mortality
* High- vs low-booster group trends
* Heatmaps of the correlation matrix
* Jackknife sensitivity plots
* Permutation distributions
* COVID outcomes vs booster rate
* Multi-year excess-mortality scatterplots

---

## **Notebook**

Main analysis notebook:
`notebooks/signal.ipynb`

Includes:

* data loading & cleaning
* correlation matrix generation
* multiple-testing correction tables
* jackknife & permutation procedures
* all figures & outputs

The full workflow runs from raw CSV → results → figures.

---

## **Requirements**

Install dependencies:

```bash
pip install -r requirements.txt
```

Or run directly in GitHub Codespaces.

---

## **Reproducibility**

This repository provides:

- full dataset
- full analysis notebook
- all generated figures
- Substack article link
- environment file (`requirements.txt`)

To reproduce all results:

```bash
notebooks/signal.ipynb
```

---

## **Limitations**

* Only 16 German states → exploratory correlations
* Ecological fallacy risk
* Potential unmeasured confounders
* Cause-of-death labels for 2023 appear unreliable
* Yearly aggregates cannot resolve temporal sequencing

These results highlight a **statistical signal**, not a final explanation.

---

## **Conclusion**

German state-level data show a **clear, consistent pattern**:

> States with higher booster uptake experienced **larger Year-3 excess-mortality increases**, surviving multiple robustness checks.

The mechanism remains unknown.
This analysis motivates:

* further transparent cause-of-death investigation
* individual-level longitudinal work
* cross-country comparisons
* open, reproducible data pipelines

The purpose of this repository is to support **honest, transparent, quantitative exploration** of a complex and sensitive public-health dataset.

---

## **Contact**

For questions or collaboration:

**data stuff**
`x34mev@proton.me`
GitHub: [https://github.com/slashennui](https://github.com/slashennui)