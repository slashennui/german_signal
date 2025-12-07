# Key tables

## High vs low booster states – excess mortality by year

| group        |   EM_Year1 |   EM_Year2 |   EM_Year3 |
|:-------------|-----------:|-----------:|-----------:|
| high_booster |   0.361081 |    1.42955 |    8.67285 |
| low_booster  |   4.61798  |    4.62912 |    7.17785 |



## Core booster vs ΔEM correlation

| predictor       | outcome           |     r |    R2 |   CI_low |   CI_high |   N_states |   perm_p |
|:----------------|:------------------|------:|------:|---------:|----------:|-----------:|---------:|
| Booster rate Y3 | ΔEM (Year2→Year3) | 0.932 | 0.868 |     0.81 |     0.976 |         16 |   0.0002 |



## Predictors vs ΔEM (Year2→Year3) with FDR / Bonferroni

| predictor            |      r |   p_raw |   p_fdr |   p_bonf | sig_fdr   | sig_bonf   |
|:---------------------|-------:|--------:|--------:|---------:|:----------|:-----------|
| Booster rate Y3      |  0.932 |   0     |   0     |    0     | ✓         | ✓          |
| 2-dose rate Y3       |  0.795 |   0     |   0.002 |    0.008 | ✓         | ✓          |
| Mean age             | -0.487 |   0.056 |   0.167 |    1     |           |            |
| Care needs %         | -0.393 |   0.132 |   0.358 |    1     |           |            |
| Poverty rate         |  0.386 |   0.139 |   0.358 |    1     |           |            |
| GDP per capita       |  0.328 |   0.215 |   0.476 |    1     |           |            |
| COVID infections Y3  |  0.248 |   0.355 |   0.64  |    1     |           |            |
| COVID deaths Y3      |  0.151 |   0.578 |   0.832 |    1     |           |            |
| Policy stringency Y3 | -0.006 |   0.981 |   0.981 |    1     |           |            |

