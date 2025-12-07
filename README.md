# Excess Mortality in Germany (2020–2023) – State‑Level Signal

This repository contains the full, reproducible Python workflow behind an exploratory analysis of **state‑level excess mortality in Germany** during the first three pandemic years, using the public dataset from:

> **Kuhbandner & Reitzner (2025), Royal Society Open Science** > “Regional patterns of excess mortality in Germany during the COVID‑19 pandemic: a state‑level analysis”

The goal is *not* to re‑estimate the baseline mortality, but to ask:

> Given the excess‑mortality series in the RSOS paper, what other variables (vaccination, COVID burden, demographics, etc.) best explain the **change** between Year 2 and Year 3?

---

## Live notebook (MyBinder)

Launch the notebook interactively in your browser (no local setup required):

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/slashennui/german_signal/main?urlpath=%2Fdoc%2Ftree%2Fnotebooks%2Fsignal.ipynb)

---

## Key result (descriptive summary)

Using the RSOS excess‑mortality estimates for the 16 German federal states:

* The **change in excess mortality from Year 2 → Year 3 (ΔEM)** is **strongly, positively associated** with **booster coverage by end of Year 3** (Pearson $r \approx 0.93$, $R^2 \approx 0.87$; Spearman $\rho \approx 0.92$; permutation $p \approx 0.00020$; bootstrap 95% CI roughly $[0.84, 0.97]$).

* High‑booster states started with **lower** excess mortality in Years 1–2 but show **higher** excess mortality by Year 3 than low‑booster states.

* Across a broad panel of candidate predictors (age, GDP per capita, poverty, care needs, policy stringency, COVID deaths/infections, etc.), only booster and 2‑dose coverage remain associated with ΔEM after controlling the false‑positive rate with FDR and Bonferroni corrections.

These results are **descriptive** and **hypothesis‑generating**. They do not establish mechanism or individual‑level risk.

---

## What the analysis does *not* claim

This analysis **does not**:

* Prove that vaccines caused the rise in excess mortality.
* Imply that vaccines had no benefits or did not prevent COVID deaths.
* Rule out important contributions from COVID‑19 itself, health‑system strain, delayed care, heatwaves, influenza, or other factors.
* Determine individual‑level risks or causal pathways.

What it **does** show is narrower:

> Given the variables in this dataset, the **strongest and most consistent statistical alignment** with the late‑pandemic (Year‑3) excess‑mortality jump is found in the **Year‑3 vaccination metrics**, not in the usual alternative predictors.

The mechanism behind this pattern remains unresolved and requires additional work (cause‑of‑death analysis, individual‑level data, cross‑country comparisons, etc.).

---

## Dataset

The analysis uses the publicly released dataset from:

