# Data Notes

## Source

All variables are sourced from the **Department of Statistics Malaysia (DOSM)**.

| Variable | Source | Frequency |
|---|---|---|
| Fish Landings | DOSM — Fisheries Statistics | Quarterly |
| Fishing Sector GDP | DOSM — National Accounts | Quarterly |
| Food CPI | DOSM — Consumer Price Index | Quarterly |
| Food Exports | DOSM — External Trade Statistics | Quarterly |

## Coverage

- **Period:** 2018 Q1 – 2023 Q4
- **Observations:** n = 24 quarterly data points
- **Note:** The small sample size (n = 24) is a known limitation of this study. It constrains statistical power, particularly for multivariate Granger causality tests.

## Data Availability

Raw data files (`.csv`) are **not included** in this repository due to DOSM licensing terms. The `master_dataset_analysis.csv` output from Phase 1–2 is also excluded for the same reason.

To reproduce the analysis:
1. Obtain the relevant datasets from [DOSM](https://www.dosm.gov.my) directly
2. Run `phase1_2_v2.ipynb` to construct the master dataset
3. Proceed with subsequent notebooks in order

## COVID-19 Structural Break

A binary dummy variable is used to control for the 2020–2021 COVID-19 disruption period (2020 Q1 – 2021 Q4). This is included in all regression and VAR models to reduce structural break bias, not to fully remove it.

## Planned Improvements

- Rename notebooks from phase-based to numbered sequence (`01_`, `02_`, etc.) using local `git mv`
- Move notebooks into a `notebooks/` subfolder for cleaner structure
- These changes require local git operations to preserve history
