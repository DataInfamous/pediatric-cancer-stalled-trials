# Analysis Validation

## Overview

This document records validation steps taken to test the robustness of the primary analysis:

> Do pediatric cancer diseases with greater survivor harm show higher clinical trial stall rates?

The goal of this validation was to ensure that any observed relationship was not driven by methodological artifacts such as aggregation bias, temporal confounding, or inconsistent disease classification.

-----

## Dataset Scope

Trials were included if their ClinicalTrials.gov eligibility categories included `CHILD`. This reflects pediatric-eligible trials rather than strictly pediatric-only trials, and includes trials enrolling both children and adults. Age filtering is based on `StdAges` category labels, not numeric age limits.

-----

## Initial Result (Aggregated Categories)

The first analysis grouped diseases into broad categories (e.g., leukemia, lymphoma, sarcoma) and merged these with CCSS burden data using averaged subtype values.

- Spearman correlation: **ρ ≈ 0.80**
- p-value: **≈ 0.10**
- n = 5 disease groups

### Interpretation

This suggested a strong positive relationship between disease burden (non-recurrence mortality) and stall rates. However, the result was not statistically significant and relied on a small number of aggregated categories with averaged burden values.

-----

## Issue Identified: Aggregation Bias

Broad grouping combined biologically distinct diseases into single categories:

- Leukemia = ALL + AML
- Sarcoma = Ewing + Osteosarcoma + STS
- Lymphoma = Hodgkin + NHL

Averaging CCSS burden values across subtypes within these groups smoothed over meaningful variation in both stall rates and late-effects burden, producing a spurious correlation signal.

-----

## Expanded Analysis (Disaggregated Categories)

Disease categories were expanded into clinically meaningful subtypes aligned with CCSS groupings:

- ALL, AML
- Hodgkin, NHL (where applicable)
- Ewing, Osteosarcoma, STS
- Neuroblastoma
- CNS (aggregated fallback)

Filtering criteria:

- Minimum trial count threshold applied (≥50 trials per group)
- “Other” and ambiguous categories excluded
- Only categories present in both datasets retained

### Result

- Spearman correlation: **ρ = 0.18**
- p-value: **0.67**
- n ≈ 7–8 disease groups

-----

## Interpretation of Final Result

The correlation observed in the aggregated analysis **disappears when categories are properly disaggregated**.

This indicates:

- The initial signal was driven by aggregation bias, not a true underlying relationship
- There is **no meaningful or statistically significant relationship** between disease burden and trial stall rates at the subtype level

-----

## Additional Robustness Checks

### 1. Temporal Control

- Trials after 2020 excluded to avoid right-censoring bias
- Identified a major system-wide increase in stall rates during 2016–2020

### 2. Funder Stratification

- Stall rates analyzed by funding type
- Structured systems (NIH, networks) consistently showed lower stall rates
- Pattern remained stable across time periods

### 3. Statistical Testing

- Spearman correlation used for primary analysis
- Mann–Whitney and t-tests used for temporal comparisons

-----

## Final Conclusion

After controlling for:

- Time (censoring and structural shifts)
- Disease classification (aggregation bias)
- Sample size thresholds

The analysis finds:

> There is no meaningful relationship between disease-level survivor burden and clinical trial stall rates.

Instead, trial outcomes appear to be driven primarily by:

- System-level factors (time period)
- Structural factors (funding and institutional coordination)

-----

## Key Insight

The most important finding is not the absence of correlation, but the process by which an apparent correlation was shown to be an artifact of coarse disease grouping. This highlights the importance of:

- Proper disease classification at the subtype level
- Sensitivity testing across aggregation choices
- Avoiding premature conclusions from aggregated data

-----

## Implication for Future Work

Future analyses should:

- Expand disease subtype coverage where data allows
- Incorporate additional structural variables (trial phase, enrollment size, geography)
- Use longitudinal modeling to better understand temporal effects
- Switch to `MinimumAge`/`MaximumAge` API fields for true numeric age filtering

-----

*Author: Benjamyn Wilson*