# A Signal – Excess Mortality Analysis for Germany (2020–2023)

**Notebook, figures, and data for the analysis published in _A Signal_.**  

- **Notebook:** `notebooks/signal.ipynb`  
- **Article:** _A Signal_ on fool_me_once Substack – https://substack.com/@memanu/posts  
- **Repo:** https://github.com/slashennui/german_signal  

---

## Overview

This repository contains the full Python workflow, dataset, and generated figures for an exploratory analysis of **state‑level excess mortality in Germany** across the first three pandemic years:

- **Year 1:** Apr 2020 → Mar 2021  
- **Year 2:** Apr 2021 → Mar 2022  
- **Year 3:** Apr 2022 → Mar 2023  

The analysis revisits the state‑level dataset released by **Kuhbandner & Reitzner (2025)** and examines how excess mortality relates to:

- vaccination metrics (first, second, and booster doses)
- recorded COVID‑19 deaths and cases
- demographic factors (age structure, care‑needs share)
- socio‑economic indicators (GDP per capita, poverty rate)
- policy stringency / “measures” indices

All computations are fully reproducible via the supplied notebook and dataset.

---

## Key Result (Summary)

Across ~25 predictors and 5 mortality outcomes (~125 correlations in total), one pattern consistently survives stringent robustness checks:

> **States with higher booster uptake experienced larger increases in excess mortality from Year 2 to Year 3.**

In the main analysis (N = 16 federal states):

- Pearson correlation: **r ≈ 0.93**, **R² ≈ 0.87**
- Analytic 95% CI for r (Fisher z): roughly **[0.81, 0.98]**
- Bootstrap 95% CI: similarly strongly positive
- Spearman rank correlation: **ρ ≈ 0.94**
- Permutation test (5,000 random shuffles): **p ≈ 2×10⁻⁴**
- Jackknife (leave‑one‑state‑out) correlations: **≈ 0.92–0.95**

Other commonly proposed explanations—COVID‑19 deaths, infections, age structure, GDP per capita, poverty rate, simple East/West history—show only **weak and statistically non‑significant** alignment with the Year‑3 excess‑mortality increase once multiple‑testing corrections are applied.

> **Important:** This is an **ecological analysis** using **state‑level aggregates**.  
> It **does not establish individual‑level causality**, nor does it provide a vaccine benefit–risk calculation.  
> The signal is hypothesis‑generating, not a mechanistic conclusion.

---

## What the Analysis Does *Not* Claim

This analysis **does not**:

- prove that vaccines caused the rise in excess mortality,
- imply that vaccines had no benefits or did not prevent COVID deaths,
- rule out important contributions from COVID‑19 itself, health‑system strain, delayed care, heatwaves, influenza, or other factors,
- determine individual‑level risks or causal pathways.

What it **does** show is narrower:

> Given the variables in this dataset, the **strongest and most consistent statistical alignment** with the late‑pandemic (Year‑3) excess‑mortality jump is found in the **Year‑3 vaccination metrics**, not in the usual alternative predictors.

The mechanism behind this pattern remains unresolved and requires additional work (cause‑of‑death analysis, individual‑level data, cross‑country comparisons, etc.).

---

## Dataset

The analysis uses the publicly released dataset from:

**Kuhbandner & Reitzner (2025)**  
- Data archive (OSF): https://osf.io/xg8eu/  
- Paper (Royal Society Open Science): https://royalsocietypublishing.org/doi/10.1098/rsos.250790  

Dataset included in this repo:

- `data/Data Excess Mortality Germany Federal States Kuhbandner Reitzner RSOS 2025.csv`

Key variable groups:

- observed & expected deaths for Years 1–3
- excess mortality (%) for Years 1–3
- vaccination coverage (1st, 2nd, booster / 3rd dose)
- COVID‑19 cases & deaths
- mean age, care‑needs share
- GDP per capita, poverty rate
- policy stringency / “measures” indices

---

## Methods

All methods live in `notebooks/signal.ipynb`. At a high level:

### 1. Correlation analysis

- Pearson correlations for ~125 predictor–outcome combinations  
- False‑discovery‑rate (FDR) corrections:
  - Benjamini–Hochberg  
  - Benjamini–Yekutieli  
- Family‑wise error‑rate corrections:
  - Holm  
  - Bonferroni  

### 2. Robustness tests

- **Permutation testing** (5,000 iterations) for the core booster–Δ excess‑mortality correlation  
- **Leave‑one‑out jackknife analysis** to test sensitivity to any single state  
- **Spearman rank correlation** as a non‑parametric check  
- **Analytic & bootstrap confidence intervals** for the main correlation  
- **Partial correlations** (booster vs Δ excess mortality, controlling for prior excess mortality in Years 1 and 2)  
- **Exploratory multivariate OLS models**, e.g.:  
  - Δ excess mortality (Year 2→3) ~ booster rate + Year‑2 excess mortality + (optional) age, GDP, poverty  
