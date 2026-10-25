# ConnectaTel Customer Behavior Analysis

An end-to-end exploratory data analysis of a Latin American telecommunications company, covering **data quality, usage profiling, outlier detection and customer segmentation**, to support retention strategies and plan design.

**Tech stack:** Python · pandas · NumPy · seaborn · Matplotlib · Jupyter Notebook

---

## Overview

ConnectaTel offers two plans (Basic and Premium) to customers across Latin America. To make good decisions about retention and pricing, the business needs to know who its customers are, how they actually use the service, and whether the current plans fit that behavior.

This project turns three raw datasets (plans, customers and usage records through 2024) into a clean customer profile. It identifies and fixes data quality problems, describes usage patterns by plan and age, flags atypical consumers, and groups customers into segments that can be targeted commercially.

## Objectives

1. Assess the quality of the data and correct invalid values, missing values and impossible dates.
2. Build a statistical profile of customers and of their real usage (calls, minutes and messages).
3. Detect atypical usage behavior and decide how to treat it.
4. Segment customers by usage level and by age.
5. Translate the findings into recommendations to improve the current plans and retention strategy.

## Data

| Dataset | Content | Size |
|---|---|---|
| `plans.csv` | Current plans: price, included minutes, included GB and cost per extra | 2 rows, 8 columns |
| `users_latam.csv` | Customers: age, city, registration date, plan and churn date | 4,000 rows, 8 columns |
| `usage.csv` | Individual service usage records (calls and text messages) | 40,000 rows, 6 columns |

## Data quality issues found and how they were handled

| Column | Issue | Treatment |
|---|---|---|
| `users.age` | Sentinel value of -999 (impossible age) in 55 rows (1.4%) | Replaced with the median, calculated excluding the sentinel |
| `users.city` | 469 nulls (11.7%) plus 96 records with `'?'` as a text sentinel (2.4%), 565 nulls in total (14.1%) | `'?'` converted to `pd.NA`; nulls kept, not imputed |
| `users.reg_date` | 40 rows (1%) dated 2026, outside the data range (through 2024) and inconsistent with usage already recorded in 2024 | Marked as `NaT` |
| `users.churn_date` | 3,534 nulls (88.35%) | Not an error: an empty value means the customer is still active |
| `usage.date` | 50 nulls (0.125%) | Kept as `NaT` |
| `usage.duration`, `usage.length` | 55.19% and 44.74% nulls | Confirmed as *Missing At Random*: they depend on `type` (duration only applies to calls, length only to texts), so they were left as nulls |

## Methodology

The analysis follows seven documented steps in the notebook:

1. **Load and explore** the three datasets: structure, data types and first rows.
2. **Identify data quality issues:** null values, sentinels and impossible or out-of-range dates.
3. **Clean the data:** replace sentinels, mark invalid dates and justify how missing values are handled.
4. **Summarize usage per user:** aggregate calls, minutes and messages by `user_id` and merge them with the customer table into a single `user_profile`.
5. **Visualize distributions and outliers:** histograms by plan, boxplots and IQR limits.
6. **Segment customers** by usage level (`grupo_uso`) and by age (`grupo_edad`).
7. **Write the executive insight** for stakeholders.

### Segmentation rules

| Segment | Rule |
|---|---|
| Usage: low (`'Bajo uso'`) | calls < 5 and messages < 5 |
| Usage: medium (`'Uso medio'`) | calls < 10 and messages < 10 |
| Usage: high (`'Alto uso'`) | all other cases |
| Age: young (`'Joven'`) | age < 30 |
| Age: adult (`'Adulto'`) | age < 60 |
| Age: older adult (`'Adulto Mayor'`) | age ≥ 60 |

## Key findings

- **Plan mix:** 64.9% of customers are on the Basic plan and 35.1% on Premium.
- **Premium follows age more than consumption.** The older the customer, the higher the relative share of Premium users; younger customers are concentrated in the Basic plan.
- **Basic customers use more voice.** They make more calls and accumulate more total call minutes than Premium customers, while there is no clear difference between plans in messages.
- **Usage is right-skewed.** Most customers send about 5 messages and make about 4 calls (the medians), while a small group sits far above that.
- **Outliers exist only on the high side** for messages (12–17), calls (11–15) and call minutes (above about 62, up to 155.69). Age has no outliers (range 18–79).

## Recommendations

- Create an **intermediate plan** for customers, especially young people and adults, with heavy call usage who do not need everything Premium includes.
- **Review the minutes included in the Basic plan.** It is the segment that consumes the most minutes, which may expose it to overage charges and churn.
- Design **upselling campaigns** aimed at older Basic customers, who show a greater tendency to move to Premium.
- Provide **special follow-up for outliers in call minutes** as candidates for personalized, higher-value offers.

## Repository contents

| File | Description |
|---|---|
| `connectatel_customer_analysis_EN.ipynb` | Full analysis notebook, with code, documentation and saved outputs (tables and charts) |
| `README.md` | Project description |

## Viewing and reproducing the analysis

The notebook is saved with its outputs, so tables and charts can be read directly on GitHub without running any code.

In the notebook, the source files are read from `/datasets/plans.csv`, `/datasets/users_latam.csv` and `/datasets/usage.csv`. To re-run the analysis, place the three files in a folder of your choice and update those paths in the data loading cell. Required libraries: `pandas`, `numpy` and `seaborn`, plus `matplotlib`.

## Author

**Natalia Sepúlveda** — Data Analyst | Business Intelligence

[LinkedIn](https://www.linkedin.com/in/natalia-sepulveda-escobar) · [GitHub](https://github.com/nataliasepulveda-28)
