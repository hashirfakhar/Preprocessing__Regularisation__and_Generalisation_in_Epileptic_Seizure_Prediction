# Epileptic Seizure Prediction: A Comparative Machine Learning Study

Epileptic seizure prediction is a critical clinical problem where machine learning can deliver significant value. This project investigates how preprocessing choices, regularisation strategies, and class imbalance handling affect the generalisation of predictive models across three distinct EEG-based datasets.

---

## Project Overview

Using logistic regression as a controlled baseline, this study provides a transparent platform to isolate the individual contributions of different methodological choices. The repository explores the interaction between step ordering and model capacity to establish practical guidelines for clinical EEG classification.

### Key Research Contributions
* **Systematic Preprocessing**: Comparison of pipelines differing in step ordering to evaluate their impact on performance.
* **Regularisation Analysis**: Benchmarking L1, L2, and Elastic Net penalties with a focus on sparsity and feature selection.
* **Imbalance Strategies**: Evaluation of SMOTE, Random Undersampling, and Class Weighting to improve minority-class sensitivity.

---

## Methodology

### 1. Dataset Collection
The study utilizes three publicly available datasets to ensure diversity in size and class balance:
* **Bonn University EEG**: Single-channel raw signal data representing the time-series paradigm.
* **ADHD EEG 19-Channel**: Multi-electrode recordings providing pre-extracted features and a near-balanced distribution.
* **UCI Seizure Recognition**: A high-dimensional reference point with 178 statistical features per segment.

### 2. Preprocessing Pipelines
The project demonstrates that step ordering is not arbitrary. Two primary pipelines were designed:
* **Pipeline A**: Normalisation -> Noise Removal -> Feature Selection.
* **Pipeline B**: Standard Scaling -> Principal Component Analysis (PCA).

### 3. Regularisation Benchmarking
Three penalties were examined to balance the bias-variance tradeoff:
* **L2 (Ridge)**: Shrinks all coefficients towards zero but preserves all features.
* **L1 (Lasso)**: Induces sparsity by driving irrelevant feature coefficients exactly to zero.
* **Elastic Net**: Combines both properties to maintain grouping stability with sparsity.

---

## Core Findings

* **Ordering Matters**: Scaling must precede feature selection and PCA to ensure that statistical measures like F-statistics and covariance are computed on comparable scales.
* **L1 Superiority**: L1 regularisation produces the best overall generalisation on high-dimensional data by effectively identifying the most discriminative features.
* **Optimal Imbalance Handling**: Class Weighting is the most practical first-line strategy, improving the seizure class F1-score without the risks of synthetic data generation or information loss.
* **Best Combination**: The most effective configuration across datasets is Scale -> Select -> PCA combined with L1 regularisation and Class Weighting.

---

## Evaluation Metrics

Models are assessed using metrics that account for severe class imbalance:
* **F1-Score**: Harmonic mean of precision and recall.
* **PR-AUC**: The primary metric for measuring discrimination ability across all thresholds.
* **Sparsity Analysis**: Quantification of coefficients driven to near-zero (below 10^-6).
