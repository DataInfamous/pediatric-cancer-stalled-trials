# Where Pediatric Cancer Trials Stall
### A Global Registry Analysis of Trial Termination, Suspension, and Missing Stop Reasons, 1995–Present

A geospatial and epidemiological analysis of 954 stalled pediatric cancer 
trials across 89 countries — examining where research stops, why it stops, 
and what the patterns reveal about global research infrastructure.

## Live Dashboard
[View on Power BI](https://app.powerbi.com/groups/me/reports/2cd4bd95-17e8-40d2-b5ed-1c63881d3681/f47d90003a9e67905063?experience=power-bi)

---

## Key Findings
- **954 stalled trials** across 89 countries spanning 1995–present
- **54% have no recorded stop reason** — reflecting registry incompleteness, 
  not a clinical finding
- **Low enrollment/accrual** is the #1 documented cause among trials with 
  recorded reasons (190 trials)
- Stalled trials **peaked in 2021** — consistent with COVID-era disruption, 
  though this reflects association, not causation
- **United States accounts for 394 trial locations** — more than 4x France 
  (92), consistent with high-income country concentration in pediatric 
  oncology research
- **St. Jude Children's Research Hospital stall rate: 7.2%** (10/138 trials) 
  vs overall dataset rate of 41.8% — consistent with philanthropic funding 
  model providing institutional resilience during public funding disruptions
- **Post-2025 trials are significantly more likely to stall for 
  funding-related reasons** (logistic regression, p=0.002), consistent with 
  DOGE-era NIH/HHS funding disruptions beginning January 2025

---

## Regression Analysis
Logistic regression (n=954) predicting funding-related trial termination:

| Predictor | Coefficient | p-value | Interpretation |
|-----------|-------------|---------|----------------|
| Post2025 | 3.202 | 0.002 | Trials starting 2025+ significantly more likely to stall for funding reasons |
| NumCountries | 0.059 | 0.028 | Multi-country trials show slightly higher funding-related stall risk |
| SponsorType_Pharma | 1.055 | 0.005 | Pharma-sponsored trials more likely to cite funding/business reasons |
| SponsorType_Other | -0.009 | 0.980 | Not significant |

**Model**: Logistic regression, MLE, converged. Pseudo R² = 0.048. 
LLR p-value = 0.0008.

**Note**: Post2025 association is consistent with DOGE-era NIH/HHS funding 
disruptions beginning January 2025. Causation cannot be established from 
registry data alone.

---

## Definitions

| Term | Definition |
|------|------------|
| Stalled | Any trial with status: TERMINATED, WITHDRAWN, UNKNOWN, SUSPENDED, or NO_LONGER_AVAILABLE |
| TERMINATED | Trial started but stopped before completion |
| WITHDRAWN | Trial never enrolled participants |
| UNKNOWN | No registry update in extended period |
| SUSPENDED | Temporarily halted, reason may vary |
| NO_LONGER_AVAILABLE | Access discontinued |
| Country | Country of at least one registered trial site |

---

## Data Source
[ClinicalTrials.gov API v2](https://clinicaltrials.gov/data-api/api)

**Filters applied:**
- Condition: Pediatric Cancer
- Statuses: TERMINATED, WITHDRAWN, UNKNOWN, SUSPENDED, NO_LONGER_AVAILABLE

---

## Tools
- Python (data extraction, cleaning, feature engineering, logistic regression)
- Microsoft Excel (data cleaning)
- Power BI (dashboard and geospatial visualization)

---

## Limitations
- Registry data is self-reported and inconsistently maintained — stop reasons 
  are missing for 54% of trials
- Status categories are not clinically interchangeable and reflect different 
  operational realities
- Country counts reflect trial site locations, not sponsoring country
- Analysis is descriptive and associative; temporal patterns cannot establish 
  causation
- ClinicalTrials.gov skews toward US and high-income country trials — global 
  coverage is incomplete without WHO ICTRP
- Post-2025 sample is small — regression findings should be interpreted 
  cautiously pending additional data

---

## Project Structure


├── data/

│   ├── stalled_trials_final.csv

│   └── trials_by_country.csv

├── notebooks/

│   └── pediatric_cancer_trial_analysis.ipynb
└── README.md


---

## Future Research Directions
- Use ClinicalTrials.gov API condition tags (rather than title keywords)
  to improve disease categorization for cross-analysis with late-effects
  burden data
- Cross-reference with [Grant Watch Database](https://www.statnews.com/2025/05/27/nih-cuts-tracked-in-grant-watch-database-q-and-a-with-harvard-researcher-scott-delaney/)
  (Harvard, 2025) — 383 trials disrupted, 74K participants affected
- Download AACT full ClinicalTrials.gov dataset for expanded regression 
  with post-2025 cohort
- Merge with HHS TAGGS grant termination data to identify specific 
  institutions affected
- Normalize by total pediatric cancer trials per country to calculate 
  stalled trial rates
- Expand to WHO ICTRP for broader global coverage
- Re-pull API in Q3 2026 to assess whether Post2025 signal strengthens

---

## Related Work

This dataset is used as an input in
[pediatric-cancer-research-gaps](https://github.com/DataInfamous/pediatric-cancer-research-gaps),
which correlates stalled trial distribution against late-effects burden
from CCSS mortality data and CDC WONDER incidence rates — asking whether
the diseases most represented in stalled trials are the ones where
survivor harm is greatest.

---

*Author: Benjamyn Wilson | [DataInfamous](https://github.com/DataInfamous)*
