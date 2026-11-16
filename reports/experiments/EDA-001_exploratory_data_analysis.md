# EDA-001 — Exploratory Data Analysis

## 1. Objective

Explore a synthetic account-level dataset, assess data quality, investigate feature distributions, and identify potential challenges for anomaly detection.

## 2. Dataset

The dataset consists of 1,000 synthetic accounts:

- 970 normal accounts
- 30 artificially generated anomalous accounts.

Three numerical features were investigated:

- `num_devices`
- `num_transactions_24h`
- `connected_accounts`

The dataset also includes an account identifier and a synthetic anomaly label.

## 3. Data Quality

Initial checks showed:

- 1,000 observations
- No missing values
- No duplicate account identifiers
- No negative feature values

The synthetic anomaly proportion is 3%.

## 4. Descriptive Statistics

| Feature | Mean | Median | Maximum |
|---|---:|---:|---:|
| Number of devices | 2.324 | 2 | 19 |
| Transactions in 24 hours | 10.663 | 8 | 149 |
| Connected accounts | 4.142 | 3 | 59 |

All three numerical features have higher means than medians, consistent with the influence of a small group of high-value observations.

## 5. Correlation Analysis

The full dataset exhibited relatively strong positive correlations:

| Feature pair | Correlation |
|---|---:|
| Devices — Transactions | 0.70 |
| Devices — Connected accounts | 0.70 |
| Transactions — Connected accounts | 0.87 |

However, correlations among normal accounts were approximately zero:

| Feature pair | Correlation |
|---|---:|
| Devices — Transactions | 0.02 |
| Devices — Connected accounts | -0.03 |
| Transactions — Connected accounts | -0.04 |

This indicates that the strong overall correlations were largely driven by differences between the synthetically generated account groups.

## 6. Key Learnings

- Exploratory Data Analysis helps identify the structure and limitations of a dataset before model training.
- Aggregated correlations can be misleading when distinct populations are combined.
- Synthetic data generation can create artificial relationships between features.
- Feature distributions strongly influence anomaly detection difficulty.

## 7. Limitations

- The dataset is entirely synthetic.
- Anomalies were deliberately generated with extreme feature values.
- There are no actual graph edges or transaction histories.
- The account features are simplified numerical representations.
- Findings cannot be generalized to real financial fraud datasets.

## 8. Next Steps

Train an Isolation Forest baseline using the three numerical features and evaluate its ability to detect the synthetic anomalies.

## Related Notebook

[01 — Exploratory Data Analysis](../../notebooks/01_eda.ipynb)
