# EXP-003 — Isolation Forest Feature Ablation Study

## 1. Research Question

How does removing individual account-level features affect Isolation Forest performance, particularly when detecting subtle anomalies?

## 2. Hypothesis

Removing informative features may reduce anomaly detection performance, especially for subtle cases.

## 3. Dataset and Methodology

The experiment uses Synthetic Account Dataset v2, containing 1,000 accounts:

- 940 normal accounts
- 30 extreme synthetic anomalies
- 30 subtle synthetic anomalies

Three numerical features were evaluated:

- `num_devices`
- `num_transactions_24h`
- `connected_accounts`

Four Isolation Forest configurations were trained: one with all three features and three variants, each omitting a different feature.

All models used 100 estimators, `contamination=0.06`, `random_state=42`, and the same 80/20 stratified train/test split.

Anomaly labels were not used during model fitting.

## 4. Results

| Feature set | Precision | Recall | F1-score | Subtle Recall |
|---|---:|---:|---:|---:|
| All features | 0.846 | 0.917 | 0.880 | 0.833 |
| Without connected accounts | 0.556 | 0.833 | 0.667 | 0.667 |
| Without number of devices | 1.000 | 0.833 | 0.909 | 0.667 |
| Without transactions | 0.750 | 0.750 | 0.750 | 0.500 |

The model without `num_devices` achieved the highest overall F1-score (0.909).

However, the full-feature baseline achieved the highest subtle anomaly recall (0.833).

This demonstrates that selecting a model based on overall F1-score can lead to a different choice than selecting one based on recall for a specific anomaly category.

## 5. Per-Account Error Analysis

Six subtle anomalies were examined individually.

Three findings were particularly interesting:

**ACC_00619 — Missed by all models**

The account had 3 devices, 14 transactions in 24 hours, and 7 connected accounts. All four models classified it as normal.

Its features were relatively close to typical account behavior, potentially making it difficult to isolate.

**ACC_00663 — Sensitive to feature selection**

This anomaly was detected by the full-feature model and the model without `connected_accounts`, but missed by the other two configurations.

**ACC_00873 — Missed without connected accounts**

The full-feature model and two other variants detected this account, while the variant without `connected_accounts` did not.

These observations suggest that feature subset selection changes which individual anomalies are detected.

They do not establish definitive feature-level causal explanations.

## 6. Key Learnings

1. Higher overall F1-score does not necessarily imply better recall for subtle anomalies.
2. Removing features can improve some metrics while worsening others.
3. Per-account prediction comparisons provide useful information beyond aggregate metrics.
4. Different feature subsets may produce complementary detection patterns.
5. When every model misses the same anomaly, simple voting among those models cannot recover it.

## 7. Limitations

- Data are synthetic and deliberately constructed.
- The test set contains only six subtle anomalies.
- Results are based on one random seed and one train/test split.
- Feature configurations were compared using test labels, making the comparison exploratory rather than an independent model-selection procedure.
- The `connected_accounts` feature represents an aggregated count, not actual graph connectivity.
- The study does not establish causal feature importance or real-world fraud detection capability.

## 8. Next Steps

- Evaluate stability across multiple random seeds.
- Introduce separate validation and test sets.
- Compare Isolation Forest with Local Outlier Factor.
- Explore a more realistic transaction dataset.
- Engineer graph-based features and investigate Memgraph.
- Later compare traditional ML with Graph Neural Networks.

## 9. Personal Research Reflection

The most important lesson from this experiment is that model evaluation requires more than selecting the highest metric.

Although removing the device feature improved overall F1-score, it reduced the detection rate for subtle anomalies.

I also observed that different feature subsets could detect different accounts. However, one subtle anomaly was missed by every model.

This raises an important question for future research: are the current numerical features sufficient, or would additional contextual and graph-based information help detect less obvious patterns?

I intend to test this rather than assume graph-based models will necessarily perform better.

## Related Work

- [EXP-002 — Harder Anomaly Detection](EXP-002_harder_anomalies.md)
- [Notebook 04 — Feature Ablation](../../notebooks/04_feature_ablation.ipynb)

## Reference

Liu, F. T., Ting, K. M., & Zhou, Z.-H. (2008). *Isolation Forest*. IEEE International Conference on Data Mining. https://doi.org/10.1109/ICDM.2008.17
