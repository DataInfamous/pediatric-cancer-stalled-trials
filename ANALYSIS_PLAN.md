# Analysis Plan

## Project Question

This re-analysis asks whether pediatric cancer diseases with greater survivor harm show higher or lower clinical trial stall rates. The goal is to test whether research activity, measured by stalled trial rates, aligns with disease burden among childhood cancer survivor groups.

## Data Source

Clinical trial records will be retrieved from ClinicalTrials.gov using the REST API v2.

Primary query:

`AREA[ConditionSearch](Neoplasms) AND AREA[StdAge](CHILD)`

This query is intended to capture studies related to neoplasms that include child participants.

## Inclusion Criteria

Trials are in scope if they meet both criteria:

1. The study is returned by the ClinicalTrials.gov query above.
2. The study includes child participants according to the ClinicalTrials.gov standard age field.

The primary dataset will include all study statuses so that stalled trial rates can be calculated using both numerator and denominator.

## Fields to Retrieve

The API pull will retain the fields needed for analysis and auditing:

- `NCTId`
- `BriefTitle` or `OfficialTitle`
- `OverallStatus`
- `Conditions`
- `ConditionMeshTerms`
- `LeadSponsorName`
- `LeadSponsorClass`
- `StudyType`
- `Phases`
- `EnrollmentCount`
- `StartDate`
- `CompletionDate`
- `WhyStopped`
- `LocationCountry`
- `MinimumAge`
- `MaximumAge`
- `StdAges`
- API version / data timestamp when available

## Stalled Trial Definition

The primary stalled definition will include:

- `TERMINATED`
- `WITHDRAWN`
- `SUSPENDED`
- `NO_LONGER_AVAILABLE`

`UNKNOWN` will be analyzed separately as a sensitivity check because it may reflect missing registry status rather than a confirmed stalled or discontinued trial.

## Disease Classification

Disease groups will be mapped using structured MeSH terms first, with free-text conditions used only as a fallback.

The goal is to align trial records with approximately 10 CCSS-compatible pediatric cancer categories. Trials that map to multiple disease categories will be flagged. The primary analysis will use the first clearly mapped category or exclude ambiguous multi-category records in a sensitivity check.

Trials that cannot be mapped to a target disease category will be assigned to `other` and excluded from disease-level correlation analysis, but retained for dataset auditing.

## Primary Correlation

The primary test will be:

Spearman correlation between disease-level stalled trial rate and CCSS non-recurrence mortality.

Unit of analysis:

Disease group.

Expected n:

Approximately 10 disease groups, depending on successful mapping and minimum sample size thresholds.

## Secondary Analyses

Secondary tests may include:

- Spearman correlation between stalled trial rate and disease incidence
- Spearman correlation between stalled trial rate and late-effects burden index
- Comparison of raw stalled trial counts versus stalled trial rates

## Significance Threshold

The primary significance threshold will be:

`alpha = 0.05`

Because multiple correlations may be tested, secondary analyses will be interpreted cautiously. If more than one primary-style comparison is emphasized, Bonferroni or false discovery rate correction will be reported.

## Robustness Checks

The following sensitivity analyses will be run regardless of the primary result:

1. Excluding `UNKNOWN` from the stalled definition.
2. Including `UNKNOWN` in the stalled definition.
3. Excluding disease groups with fewer than 100 total trials.
4. Excluding ambiguous multi-category trials.
5. Comparing MeSH-based mapping against free-text fallback mapping.
6. Comparing API-derived results against the previous CSV-derived dataset.
7. Reporting whether conclusions change when using stalled trial counts instead of stalled trial rates.

## Planned Outputs

The analysis will produce:

- Clean API-derived dataset
- Disease-level trial counts
- Disease-level stalled trial counts
- Disease-level stalled trial rates
- Mapping audit table
- Correlation results
- README methodology note
