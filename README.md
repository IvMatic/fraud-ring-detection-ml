# Fraud Ring Detection — Graph Analytics & Machine Learning

**An experimental Data Science project exploring anomaly detection, graph-based features, traditional machine learning, and Graph Neural Networks for financial fraud detection.**

## Project Overview

This project investigates how unusual financial account behavior and relationships between entities can be used to identify potential fraud risks.

The project follows an incremental, experiment-driven approach, starting with unsupervised anomaly detection and progressing toward graph analytics, supervised machine learning, and Graph Neural Networks.

The objective is not only to develop models, but also to understand their behavior, evaluate their limitations, and document the reasoning behind methodological decisions.

## Research Questions

- Can Isolation Forest identify anomalous account behavior without labeled fraud examples?
- How does the choice of anomaly detection threshold affect Precision and Recall?
- Which account-level and graph-based features provide useful anomaly signals?
- Can graph-based features improve traditional machine learning models?
- Do Graph Neural Networks offer advantages over feature-based approaches?


## Project Roadmap

| Phase | Focus | Status |
|---|---|---|
| 01 | Synthetic Data Exploration & EDA | Completed |
| 02 | Isolation Forest Baseline | Completed |
| 03 | Harder Anomalies & Error Analysis | Completed |
| 04 | Feature Ablation Study | Completed |
| 05 | Anomaly Detection Model Comparison | Planned |
| 06 | Transaction Fraud Detection Dataset | Planned |
| 07 | Memgraph & Graph Feature Engineering | Planned |
| 08 | Traditional ML — XGBoost / Random Forest | Planned |
| 09 | Graph Neural Networks | Planned |
| 10 | Ensemble Strategies & Model Comparison | Planned |


## Experiments and Results

| ID | Experiment | Dataset | F1-score |
|---|---|---|---:|
| EXP-001 | Isolation Forest Baseline | Synthetic v1 | 1.000 |
| EXP-002 | Harder Anomaly Detection | Synthetic v2 | 0.880 |
| EXP-003 | Feature Ablation — All Features | Synthetic v2 | 0.880 |
| EXP-003 | Feature Ablation — Without Devices | Synthetic v2 | 0.909 |

All results are from small, held-out synthetic
test sets. They are not real-world fraud detection
performance estimates.

### Experiment Notebooks

- [01 — Exploratory Data Analysis](notebooks/01_eda.ipynb)
- [02 — Isolation Forest Baseline](notebooks/02_isolation_forest.ipynb)
- [03 — Harder Anomaly Detection](notebooks/03_anomaly_simulation.ipynb)
- [04 — Feature Ablation](notebooks/04_feature_ablation.ipynb)


### Experiment Reports

| ID | Experiment | Report |
|---|---|---|
| EDA-001 | Exploratory Data Analysis | [Read Report](reports/experiments/EDA-001_exploratory_data_analysis.md) |
| EXP-001 | Isolation Forest Baseline | [Read Report](reports/experiments/EXP-001_isolation_forest_baseline.md) |
| EXP-002 | Harder Anomaly Detection | [Read Report](reports/experiments/EXP-002_harder_anomalies.md) |
| EXP-003 | Feature Ablation Study | [Read Report](reports/experiments/EXP-003_feature_ablation.md) |


### Main Findings

**1. Easy anomalies can produce misleadingly
strong results.**

The initial model achieved F1 = 1.000 because
the synthetic anomalies were deliberately extreme.

**2. Subtle anomalies are more challenging.**

On Dataset v2, Isolation Forest achieved
F1 = 0.880 and missed one subtle anomaly.

**3. Feature selection changes model behavior.**

Removing `num_devices` improved overall F1
to 0.909 but reduced subtle anomaly recall
from 0.833 to 0.667.

**4. Individual error analysis matters.**

All four feature configurations missed
the same subtle anomaly, ACC_00619.

**5. Graph-based information remains a hypothesis.**

The current dataset has no actual graph edges.
Future experiments will investigate whether
graph features provide additional detection value.


## Technology Stack

Python · Pandas · NumPy · Scikit-learn · Matplotlib · Seaborn · Google Colab

Planned: Memgraph · XGBoost · PyTorch · PyTorch Geometric

## Reproducibility

Experiments are developed in Google Colab and version-controlled through GitHub.

Synthetic datasets are used for initial experiments. Data generation scripts, dependencies, and detailed execution instructions will be added as the project progresses.

## Project Scope and Disclaimer

This is an independent educational and research portfolio project, not a production-ready financial fraud detection system.

Initial experiments use synthetic data. Anomaly detection results are not equivalent to confirmed fraud detection.

No private banking or company data is included.
