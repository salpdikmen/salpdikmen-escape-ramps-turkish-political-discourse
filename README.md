# Escape Ramps: Crisis, Nostalgia, and Parliamentary Rhetoric
### A Computational Analysis of Turkish Political Discourse (2011–2022)

> **MSc Thesis** · Politics and Data Science · University College Dublin · 2.1 Honours  
> Sadullah Alp Dikmen

---

## Overview

This project investigates whether Turkey's Justice and Development Party (AKP) strategically increases nostalgic rhetoric in parliamentary speeches during periods of economic hardship — and whether that response is *delayed*, suggesting deliberate political strategy rather than spontaneous emotional reaction.

Using **29,860 AKP parliamentary speeches** from the Turkish Grand National Assembly (2011–2022), the study applies computational text analysis to detect nostalgic discourse and correlate it with macroeconomic indicators including inflation, unemployment, and currency depreciation.

**Key finding:** Nostalgic discourse peaks 6–12 months *after* economic shocks — consistent with nostalgia functioning as a deliberate "concealment mechanism" to redirect public attention from policy failures.

---

## Research Questions

1. Does the AKP's nostalgic rhetoric increase during economic downturns?
2. Did a structural shift in nostalgic discourse occur following Turkey's 2017 constitutional referendum?

Both hypotheses were confirmed empirically.

---

## Methods & Technical Stack

| Component | Tools / Approach |
|---|---|
| **Data source** | ParlaMint-TR corpus (CLARIN ERIC) — standardised XML parliamentary data |
| **Language preprocessing** | Zemberek NLP (Turkish lemmatisation, 94.3% success rate) |
| **Text analysis** | R + Quanteda (document-feature matrix, dictionary-based scoring) |
| **Nostalgia detection** | Custom-built nostalgia dictionary (iterative refinement: 283 → 76 → 26 collocations) |
| **Validation** | Manual coding of 1,500 stratified sentences (500 per dictionary × 3 versions) — **87.6% accuracy, F1: 87.7%** |
| **Statistical models** | Correlation analysis, lag regression (0–4 quarters), structural break testing, VIF diagnostics |
| **Economic data** | TÜİK (inflation, unemployment) + CBRT (CPI, exchange rate, consumer confidence) |

---

## Key Results

### Dictionary Performance
| Dictionary | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|
| Strong (26 collocations) | **87.6%** | **88.4%** | **87.0%** | **87.7%** |
| Medium (76 collocations) | 72.1% | 71.3% | 72.9% | 69.0% |
| Weak (283 collocations) | 72.9% | 55.7% | 85.0% | 52.8% |

> Validation: 1,500 manually coded sentences total (500 stratified sentences per dictionary version), with balanced nostalgic/non-nostalgic sampling.

### Economic Indicators vs. Nostalgic Discourse
- **Inflation** (lag 4, ~12 months): β = 0.032, p < 0.001, R² = 42.2%
- **Unemployment** (lag 2–4): significant across multiple periods
- **Consumer Confidence Index**: r = –0.50 (stronger negative correlation post-2017)
- **TRY/USD Exchange Rate**: r = 0.46, optimal lag at 3 months

### 2017 Structural Break
- Post-2017 dummy: β = 6.838, **p = 0.015**
- R² increased from 27.1% → 41.2% after including the 2017 breakpoint
- Consumer confidence interaction post-2017: β = –0.061, p = 0.018

---

## Theoretical Contribution

The findings empirically support Müller & Proksch's (2024) concept of nostalgia as a **"concealment mechanism"** — the 12-month lag between economic shock and peak nostalgic discourse suggests deliberate, strategically timed political communication rather than spontaneous emotional response.

This is the first large-scale quantitative study to examine the economic crisis–nostalgia relationship in Turkish parliamentary discourse, shifting focus from leader-centric analyses to institutional party rhetoric.

---

## Repository Structure

```
├── data/
│   ├── raw/                  # ParlaMint-TR corpus extracts
│   ├── processed/            # Lemmatised & cleaned speeches
│   └── economic/             # TÜİK + CBRT quarterly indicators
├── dictionaries/
│   ├── strong_dict.csv       # Final 26-collocation nostalgia dictionary
│   ├── medium_dict.csv       # 76-collocation version
│   └── weak_dict.csv         # 283-collocation version
├── notebooks/
│   ├── 01_preprocessing.R    # Lemmatisation + cleaning pipeline
│   ├── 02_dictionary_dev.R   # Collocation extraction + validation
│   ├── 03_scoring.R          # Nostalgia score calculation
│   └── 04_analysis.R         # Regression, lag models, structural break
├── validation/
│   └── validation_500.csv    # 500 manually coded sentences + guidelines
├── outputs/
│   └── figures/              # All charts and visualisations
└── README.md
```

---

## Reproducing the Analysis

### Prerequisites
```r
# R packages
install.packages(c("quanteda", "quanteda.textstats", "ggplot2", 
                   "dplyr", "stringr", "lubridate", "readxl", "writexl"))
```

```bash
# Python (for Zemberek lemmatisation preprocessing)
pip install zemberek-python
```

### Run Order
```bash
# 1. Preprocess and lemmatise
Rscript notebooks/01_preprocessing.R

# 2. Build and validate dictionary
Rscript notebooks/02_dictionary_dev.R

# 3. Calculate nostalgia scores
Rscript notebooks/03_scoring.R

# 4. Run statistical models
Rscript notebooks/04_analysis.R
```

---

## AI-Assisted Workflow

This project incorporated **Claude (Anthropic)** as a research and development tool throughout the analysis pipeline:

- **Validation assistance:** Supporting iterative refinement of coding guidelines and edge case resolution during the 1,500-sentence manual validation process
- **Dictionary development:** Assisting in conceptual disambiguation between nostalgic, nationalist, and Islamist rhetoric categories
- **Code review:** R and Python script debugging and optimisation
- **Research writing:** Structuring arguments and reviewing analytical framing

> Proficiency in prompt engineering and AI-assisted research workflows is increasingly central to modern data science practice — this project reflects that approach.

---

- **Parliamentary speeches:** [ParlaMint 5.0](https://www.clarin.si/repository/xmlui/handle/11356/2004) — Erjavec et al. (2025)
- **Inflation / Unemployment:** [TÜİK](https://www.tuik.gov.tr)
- **Exchange rates / Consumer Confidence:** [CBRT EVDS](https://evds2.tcmb.gov.tr)

---

## Citation

```bibtex
@mastersthesis{dikmen2025escape,
  author  = {Sadullah Alp Dikmen},
  title   = {Escape Ramps: Crisis, Nostalgia, and Parliamentary Rhetoric —
             A Computational Analysis of Turkish Political Discourse},
  school  = {University College Dublin},
  year    = {2025},
  month   = {August}
}
```

---

## Contact

**Alp Dikmen**  
[LinkedIn](https://www.linkedin.com/in/alp-dikmen-428b54156/) · alpdikmen007@gmail.com  
Dublin, Ireland

---

*Built with R · Quanteda · Zemberek NLP · Python*
