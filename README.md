# Coca Supply Shocks and Violence in Colombia

An applied **difference-in-differences** case study exploring whether coca-growing departments experienced a larger change in recorded violence than comparison departments. The analysis demonstrates causal reasoning beyond A/B testing through an observational research design, pre-trend diagnostics, a placebo test, and covariate-adjusted regressions.

[Open the notebook](Original_Coca_Violence_Difference_in_Differences.ipynb)

## Project overview

The study compares **1991–1993** with **1996–1998**, using an extract associated with Angrist and Kugler (2008). Exposure is defined by nine department codes classified as coca-growing. The original research describes disruption of the coca supply air bridge beginning in 1994; 1996 is the start of the selected post-analysis window, not the event date.

The central question is whether violence changed more in exposed regions than in comparison regions. A causal interpretation requires parallel counterfactual trends and the absence of relevant differential shocks, anticipation, or spillovers.

## Methods demonstrated

- Construction of exposure, period, and interaction indicators.
- Distributional exploration by exposure group and sex code.
- Descriptive before–after changes by age category.
- Linear and categorical pre-treatment trend regressions.
- A pre-period placebo using 1992–1993 as a false post-period.
- Four-mean and regression-based difference-in-differences estimation.
- Comparison of pooled specifications with additional covariates.
- Discussion of confounding, post-treatment adjustment, and identification limits.

## Saved results

The outcome is `log(violent_ + 1) - log(populati + 1)`, a log-smoothed population-normalized violence measure.

| Pooled specification | DiD estimate | Reported p-value |
|---|---:|---:|
| Exposure, period, and interaction | 0.2526 | 0.003 |
| Add age and sex codes | 0.1869 | 0.007 |
| Also add supplied population | 0.1808 | 0.009 |

These values come from the **original saved outputs**, not a new execution. All three models report conventional, nonrobust OLS standard errors. The baseline interval is approximately [0.083, 0.422].

The placebo coefficient is approximately −0.0124 (p = 0.909). Individual pre-year interaction tests also fail to reject. These diagnostics do not prove parallel trends, establish random assignment, or rule out confounding. The notebook does not implement a joint pre-trend test, clustered inference, department fixed effects, or an event-study model.

The positive estimates describe a differential change in the transformed outcome. They should not be presented as a verified percentage increase in individual mortality risk or proof of a specific mechanism.

## Data and interpretation

The included tab-separated extract contains **12,544 rows**, **11 source columns**, **33 department codes**, and years **1990–2000**. Observations are department–year–age-code–sex-code cells. The saved main regressions use 6,449 observations.

- `age` contains category codes, not literal ages. The original regressions nevertheless treat it numerically.
- Population is missing in 682 rows. The original models drop rows with missing required values through their default behavior.
- Population denominators are repeated across matched male/female cells. Sex-specific mortality rates are not validated by this extract.
- Missing cells, concurrent regional shocks, and post-treatment population adjustment are relevant limitations.

The supplied data file is included unchanged as `data00_AngristKugler.tab` **beside the notebook**, matching the original code's relative path. Its detailed transformation history and redistribution terms were not supplied.

## View and use

Open the notebook on GitHub or in a Jupyter-compatible editor to inspect its saved figures and regression tables. No execution is required to review those results.

Keep the notebook and data file in the same directory. The dependency list is unpinned because the original execution environment is unknown.

**Known execution dependency:** the DiD-summary section reloads `data` without reconstructing `growafter`; later regressions reference that column. A fresh top-to-bottom execution may therefore fail at that point. This version intentionally preserves the original code, rather than silently fixing it. The saved outputs remain available, but a successful fresh run is not claimed.

## Files

| File | Purpose |
|---|---|
| `Original_Coca_Violence_Difference_in_Differences.ipynb` | English project narrative with original code and saved outputs |
| `data00_AngristKugler.tab` | Unmodified supplied data |
| `README.md` | Project overview, saved findings, and limitations |

## Preservation and attribution

Source: Angrist, J. D., & Kugler, A. D. (2008). *Rural Windfall or a New Resource Curse? Coca, Income, and Civil Conflict in Colombia.* Review of Economics and Statistics, 90(2), 191–215. [Paper](https://economics.mit.edu/sites/default/files/publications/AK2008_corrected.pdf) · [MIT data archive](https://economics.mit.edu/people/faculty/josh-angrist/angrist-data-archive).

