# Pediatric Cancer Stalled Trials

An analysis of 950 stalled pediatric cancer trials registered globally on ClinicalTrials.gov — exploring where research stops, why it stops, and who is responsible.

## Live Dashboard
[View on Power BI](https://app.powerbi.com/groups/me/reports/2cd4bd95-17e8-40d2-b5ed-1c63881d3681/f47d90003a9e67905063?experience=power-bi)

## Key Findings
- 950 stalled trials spanning 1995–2026 across 89 countries
- 54% have no recorded reason for stopping — the largest single category
- Low enrollment/accrual is the #1 documented cause, affecting 190 trials
- St. Jude Children’s Research Hospital appears in the top 15 sponsors with stalled trials
- Stalled trials peaked in 2021 then declined — COVID disruption visible in the data
- United States dominates with 394 trial locations, more than 4x the next country (France, 92)

## Data Source
- ClinicalTrials.gov API v2  
  - Filtered for pediatric cancer  
  - Statuses: TERMINATED, WITHDRAWN, UNKNOWN, SUSPENDED, NO_LONGER_AVAILABLE

## Tools
- Python (data extraction, cleaning, feature engineering)
- Microsoft Excel (data cleaning)
- Power BI (dashboard)

## Project Structure

├── data/


│ ├── stalled_trials_final.csv
│ └── trials_by_country.csv


├── notebooks/
│ └── data_extraction.ipynb


└── README.md


## Future Research Directions
- Correlate stalled trial rates with pharmaceutical lobbying expenditure by country
- Connect funding disruption events (NIH restructuring, HHS changes) to trial termination spikes
- Expand to WHO ICTRP for broader global coverage beyond ClinicalTrials.gov
