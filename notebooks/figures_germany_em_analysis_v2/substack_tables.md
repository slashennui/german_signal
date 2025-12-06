# Key tables for Substack

## High vs low booster states – excess mortality by year

| group        |   EM_Year1 |   EM_Year2 |   EM_Year3 |
|:-------------|-----------:|-----------:|-----------:|
| High booster |   0.361081 |    1.42955 |    8.67285 |
| Low booster  |   4.61798  |    4.62912 |    7.17785 |



## Core correlation: booster rate vs ΔEM (Year2→Year3)

| predictor       | outcome           |     r |    R2 |   CI_low |   CI_high |   N_states |   perm_p |
|:----------------|:------------------|------:|------:|---------:|----------:|-----------:|---------:|
| Booster rate Y3 | ΔEM (Year2→Year3) | 0.932 | 0.868 |     0.81 |     0.976 |         16 |   0.0002 |



## Predictors vs ΔEM (Year2→Year3) with FDR & Bonferroni

| predictor                                   |           r |       p_raw |       p_fdr |      p_bonf | sig_fdr   | sig_bonf   |
|:--------------------------------------------|------------:|------------:|------------:|------------:|:----------|:-----------|
| Third_Vaccination_Rate_End_Pandemic_Year_3  |  0.931651   | 1.55763e-07 | 5.60747e-06 | 5.60747e-06 | True      | True       |
| Second_Vaccination_Rate_End_Pandemic_Year_3 |  0.794929   | 0.000233209 | 0.00209888  | 0.00839551  | True      | True       |
| Mean_Age_2022                               | -0.487236   | 0.0555892   | 0.166768    | 1           | False     | False      |
| Care_Needs_Percent_31.12.2021               | -0.393007   | 0.132099    | 0.358464    | 1           | False     | False      |
| Risk_of_poverty_rate_2022                   |  0.386318   | 0.139403    | 0.358464    | 1           | False     | False      |
| GDP_per_capita_2022                         |  0.327716   | 0.215308    | 0.47615     | 1           | False     | False      |
| COVID_infections_Pandemic_Year3             |  0.247523   | 0.355344    | 0.639619    | 1           | False     | False      |
| COVID_deaths_Pandemic_Year3                 |  0.150584   | 0.577757    | 0.831969    | 1           | False     | False      |
| Measures_Overall_Pandemic_Year3             | -0.00636975 | 0.981321    | 0.981321    | 1           | False     | False      |

