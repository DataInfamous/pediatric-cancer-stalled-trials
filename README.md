# Where Pediatric Cancer Trials Stall

### A Structural Analysis of Trial Discontinuation in Pediatric Oncology (1995–Present)

A global analysis of pediatric-eligible cancer trials examining where trials stall, why they stall, and what these patterns reveal about the structure of the research system.

-----

## Overview

This project analyzes pediatric-eligible cancer trials using ClinicalTrials.gov registry data to evaluate whether trial failure is driven by:

- Disease-level burden (e.g., survivor harm)
- Structural factors (e.g., funding, coordination)
- Temporal shifts in the research system

The analysis integrates registry data, statistical modeling, and external context to identify patterns in trial discontinuation.

-----

## Key Findings

- **954 stalled trials** across 89 countries (1995–present)
- **Stall rates increased sharply in the late 2010s**, indicating a system-wide shift in trial outcomes
- **No meaningful relationship between disease burden and stall rates** after controlling for aggregation and temporal effects
- **Funder structure matters**:
  - NIH and research networks show the lowest stall rates (~10–15%)
  - Industry shows moderate rates (~26%)
  - Heterogeneous funding environments show higher rates (~30–38%)
- **Funding-related trial failure increased significantly in post-2025 cohorts** (logistic regression, p = 0.002)
- **54% of trials lack recorded stop reasons**, reflecting registry limitations
- **Low enrollment/accrual is the most common documented cause**

-----

## Core Insight

> Trial discontinuation in pediatric oncology is driven more by system-level factors than by disease-specific burden.

Initial analysis suggested a strong relationship between disease burden and stall rates. However, this relationship disappeared after disaggregating disease categories into clinically meaningful subtypes. The initial signal was an artifact of coarse grouping, not a true underlying relationship.

-----

## Regression Analysis

Logistic regression (n = 954) predicting funding-related trial discontinuation:

|Predictor         |Coefficient|p-value|Interpretation                                                                     |
|------------------|-----------|-------|-----------------------------------------------------------------------------------|
|Post2025          |3.202      |0.002  |Trials starting 2025+ are significantly more likely to cite funding-related reasons|
|NumCountries      |0.059      |0.028  |Multi-country trials show slightly higher risk                                     |
|SponsorType_Pharma|1.055      |0.005  |Pharma trials more likely to cite funding/business reasons                         |
|SponsorType_Other |-0.009     |0.980  |Not significant                                                                    |

**Model**: Logistic regression (MLE), converged  
**Pseudo R²**: 0.048  
**LLR p-value**: 0.0008

### Interpretation

A strong increase in funding-related trial discontinuation is observed in post-2025 cohorts. This pattern reflects changes in reported failure mechanisms over time and aligns with broader shifts in research funding environments. Registry data alone cannot establish causation.

-----

## Methodology

### Data Source

- ClinicalTrials.gov API v2

### Query

```
AREA[ConditionSearch](Neoplasms) AND AREA[StdAge](CHILD)
```

### Age Scope

Age filtering is based on ClinicalTrials.gov `StdAges` categories rather than numeric age limits. Trials were included if their eligibility categories included `CHILD`, meaning the dataset reflects pediatric-eligible trials rather than strictly pediatric-only trials. This includes trials enrolling both children and adults. Sensitivity analyses stratifying by `CHILD` versus `CHILD, ADULT` eligibility are reported separately.

### Stalled Definition

- TERMINATED
- WITHDRAWN
- SUSPENDED
- NO_LONGER_AVAILABLE
- UNKNOWN (analyzed separately)

### Disease Mapping

- Primary: keyword-based classification against named pediatric oncology subtypes
- Final analysis uses subtype-level categories aligned with CCSS groupings
- 75% of trials mapped to “other” and were excluded from disease-level correlation analysis

### Statistical Approach

- Spearman correlation (disease-level analysis)
- Logistic regression (funding-related failure)
- Mann–Whitney and t-tests (temporal comparisons)

-----

## Validation

Initial aggregated analysis suggested a strong correlation between disease burden and stall rates (ρ ≈ 0.80). After disaggregation into clinically meaningful subtypes aligned with CCSS groupings:

- **ρ = 0.18**
- **p = 0.67**

This demonstrates that the initial signal was driven by aggregation bias — broad disease groupings masked the absence of a true underlying relationship.

See: `ANALYSIS_VALIDATION.md`

-----

## Limitations

- Age filtering is based on eligibility categories, not numeric age limits — the dataset reflects pediatric-eligible trials, not pediatric-only trials
- Registry data is self-reported and inconsistently maintained
- 54% of trials lack a recorded stop reason
- Funding-related classification is based on keyword extraction from reported reasons
- ClinicalTrials.gov overrepresents high-income countries
- Post-2025 sample size is limited
- Observational data cannot establish causation

-----

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

-----

## Future Work

- Integrate direct funding datasets (NIH TAGGS, Grant Watch)
- Expand to WHO ICTRP for global coverage
- Model trial phase and enrollment size as predictors
- Normalize stall rates by total trials per disease
- Re-run analysis with updated post-2025 data
- Switch to `MinimumAge`/`MaximumAge` API fields for true numeric age filtering

-----

## Related Work

This project feeds into:

**Pediatric Cancer Research Gap Analysis**  
https://github.com/DataInfamous/pediatric-cancer-research-gaps

That follow-up analysis combines this stalled-trials dataset with CDC WONDER incidence rates and CCSS late-effects mortality data to test whether pediatric cancer research activity aligns with survivor harm.

-----

## Author

Benjamyn Wilson  
DataInfamous