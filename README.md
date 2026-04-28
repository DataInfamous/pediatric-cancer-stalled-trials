# Where Pediatric Cancer Trials Stall

### A Structural Analysis of Trial Discontinuation in Pediatric Oncology (1995–Present)

A global analysis of pediatric cancer clinical trials examining where trials stall, why they stall, and what these patterns reveal about the structure of the research system.

---

## Overview

This project analyzes stalled pediatric cancer trials using ClinicalTrials.gov registry data to evaluate whether trial failure is driven by:

* Disease-level burden (e.g., survivor harm)
* Structural factors (e.g., funding, coordination)
* Temporal shifts in the research system

The analysis integrates registry data, statistical modeling, and external context to identify patterns in trial discontinuation.

---

## Key Findings

* **954 stalled trials** across 89 countries (1995–present)
* **Stall rates increased sharply in the late 2010s**, indicating a system-wide shift in trial outcomes
* **No meaningful relationship between disease burden and stall rates** after controlling for aggregation and temporal effects
* **Funder structure matters**:

  * NIH and research networks show the lowest stall rates (~10–15%)
  * Industry shows moderate rates (~26%)
  * Heterogeneous funding environments show higher rates (~30–38%)
* **Funding-related trial failure increased significantly in post-2025 cohorts** (logistic regression, p = 0.002)
* **54% of trials lack recorded stop reasons**, reflecting registry limitations
* **Low enrollment/accrual is the most common documented cause**

---

## Core Insight

> Trial discontinuation in pediatric oncology is driven more by system-level factors than by disease-specific burden.

Initial analysis suggested a strong relationship between disease burden and stall rates. However, this relationship disappeared after:

* Disaggregating disease categories into clinically meaningful subtypes
* Controlling for temporal effects
* Removing aggregation bias

This indicates that apparent alignment between research activity and disease burden can emerge as an artifact of coarse grouping.

---

## Regression Analysis

Logistic regression (n = 954) predicting funding-related trial discontinuation:

| Predictor          | Coefficient | p-value | Interpretation                                                                      |
| ------------------ | ----------- | ------- | ----------------------------------------------------------------------------------- |
| Post2025           | 3.202       | 0.002   | Trials starting 2025+ are significantly more likely to cite funding-related reasons |
| NumCountries       | 0.059       | 0.028   | Multi-country trials show slightly higher risk                                      |
| SponsorType_Pharma | 1.055       | 0.005   | Pharma trials more likely to cite funding/business reasons                          |
| SponsorType_Other  | -0.009      | 0.980   | Not significant                                                                     |

**Model**: Logistic regression (MLE), converged
**Pseudo R²**: 0.048
**LLR p-value**: 0.0008

### Interpretation

A strong increase in funding-related trial discontinuation is observed in post-2025 cohorts. This pattern reflects changes in reported failure mechanisms over time and aligns with broader shifts in research funding environments. Registry data alone cannot establish causation.

---

## Methodology

### Data Source

* ClinicalTrials.gov API v2

### Query

```
AREA[ConditionSearch](Neoplasms) AND AREA[StdAge](CHILD)
```

### Stalled Definition

* TERMINATED
* WITHDRAWN
* SUSPENDED
* NO_LONGER_AVAILABLE
* UNKNOWN (analyzed separately)

### Disease Mapping

* Primary: MeSH-based classification
* Secondary: free-text fallback
* Final analysis uses subtype-level categories aligned with CCSS groupings

### Statistical Approach

* Spearman correlation (disease-level analysis)
* Logistic regression (funding-related failure)
* Mann–Whitney and t-tests (temporal comparisons)

---

## Validation

Initial aggregated analysis suggested a strong correlation between disease burden and stall rates (ρ ≈ 0.80).

After disaggregation into subtype-level categories:

* **ρ = 0.18**
* **p = 0.67**

This demonstrates that the initial signal was driven by aggregation effects rather than a true underlying relationship.

See: `ANALYSIS_VALIDATION.md`

---

## Limitations

* Registry data is self-reported and inconsistently maintained
* 54% of trials lack a recorded stop reason
* Funding-related classification is based on keyword extraction from reported reasons
* ClinicalTrials.gov overrepresents high-income countries
* Post-2025 sample size is limited
* Observational data cannot establish causation

---

## Project Structure

```
├── data/
│   ├── stalled_trials_final.csv
│   └── trials_by_country.csv
├── notebooks/
│   └── pediatric_cancer_trial_analysis.ipynb
├── ANALYSIS_VALIDATION.md
└── README.md
```

---

## Future Work

* Integrate direct funding datasets (NIH TAGGS, Grant Watch)
* Expand to WHO ICTRP for global coverage
* Model trial phase and enrollment size as predictors
* Normalize stall rates by total trials per disease
* Re-run analysis with updated post-2025 data

---

## Related Work

This dataset feeds into:

**pediatric-cancer-research-gaps**
Testing whether stalled trial distribution aligns with survivor burden using CCSS mortality data and CDC WONDER incidence rates.

---

## Author

Benjamyn Wilson
DataInfamous
