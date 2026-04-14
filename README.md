# Where Pediatric Cancer Trials Stall
### A Global Registry Analysis of Trial Termination, Suspension, and Missing Stop Reasons, 1995–Present

A geospatial and epidemiological analysis of 950 stalled pediatric cancer trials across 89 countries — examining where research stops, why it stops, and what the patterns reveal about global research infrastructure.

## Live Dashboard
[View on Power BI](https://app.powerbi.com/groups/me/reports/2cd4bd95-17e8-40d2-b5ed-1c63881d3681/f47d90003a9e67905063?experience=power-bi)

---

## Key Findings
- **950 stalled trials** across 89 countries spanning 1995–present
- **54% have no recorded stop reason** — reflecting registry incompleteness, not a clinical finding
- **Low enrollment/accrual** is the #1 documented cause among trials with recorded reasons (190 trials)
- Stalled trials **peaked in 2021** — consistent with COVID-era disruption, though this reflects association, not causation
- **United States accounts for 394 trial locations** — more than 4x France (92), consistent with high-income country concentration in pediatric oncology research
- **St. Jude Children's Research Hospital** appears among top sponsors by volume — a reflection of large research footprint, not comparative performance

---

## Definitions
| Term | Definition |
|------|-----------|
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
- Python (data extraction, cleaning, feature engineering)
- Microsoft Excel (data cleaning)
- Power BI (dashboard and geospatial visualization)

---

## Limitations
- Registry data is self-reported and inconsistently maintained — stop reasons are missing for 54% of trials
- Status categories are not clinically interchangeable and reflect different operational realities
- Country counts reflect trial site locations, not sponsoring country
- Analysis is descriptive; temporal patterns (e.g. COVID peak) reflect association, not causation
- ClinicalTrials.gov skews toward US and high-income country trials — global coverage is incomplete without WHO ICTRP

---

## Project Structure


```
├── data/
│   ├── stalled_trials_final.csv
│   └── trials_by_country.csv
├── notebooks/
│   └── data_extraction.ipynb
└── README.md
```




---

## Future Research Directions
- Normalize by total pediatric cancer trials per country to calculate stalled trial rates
- Add sponsor-level rates (stalled trials per registered trial) for more defensible comparisons
- Correlate stalled trial patterns with pharmaceutical lobbying expenditure by country
- Connect funding disruption events (NIH restructuring, HHS changes) to termination spikes
- Expand to WHO ICTRP for broader global coverage