**Kuhbandner & Reitzner (2025)**
* **Data archive (OSF):** [https://osf.io/xg8eu/](https://osf.io/xg8eu/)
* **Paper (Royal Society Open Science):** [https://royalsocietypublishing.org/doi/10.1098/rsos.250790](https://royalsocietypublishing.org/doi/10.1098/rsos.250790)

Dataset included in this repo:
* `data/Data Excess Mortality Germany Federal States Kuhbandner Reitzner RSOS 2025.csv`

**Key variable groups:**
* Observed & expected deaths for Years 1–3
* Excess mortality (%) for Years 1–3
* Vaccination coverage (1st, 2nd, booster / 3rd dose)
* COVID‑19 cases & deaths
* Mean age, care‑needs share
* GDP per capita, poverty rate
* Policy stringency / “measures” indices

---

## Repository contents

* **`data/`**
    * `Data Excess Mortality Germany Federal States Kuhbandner Reitzner RSOS 2025.csv`  
        Original CSV from the RSOS paper (downloaded from OSF).

* **`notebooks/`**
    * `signal.ipynb` – **Main analysis notebook**, used for all figures and tables referenced in the accompanying article.
    * `figures/` – Generated PNGs for all figures and tables (Figures 1–9, Tables A1–A3).
    * `full_results/` – Machine‑readable outputs, e.g., `corr_grid_with_FDR_Bonferroni.csv`, `tables.md`.

* **`signal.py`** – Script version of the notebook for those who prefer running a plain `.py` file.

* **`requirements.txt`** – Python dependencies needed to run the notebook.

---

## How to reproduce locally

1.  **Clone the repo:**
    ```bash
    git clone [https://github.com/slashennui/german_signal.git](https://github.com/slashennui/german_signal.git)
    cd german_signal
    ```

2.  **(Recommended) create and activate a virtual environment.**

3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Open the notebook:**
    ```bash
    jupyter notebook notebooks/signal.ipynb
    ```

5.  **Run all cells from top to bottom.**
    Figures will be written to `notebooks/figures` and key tables to `notebooks/full_results`.

*Note: If the CSV path differs on your machine, edit the `DATA_PATH` cell at the top of `notebooks/signal.ipynb`.*

---

## Methods and robustness checks

All methods live in `notebooks/signal.ipynb`. At a high level, the notebook implements:

### 1. Correlation analysis
* Pearson correlations for a grid of predictor–outcome combinations.
* **False‑discovery‑rate (FDR) corrections:**
    * Benjamini–Hochberg
    * Benjamini–Yekutieli
* **Family‑wise error‑rate corrections:**
    * Holm
    * Bonferroni

### 2. Robustness tests
* **Permutation testing** (5,000 iterations) for the core booster–ΔEM correlation.
* **Leave‑one‑out jackknife analysis** (by state).
* **Spearman rank correlation** as a non‑parametric check.
* **Analytic & bootstrap confidence intervals** for the main correlation.
* **Partial correlations** (booster vs ΔEM, controlling for prior excess mortality in Years 1 and 2).
* **Exploratory multivariate OLS models**, e.g.:
    * `ΔEM (Year 2→3) ~ booster rate + Year‑2 excess mortality + (optional) age, GDP, poverty`
* **East vs West tests:**
    * t‑test on ΔEM for East vs West state groups.
    * OLS including a simple `is_east` indicator.

These multivariate and partial‑correlation results are **exploratory** given the small sample size (N = 16). They are included to show that the booster association is not trivially eliminated by straightforward adjustments, not as final causal models.

### 3. Visualisations
Figures are saved to `notebooks/figures/`, including:
* `core_corr_booster_delta23.png` – Booster vs Δ excess mortality (Year 2→3)
* `trend_reversal_high_low.png` – High‑ vs low‑booster group trends over three years
* `covid_deaths_vs_em_by_year.png` – COVID deaths vs excess mortality by year
* `booster_vs_covid_metrics.png` – Booster vs COVID metrics (Year 3)
* `predictor_outcome_heatmap.png` – Predictor vs outcome correlation heatmap
* `jackknife_correlations.png` – Leave‑one‑out correlation values
* `permutation_histogram.png` – Null distribution of correlations from permutation
* `bootstrap_r_booster_delta23.png` – Bootstrap distribution of the main correlation
* `ols_residuals_vs_fitted.png`, `ols_resid_qq.png` – Regression diagnostics

For a broader conceptual overview of these tools, see the companion **Model Evaluation Metrics Dashboard**:  
[https://slashennui.github.io/tests_and_metrics/](https://slashennui.github.io/tests_and_metrics/)

---

## Requirements

Minimal environment to run `notebooks/signal.ipynb`. See `requirements.txt`:

```bash
ipykernel
ipywidgets==8.1.2
jupyter

numpy==1.26.4
pandas==2.2.2
scipy==1.13.1

matplotlib==3.8.4
seaborn==0.13.2

statsmodels==0.14.2
tabulate==0.9.0

tqdm==4.66.4
```

The notebook footer also prints the exact versions used when it was last run.

---

## Limitations and responsible use

Please read the analysis and any accompanying article with these limitations in mind:

* Small sample size (16 states).
* Ecological fallacy risk (state‑level ≠ individual‑level).
* Dependence on RSOS baseline modelling choices.
* Absence of individual‑level vaccination or health outcome data.
* No time‑to‑event (survival) analysis possible with this dataset.

This repository is offered in the spirit of transparency and replication. Questions or suggestions are welcome:

manu – x34mev@proton.me