- **East vs West tests**:
  - t‑test on Δ excess mortality for East vs West state groups  
  - OLS including a simple `is_east` indicator  

These multivariate and partial‑correlation results are **exploratory only** given the small sample size (N = 16). They are included to show that the booster association is not trivially eliminated by straightforward adjustments, not as final causal models.

### 3. Visualizations

Figures are saved to:

```text
notebooks/figures_germany_em_analysis/
notebooks/figures_germany_em_analysis_v2/
````

Including, among others:

* `core_corr_booster_delta23.png` – booster vs Δ excess mortality (Year 2→3)
* `trend_reversal_high_low.png` – high‑ vs low‑booster group trends over three years
* `covid_deaths_vs_em_by_year.png` – COVID deaths vs excess mortality by year
* `booster_vs_covid_metrics.png` – booster vs COVID metrics (Year 3)
* `predictor_outcome_heatmap.png` – predictor vs outcome correlation heatmap
* `jackknife_correlations.png` – leave‑one‑out correlation values
* `permutation_histogram.png` – null distribution of correlations from permutation
* `bootstrap_r_booster_delta23.png` – bootstrap distribution of the main correlation
* `ols_residuals_vs_fitted.png`, `ols_resid_qq.png`, `ols_leverage_vs_cooks.png` – regression diagnostics

For a non‑technical explanation of these plots, see the **“How to interpret the figures (for non‑technical readers)”** section in the article / accompanying document.

---

## Notebook & Outputs

Main analysis notebook:

* `notebooks/signal.ipynb`

The notebook covers:

* data loading & cleaning,
* correlation matrix generation,
* multiple‑testing correction tables,
* jackknife & permutation procedures,
* robustness checks (Spearman, bootstrap CIs, partial correlations, OLS, East/West tests),
* exporting:

  * all figures,
  * a CSV of the full correlation grid with FDR/Bonferroni, and
  * Substack‑ready markdown tables.

Key outputs include:

* Figures in `notebooks/figures_germany_em_analysis/` and `notebooks/figures_germany_em_analysis_v2/`
* Correlation grid CSV:

  * `notebooks/figures_germany_em_analysis_v2/corr_grid_with_FDR_Bonferroni.csv`
* Markdown tables for the article:

  * `notebooks/figures_germany_em_analysis_v2/substack_tables.md`

The full workflow runs from raw CSV → cleaned data → statistics → figures and tables.

---

## Requirements & How to Run

Install dependencies (recommended):

```bash
pip install -r requirements.txt
```

Then:

```bash
jupyter notebook notebooks/signal.ipynb
```

or run inside GitHub Codespaces using the provided devcontainer setup.

To reproduce all results, simply run the notebook top‑to‑bottom; all figures and tables will be regenerated in the corresponding output folders.

---

## Reproducibility

This repository provides:

* the full state‑level dataset used in the analysis,
* the complete Jupyter notebook (`notebooks/signal.ipynb`),
* all generated figures and core CSV tables,
* the Substack article link and supporting prose,
* an environment file (`requirements.txt`) for installing dependencies.

The intent is that any interested reader can:

1. download or clone the repo,
2. run the notebook, and
3. confirm or critique every step of the analysis.

---

## Limitations

Some key limitations of this work:

* Only **16 German states** → small sample (wide uncertainty; exploratory only).
* **Ecological design** → analysis uses aggregates, so ecological fallacy is a risk.
* Potential **unmeasured confounders** (e.g. health‑system capacity, specific treatment protocols, weather, detailed comorbidities, etc.).
* Cause‑of‑death labels (e.g. “COVID death”) appear unstable by Year 3, which is why the focus is on **all‑cause excess mortality** rather than specific labels.
* Yearly aggregates cannot resolve detailed temporal patterns (e.g. weekly lags between vaccination waves, COVID waves, and mortality spikes).

These results highlight a **statistical signal**, not a final explanation. They are intended to motivate further, more granular research rather than to close the question.

---

## Conclusion

German state‑level data show a **clear, consistent pattern** within this dataset:

> States with higher booster uptake experienced **larger Year‑3 excess‑mortality increases**, and this signal survives multiple robustness checks.

The mechanism behind this pattern is unknown. This repository is meant to support:

* transparent cause‑of‑death investigations,
* individual‑level longitudinal studies,
* cross‑country comparisons, and
* open, reproducible data pipelines.

The aim is **honest, transparent, quantitative exploration** of a complex and sensitive public‑health dataset—not to provide the last word, but to make the evidence and code easy to inspect, reuse, and challenge.

---

## Contact

* Email: `x34mev@proton.me`
* GitHub: [https://github.com/slashennui](https://github.com/slashennui)


