# Malaysia Fisheries & Economic Indicators — Time-Series Causality Analysis

[![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Methodology](https://img.shields.io/badge/Methodology-Toda--Yamamoto%20%7C%20VAR%20%7C%20Granger-8A2BE2)](#)

A quarterly time-series analysis of the causal relationships between Malaysia's fish landings and key economic indicators (Fishing GDP, Food CPI, Food Exports) from 2018 Q1 to 2023 Q4 (n = 24), with rigorous controls for the 2020–2021 COVID-19 structural break.

**This is a causality study, not a forecasting exercise.** The goal is to determine whether fish landings lead or lag economic variables in the Granger-causal sense, and to what degree they are related.

---

## Key Findings

### Primary Analysis — Toda-Yamamoto (TY) Granger Causality

The core 3-variable TY test (Landings, Fishing GDP, Food CPI) found **no statistically significant Granger causality** at conventional levels across all 6 directional pairs. This null result is attributed to the limited sample size (n = 24), which constrains statistical power in the multivariate framework.

### Robustness Check — Bivariate Granger Causality

Standard bivariate Granger tests on pre-residualised series revealed suggestive evidence of causality in three directions:

| Direction | F-stat | p-value | Significance |
|:---|:---:|:---:|:---:|
| **Food CPI → Fish Landings** | 11.93 | 0.0025 | ★★★ |
| **Food CPI → Fishing GDP** | 17.83 | 0.0004 | ★★★ |
| **Fish Landings → Fishing GDP** | 4.50 | 0.0467 | ★★ |

These results, while not surviving the stricter TY framework, are consistent with a **demand-pull narrative**: consumer food price inflation is associated with subsequent changes in both landings and sectoral output.

### Cross-Correlation (CCF) Analysis

Significant lead-lag relationships were detected between fish landings and fishing GDP (multiple lags, bidirectional), and between landings and food exports (notably Landings → Food Exports at lag +3: r = −0.852). No significant CCF was found between landings and Food CPI.

---

## Repository Structure

| Notebook | Phase | Content |
|:---|---:|:---|
| `phase1_2_v2.ipynb` | 1–2 | Data preparation, variable construction, and exploratory correlation analysis |
| `phase3_stationarity.ipynb` | 3 | ADF and KPSS stationarity tests; Johansen cointegration test |
| `phase4_ccf_eda.ipynb` | 4 | Cross-correlation functions (CCF), scatter plots, rolling correlations, lead-lag heatmap |
| `phase5_6_regression.ipynb` | 5–6 | Baseline OLS regression with HC3 robust standard errors; residual diagnostics |
| `phase7_v5_3var_ty.ipynb` | 7 | **Core analysis:** VAR lag selection, Toda-Yamamoto Granger causality, bivariate Granger robustness, impulse response functions (IRF) |

---

## Methodology

### Study Design
- **Period:** 2018 Q1 – 2023 Q4 (24 quarterly observations)
- **Frequency:** Quarterly (all monthly sources aggregated via sum or mean)
- **Data transformation:** Natural logarithms (`ln_*`); first differences (`Δln`) for stationarity

### Core Variables
| Variable | Source | Transformation |
|:---|---|:---:|
| Fish Landings (national) | DOSM | `Δln` |
| Fishing Sector GDP | DOSM (p1.4) | `Δln` |
| Food CPI (National, Div 01) | DOSM | `Δln` |
| Food Exports (SITC Section 0) | DOSM | `Δln` |

### Controls
- **COVID-19 structural break dummy** (2020 Q1 – 2021 Q4)
- **Seasonal dummies** (Q2, Q3, Q4; Q1 as baseline)
- **Weather controls** (wind speed, humidity) tested but not included in final models

### Statistical Framework
1. **Stationarity:** ADF + KPSS complementary testing; all variables treated as I(1) with conservative default to first-differencing
2. **Cointegration:** Johansen test (no reliable long-run equilibrium given small sample)
3. **Primary:** Toda-Yamamoto (TY) Granger causality in a 3-variable VAR(p + dₘₐₓ) framework
4. **Robustness:** Bivariate Granger causality on pre-residualised series + IRF analysis

---

## Reproducibility

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels scikit-learn
```

### Running the Analysis
Open notebooks in order (`phase1_2_v2.ipynb` → `phase7_v5_3var_ty.ipynb`) in Jupyter Notebook, JupyterLab, or Google Colab. Notebooks were originally authored in Google Colab and may reference Google Drive mount points — adjust file paths if running locally.

> **Note:** Raw data files (`.csv`) from DOSM are not included in this repository due to licensing. The `master_dataset_analysis.csv` output from Phase 2 is also excluded. To fully reproduce, obtain the original DOSM datasets and run Phase 1–2 to construct the master dataset.

---

## Citation

```bibtex
@misc{nyan2026malaysiafisheries,
  author = {Nyan},
  title  = {Malaysia Fisheries and Economic Indicators: A Time-Series Causality Analysis},
  year   = {2026},
  url    = {https://github.com/nyan-dev/malaysia-fisheries-causality}
}
```

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

*Part of graduate research in Data Science, INTI International University, Malaysia.*
