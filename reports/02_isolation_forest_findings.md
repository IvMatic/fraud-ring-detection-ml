# Isolation Forest — Baseline Experiment

## 1. Objective

Evaluate whether Isolation Forest can detect anomalous account behavior using synthetic account-level features.

## 2. Dataset

The experiment uses 1,000 synthetic accounts:

- 970 normal accounts
- 30 artificially generated anomalous accounts
- 3 numerical features: number of devices, transactions in 24 hours, and connected accounts

Anomalous accounts were deliberately generated with substantially higher feature values than normal accounts.

## 3. Methodology

An Isolation Forest model was trained using:

- 100 estimators
- `max_samples="auto"`
- `random_state=42`
- Initial contamination setting of 0.03

An 80/20 stratified train/test split was used, resulting in 800 training accounts and 200 test accounts.

The anomaly labels were excluded from model training.

## 4. Results

At `contamination=0.03`, the model achieved:

| Metric | Test result |
|---|---:|
| Precision | 1.00 |
| Recall | 1.00 |
| F1-score | 1.00 |
| True Positives | 6 |
| False Positives | 0 |
| False Negatives | 0 |
| True Negatives | 194 |

### Contamination Sensitivity

| Contamination | Precision | Recall | F1 |
|---|---:|---:|---:|
| 0.01 | 1.00 | 0.50 | 0.667 |
| 0.02 | 1.00 | 0.833 | 0.909 |
| 0.03 | 1.00 | 1.00 | 1.000 |
| 0.05 | 0.60 | 1.00 | 0.750 |
| 0.10 | 0.40 | 1.00 | 0.571 |

## 5. Key Findings

- Isolation Forest successfully identified all six synthetic anomalies in the test set at the initial contamination threshold.
- Lower contamination settings reduced recall.
- Higher contamination settings increased false positives and reduced precision.
- The synthetic anomalies were intentionally easy to separate from normal accounts.

## 6. Limitations

- The dataset is synthetic and does not represent real financial fraud.
- The anomaly rate was known in advance and influenced the initial threshold selection.
- Only six anomalous accounts were present in the test set.
- The contamination sensitivity experiment reused test labels to compare thresholds; therefore, the threshold comparison is exploratory rather than a final unbiased model-selection procedure.
- Graph relationships were represented only through aggregated numerical features, not modeled directly.

## 7. Next Steps

1. Introduce more realistic fraud detection datasets.
2. Establish separate training, validation, and test sets.
3. Evaluate Precision@K and Precision–Recall AUC.
4. Explore graph-based features using Memgraph.
5. Compare Isolation Forest with supervised models and eventually Graph Neural Networks.

## Reference

Liu, F. T., Ting, K. M., & Zhou, Z.-H. (2008). *Isolation Forest*. IEEE International Conference on Data Mining. https://doi.org/10.1109/ICDM.2008.17
