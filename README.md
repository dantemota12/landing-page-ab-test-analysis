# Landing Page A/B Test Analysis

Statistical analysis of an A/B experiment comparing two versions of a landing page (**A** vs **B**), with a data-driven recommendation on which version to ship.

## Business Question

Which landing page version performs better in terms of **conversion rate** and **revenue per converted user**, and do traffic source or user type influence conversion?

## Dataset

`landing_experiment.csv` — 40,000 users exposed to the experiment (Jan 1–28, 2026), one row per user, no missing values or duplicates.

| Column | Description |
|---|---|
| `user_id` | Unique user identifier |
| `date` | Date the user was exposed to the page |
| `landing` | Page version shown (`A` or `B`) |
| `region` | User region (Norte, Centro, Sur, Occidente, Oriente) |
| `dispositivo` | Device type (Mobile, Desktop) |
| `traffic_source` | Acquisition channel (Organic, Ads, Email, Referral) |
| `user_type` | New (`Nuevo`) or returning (`Recurrente`) user |
| `converted` | 1 if the user converted, 0 otherwise |
| `gasto` | Amount spent in USD (0 if the user did not convert) |

> Some column names and category values are in Spanish, as in the original dataset. The dataset file is not included in this repository.

## Methodology

1. **Data validation** — types, nulls, duplicates, date range, category checks
2. **Average spend, A vs B** — Levene's test for equal variances → Welch's t-test
3. **Conversion rate, A vs B** — two-sample z-test for proportions
4. **Traffic source vs. conversion** — chi-square test of independence
5. **User type vs. conversion** — chi-square test of independence
6. **Visualization** — grouped and stacked bar charts with counts and percentages
7. **Executive summary** — findings and recommendations for stakeholders

All tests use a significance level of α = 0.05.

## Key Results

| Question | Test | Result |
|---|---|---|
| Spend per converted user | Welch's t-test | B: **$68.75** vs A: **$61.09** (+$7.66, ~12.5%), t = -9.48, p ≈ 3.6e-21 |
| Conversion rate | Z-test for proportions | B: **15.96%** vs A: **12.57%** (+3.38 pp), z = -9.68, p ≈ 3.8e-22 |
| Traffic source vs. conversion | Chi-square | Weak but significant association (χ² = 8.66, p = 0.034); Email 14.99% and Ads 14.74% highest, Organic 13.79% lowest |
| User type vs. conversion | Chi-square | No significant association (χ² = 0.51, p = 0.474); New 14.36% vs Returning 14.09% |

## Recommendation

**Ship landing page B.** It converts more users *and* generates higher spend per converted user, and both differences are highly statistically significant. Traffic source has only a small effect on conversion, and user type has none, so the page choice does not need to be segmented.

**Caveats:** the spend comparison only covers users who converted, and statistical significance does not account for implementation costs.

## Tech Stack

Python · pandas · NumPy · SciPy · statsmodels · Matplotlib · Seaborn · Jupyter Notebook

## Repository Structure

```
.
├── README.md
├── LICENSE
├── .gitignore
└── landing_experiment_analysis.ipynb
```

## How to Run

```bash
git clone https://github.com/dantemota12/landing-page-ab-test-analysis.git
cd landing-page-ab-test-analysis
pip install pandas numpy scipy statsmodels matplotlib seaborn jupyter
jupyter notebook landing_experiment_analysis.ipynb
```

Make sure the notebook's data path (`pd.read_csv(...)`) points to your local copy of `landing_experiment.csv`.

## Files

- `sprint_9_-_cuaderno_de_jupyter_-_S9_Version_Student_Proyecto_Landing_Experiment.ipynb`: full analysis notebook (data validation, hypothesis testing, visualizations and executive summary).
- `images/`: screenshots of the charts.
- [Download the notebook from Google Drive](https://drive.google.com/file/d/10k3UKSXa_xahNnGE_aaLqUexuC3YS66m/view?usp=drive_link)

## Author

**Dante Mota** — [GitHub](https://github.com/dantemota12)
