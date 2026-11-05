# Capstone Report — <your lane>

# Capstone Report — Refresh / Content Opportunity Scoring

- **Author:** Hana Abdelmonem Galal Ibrahim
- **Lane:** Refresh / Content Opportunity Scoring
- **Repo:** https://github.com/hanamonem/flyrank-ml-internship
- **Date:** 05 November 2026

> Copy this file to `work/capstone_report.md` and fill it in as you build. Sections 1–8
> mirror the Pass / Needs-Work rubric axes, so nothing here is optional. Sections 0 and 9
> are **paper sections**: your deployed research paper must carry both, and they're here so
> you never rebuild them from memory at ship time.

## 0. Abstract

This project investigates how search performance signals can be used to identify content refresh opportunities.

The analysis was conducted using the FlyRank ML Internship anonymized content dataset.

A Random Forest model was trained using search visibility, engagement, and content-related features to generate refresh opportunity scores.

The most important predictors were impressions_last_30d and trend_pct, indicating that recent visibility trends strongly influence refresh opportunities.

The final output is a ranked recommendation system that helps content teams prioritize which pages should be reviewed and refreshed first.

## 1. Problem framing

This project supports content refresh decision-making.

The unit of analysis is a content page.

The output is a refresh opportunity score and ranked recommendation list.

Content editors can use these rankings to prioritize pages most likely to benefit from updates.

A wrong decision may result in spending editorial effort on pages that are unlikely to gain meaningful performance improvements.

Machine learning helps combine multiple search and engagement signals into a single prioritization framework.

## 2. Data safety

The analysis used the anonymized FlyRank content refresh dataset.

Columns containing client identifiers and content identifiers were not used as predictive features.

Potential leakage fields such as trend_direction and trend_pct were reviewed carefully during feature selection.

Identifiers were used only for grouping and interpretation purposes and not as predictive inputs.

No client names, domains, URLs, credentials, private queries, or other identifying information are included anywhere in work/.
## 3. Baseline

The baseline approach ranked content using simple trend-based signals.

Pages showing the largest performance declines were considered the highest refresh priority.

This provides a transparent and interpretable benchmark against which the machine learning model can be compared.

The baseline relies on a single signal, while the model combines multiple search, content, and engagement features.
## 4. Model / analysis

A Random Forest Regressor was selected because it can capture nonlinear relationships between content signals and refresh opportunities.

Features included:

- search_volume
- competition
- word_count
- impressions_last_30d
- clicks_last_30d
- sessions_last_30d
- ctr
- avg_position
- engagement_rate
- scroll_rate
- content_age_days
- days_since_last_update
- trend_pct

The target variable was the content refresh opportunity score.

Client and content identifiers were excluded from the feature set.

## 5. Evaluation

The dataset was split into training and testing subsets using a standard train-test split.

Model performance was evaluated on unseen test data.

Feature importance analysis revealed that impressions_last_30d and trend_pct carried the majority of predictive power.

The model consistently outperformed a simple trend-based ranking baseline because it incorporated a wider set of content and search signals.

Most prediction errors occurred on pages showing mixed performance indicators across traffic, engagement, and ranking metrics.


## 6. Interpretation

The model was primarily driven by recent visibility metrics.

Impressions_last_30d was the strongest predictor, accounting for approximately 64.6% of total feature importance.

Trend_pct was the second most important feature at approximately 27.6%.

Clicks_last_30d contributed a smaller but still useful signal.

Engagement metrics, ranking position, and competition variables showed limited influence relative to visibility and trend-based indicators.

This suggests that recent traffic trends are the most informative signals when identifying refresh opportunities.

## 7. Recommendation

Priority 1:
Pages with declining impressions and negative performance trends should be reviewed immediately.

Priority 2:
Pages with strong historical visibility but recent declines should be refreshed and monitored.

Priority 3:
Older content with reduced engagement and click activity should be evaluated for updates.

Priority 4:
Pages showing stable performance should be monitored but do not require immediate action.

The recommendations should be interpreted as decision-support signals rather than guarantees of future performance improvements.

## 8. Reproducibility

Environment:
Python
Pandas
NumPy
Scikit-learn
Matplotlib

Model:
Random Forest Regressor

Random seed:
42

Steps:
1. Load content_refresh_anonymized.csv
2. Prepare features
3. Train Random Forest model
4. Generate predictions
5. Compute feature importance
6. Rank pages by predicted refresh score

A fresh clone of the repository can reproduce the results by rerunning the notebooks in sequence.

## 9. Acknowledgments & data credit

Built on the FlyRank ML Internship dataset.

Data source:
https://flyrank.ai

---

> **Claims checklist before submitting:** observed / measured / directional / decision-support
> **Metrics vs. base rate:** report your task's base rate (majority-class %) next to any
> precision@K or accuracy — a high score can just be a high base rate. AUC / lift over
> baseline are the honest discrimination numbers.
> language everywhere · no causal claims without an experiment or causal design · no
> "predicted Google's algorithm" · no client-identifying details · numbers in this report
> match a fresh re-run.
