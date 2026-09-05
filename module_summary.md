# Module Summary: Reproducible Data Science Workflow for NYC Airbnb Listings

## Overview

This project implements a complete, reproducible data-science workflow on the NYC Airbnb
listings dataset, using only Python, NumPy, Pandas, Matplotlib, Seaborn, and Git — no
machine-learning models are trained (Wright, 2023). The workflow ingests a CSV, cleans and
transforms the data with documented, reusable functions, runs exploratory analysis, and
produces labeled visualizations, all version-controlled so the entire pipeline can be rerun
from scratch. In short, price in this market is driven largely by property type and location,
while availability and review metrics add little explanatory power in this univariate analysis.

## Dataset Description

The dataset is the **New York City Airbnb Open Data** release, which captures short-term
rental listings in NYC for 2019
(dgomonov, 2019). It contains roughly 48,000 listings across the five NYC boroughs, organized
into 16 tabular columns that describe the listing's location (neighbourhood_group,
neighbourhood, latitude, longitude), property characteristics (room_type, minimum_nights,
number_of_reviews, availability_365), the host (host_id, host_name), and the target variable,
`price` (US dollars per night). This report focuses on `price` as the target and examines its
relationship to `neighbourhood_group`, `room_type`, `minimum_nights`, `reviews_per_month`, and
`availability_365`.

## Workflow Description

The workflow proceeds in five stages.

- **Ingestion.** The CSV is loaded with Pandas and the first rows are displayed to confirm
  the data arrived correctly.
- **Cleaning.** Missing values, outliers, and non-rentable listings are addressed using two
  reusable cleaning functions with docstrings.
- **Exploratory analysis.** A correlation block quantifies how much variance each variable
  explains on its own, followed by grouped descriptive statistics by borough and property type.
- **Visualizations.** Four figures summarize the univariate distributions and the bivariate
  dependence of price on location and property type.
- **Summary.** The findings, assumptions, limitations, and surprising patterns are documented.

## Key Decisions and Assumptions

**Cleaning choices.** First, listings whose `last_review` is missing are given
`reviews_per_month = 0.0`. This encodes the domain assumption that an absent review date means
no rental activity, rather than a random missing value. Second, price is clipped at the 0.5%
and 99.5% quantiles to remove extreme outliers that would distort correlation values and
obscure the boxplots. Third, `shared room` listings are dropped so the analysis focuses on
whole-property nightly rates.

These choices are not free of consequence. Missing data are frequently **not** missing at
random, and common imputation or deletion approaches can shift results and amplify bias
(Little & Rubin, 2002). Setting `reviews_per_month` to 0 therefore imposes a plausible but
unverifiable assumption about inactive listings. The 1% price clip discards roughly 1% of
listings and truncates the heavy upper tail, so summary statistics no longer include the
most expensive properties. Removing shared rooms narrows the population to whole-property
rentals, so the findings describe that segment rather than all of NYC Airbnb.

**Exploratory focus.** The EDA block was designed to answer one question — "how much of price
does each feature explain on its own?" — using a common yardstick. For the numeric features,
Spearman's ρ measures monotonic association; for the categorical features, the correlation
ratio η measures how well the grouping predicts price, and η² is exactly the ANOVA effect size
(the proportion of variance explained).

**What each plot was designed to show.** Figure 1 summarizes the univariate distributions of
price and the two key categorical variables. Figure 2 shows the median nightly price by
borough to reveal the location gradient. Figure 3 shows price by property type within each
borough to demonstrate that property type raises price independently of location.

## Results and Interpretation

**How much does each feature explain on its own?** Squaring each statistic puts them on a
common scale — the proportion of price variance explained by that variable alone:

| Numeric feature       | Spearman ρ | Variance explained (ρ²) |
|-----------------------|-----------:|------------------------:|
| minimum_nights        | +0.098     | 0.96%                   |
| availability_365      | +0.099     | 0.98%                   |
| number_of_reviews     | −0.054     | 0.29%                   |

| Categorical feature | η      | Variance explained (η²) |
|---------------------|-------:|------------------------:|
| neighbourhood_group | 0.088  | 0.77%                   |
| room_type           | 0.219  | 4.8%                    |

Every feature except `room_type` explains **under 1%** of price variance on its own.
`room_type` is the lone outlier at ~5%: entire homes/apt consistently outprice private rooms.

**Location gradient (Figure 1–2).** By neighbourhood, median nightly price falls in an ordered
gradient — Manhattan ($150) > Brooklyn ($95) > Queens ($75) ≈ Staten Island ($75) > Bronx ($69)
— with Manhattan's mean (≈$181) nearly double the Bronx's (≈$88).

**Property type (Figure 3).** Within every borough, "Entire home/apt" listings command a higher
median than "Private room" listings, and this stratification holds across all five boroughs.

**Why is neighbourhood's η² so small (0.77%) despite a visible Manhattan–Bronx gap?** Because
price is heavily right-skewed, the large within-group spread and the extreme tail inflate the
denominator of η, shrinking it. The median gap is real and clearly visible in Figures 1–2; the
correlation ratio is computed on the mean, which skews badly under this distribution. For such
heavily skewed data the median is a more robust measure of central tendency than the mean
(Wilcox, 2012), which is why the grouped statistics and plots report the median.

**Takeaway.** Both the correlation results and the grouped statistics agree: price is
predominantly a function of property type, to a lesser extent location, and essentially
independent of minimum-nights, review frequency, and availability in this univariate analysis.
Yet even the strongest single feature explains less than 5% of price variance — price is driven
more by the wide spread *within* each category than by these features alone, which is exactly
why a predictive model would need more predictors than any of these univariate measures.

## Responsible Practice (Bias and Data Quality)

Several cleaning and handling decisions could introduce bias or misleading results. First,
clipping the 0.5%/99.5% quantiles discards ~1% of listings and truncates the heavy upper tail,
so the reported medians no longer reflect the most expensive listings. Second, dropping 
`shared room` listings narrows the population to whole-property rentals, so results describe 
that segment rather than all NYC Airbnb. Third, the Bronx and Staten Island have the fewest
listings, making their medians more sensitive to outliers and less stable.

## Reproducibility

Anyone can rerun this work from the cloned repository. The `requirements.txt` file, generated
with `pip freeze`, pins every dependency so the environment can be recreated exactly
(`pip install -r requirements.txt`). The code is organized into modular, reusable cleaning and
EDA functions, each with an informative docstring, and the entire workflow is tracked with Git:
development work is carried out on a separate feature branch and integrated back into `main`
through commits, which supports auditability and iteration (Wright, 2023).

## Sources and Citations

**References**

dgomonov. (2019). *New York City Airbnb Open Data.* Kaggle. https://www.kaggle.com/datasets/dgomonov/new-york-city-airbnb-open-data

Little, R. J. A., & Rubin, D. B. (2002). *Statistical analysis with missing data* (2nd ed.). John Wiley & Sons.

Wilcox, R. R. (2012). *Introduction to robust estimation and hypothesis testing* (3rd ed.). Academic Press.

Wright, T. (2023). Reproducible data science with Python: An open learning resource. *Journal of Open Source Software, 8*(90), 5784. https://doi.org/10.21105/joss.05784
