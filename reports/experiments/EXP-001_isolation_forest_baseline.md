# EXP-001 — Isolation Forest Baseline

## 1. Research Question

Can Isolation Forest identify anomalous account behavior using numerical features without requiring anomaly labels during model training?

## 2. Dataset

Synthetic Account Dataset v1:

- 1,000 accounts
- 970 normal accounts
- 30 synthetic anomalies

Input features:

- `num_devices`
- `num_transactions_24h`
- `connected_accounts`

The synthetic anomaly label was excluded from model training.

## 3. Methodology

The model was configured with:

| Parameter | Value |
|---|---|
| Algorithm | Isolation Forest |
| `n_estimators` | 100 |
| `max_samples` | auto |
| `contamination` | 0.03 |
| `random_state` | 42 |
| Train/test split | 80/20, stratified |

The training set contained 800 accounts, and the test set contained 200 accounts, including six synthetic anomalies.

## 4. Test Results

| Metric | Result |
|---|---:|
| Precision | 1.000 |
| Recall | 1.000 |
| F1-score | 1.000 |
| Accuracy | 1.000 |
| True Positives | 6 |
| True Negatives | 194 |
| False Positives | 0 |
| False Negatives | 0 |

The model correctly identified all six synthetic anomalies in the held-out test set.

## 5. Threshold Sensitivity

Different contamination settings produced the following results:

| Contamination | Precision | Recall | F1-score |
|---|---:|---:|---:|
| 0.01 | 1.000 | 0.500 | 0.667 |
| 0.02 | 1.000 | 0.833 | 0.909 |
| 0.03 | 1.000 | 1.000 | 1.000 |
| 0.05 | 0.600 | 1.000 | 0.750 |
| 0.10 | 0.400 | 1.000 | 0.571 |

Lower contamination settings resulted in missed anomalies. Higher settings increased false positives.

## 6. Key Learnings

- Isolation Forest detects anomalies through random partitioning and isolation path lengths.
- Anomaly labels are not required during model fitting.
- The contamination parameter primarily determines the threshold for identifying anomalies.
- Precision and Recall are sensitive to threshold selection.
- Anomaly scores are not calibrated fraud probabilities.
- Perfect performance on simple synthetic data does not imply real-world fraud detection effectiveness.

## 7. Limitations

- The dataset was deliberately constructed with easily distinguishable anomalies.
- The contamination parameter matched the known synthetic anomaly rate.
- Only six anomalous accounts were included in the test set.
- The threshold sensitivity analysis reused test labels for exploratory comparisons.
- Model performance has not been validated on independently generated or real financial data.
- No actual graph relationships were modeled.

## 8. Personal Research Reflection

The initial results demonstrated that Isolation Forest can successfully identify clearly separated synthetic anomalies.

However, achieving perfect Precision and Recall raised an important methodological question: was the model genuinely robust, or was the dataset simply too easy?

The threshold sensitivity experiment showed that changing the decision threshold could substantially affect Precision and Recall.

This motivated the next experiment, which introduced more subtle anomalies with overlapping feature distributions.

## 9. Next Steps

Introduce more challenging synthetic anomalies and investigate how model performance changes when anomalous behavior is less extreme.

## Related Notebook

[02 — Isolation Forest Baseline](../../notebooks/02_isolation_forest.ipynb)

## Reference

Liu, F. T., Ting, K. M., & Zhou, Z.-H. (2008). *Isolation Forest*. IEEE ICDM. https://doi.org/10.1109/ICDM.2008.17
