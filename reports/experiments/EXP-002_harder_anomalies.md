# EXP-002 — Isolation Forest Under More Challenging Conditions

## 1. Research Question

How does Isolation Forest perform when anomalous accounts exhibit different degrees of deviation from normal account behavior?

## 2. Hypothesis

Isolation Forest will detect extreme anomalies more reliably than subtle anomalies that partially overlap with normal account behavior.

## 3. Dataset

A synthetic dataset containing 1,000 accounts:

| Account type | Count |
|---|---:|
| Normal | 940 |
| Extreme anomaly | 30 |
| Subtle anomaly | 30 |

**Features:** Number of devices, number of transactions within 24 hours, and number of connected accounts.

The dataset was designed to investigate different anomaly-detection difficulties. It does not contain actual financial transactions or graph edges.

## 4. Methodology

Isolation Forest was trained using the following configuration:

| Parameter | Value |
|---|---|
| `n_estimators` | 100 |
| `max_samples` | auto |
| `contamination` | 0.06 |
| `random_state` | 42 |
| Train/test split | 80/20, stratified by anomaly type |

The model was trained without anomaly labels. Synthetic labels were used only to construct the stratified split and evaluate predictions.

## 5. Results

On the held-out test set of 200 accounts:

| Metric | Result |
|---|---:|
| Precision | 0.846 |
| Recall | 0.917 |
| F1-score | 0.880 |
| Accuracy | 0.985 |
| False Positives | 2 |
| False Negatives | 1 |

### Performance by Anomaly Type

| Type | Total | Detected | Detection rate |
|---|---:|---:|---:|
| Extreme anomalies | 6 | 6 | 100% |
| Subtle anomalies | 6 | 5 | 83.3% |
| Normal accounts | 188 | 2 | 1.06% |

For normal accounts, the detection rate represents the false positive rate.

## 6. Error Analysis

Two normal accounts were incorrectly flagged:

- **ACC_00251:** 6 devices, 3 transactions, 4 connected accounts.
- **ACC_00641:** 8 devices, 10 transactions, 5 connected accounts.

Both accounts exhibited relatively high device counts compared with typical normal accounts.

One subtle anomaly was missed:

- **ACC_00619:** 3 devices, 14 transactions, 7 connected accounts.

Its features were relatively close to normal account behavior, potentially making it more difficult to isolate.

These are plausible interpretations rather than verified feature-level explanations.

## 7. Key Findings

The results support the initial hypothesis: extreme anomalies were easier to detect than subtle anomalies in this synthetic experiment.

The experiment also demonstrates that a model can achieve high overall accuracy while still producing false positives and missing anomalous accounts.

This highlights the importance of examining class-specific metrics and individual prediction errors.

## 8. Limitations

- The dataset is entirely synthetic and deliberately constructed.
- Only 12 anomalous accounts were included in the test set.
- The contamination setting matched the known synthetic anomaly proportion.
- The results have not been validated across multiple random seeds or independently generated datasets.
- The model used numerical account-level features rather than actual graph relationships.
- Detecting statistical anomalies is not equivalent to identifying confirmed fraud.

## 9. Next Steps

The next experiment will investigate feature ablation to understand how the removal of individual features affects anomaly detection performance.

Future experiments will explore more realistic transaction datasets, graph-based features, traditional supervised machine learning, and Graph Neural Networks.

## 10. References

Liu, F. T., Ting, K. M., & Zhou, Z.-H. (2008). *Isolation Forest*. IEEE International Conference on Data Mining. https://doi.org/10.1109/ICDM.2008.17

## Related Notebook

[03 — Harder Anomaly Detection](../../notebooks/03_anomaly_simulation.ipynb)
