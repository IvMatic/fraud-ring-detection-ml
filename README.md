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
| 01 | Synthetic data exploration and EDA | Completed |
| 02 | Isolation Forest baseline | Completed |
| 03 | Harder anomaly detection experiments | Planned |
| 04 | Realistic transaction datasets | Planned |
| 05 | Memgraph and graph feature engineering | Planned |
| 06 | Traditional machine learning | Planned |
| 07 | Graph Neural Networks | Planned |
| 08 | Model comparison and ensemble strategies | Planned |

## Initial Findings

The first Isolation Forest experiment achieved perfect Precision, Recall, and F1-score on a small, held-out synthetic test dataset.

However, the synthetic anomalies were deliberately constructed to be clearly distinguishable from normal accounts. These results should not be interpreted as evidence of real-world fraud detection performance.

Threshold sensitivity experiments also demonstrated the trade-off between detecting more anomalies and generating false positives.

See the experiment reports and notebooks for detailed methodology and limitations.

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
