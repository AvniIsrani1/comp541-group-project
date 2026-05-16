# Phishing URL Detection - COMP 541 Group Project

**The Mining Company (Group 3)** | California State University, Northridge | Spring 2026

A machine learning pipeline for detecting phishing URLs using the PhiUSIIL Phishing URL Dataset from the UCI Machine Learning Repository. Final deployed model is an MLP achieving F1 = 0.9997 on a held-out test set.

## Team

Isae Arreola, Gus Axelson, Fotios Bampouridis, Rene Barseghian, Avni Israni, Alberto Sandoval, Arrshan Saravanabavanandam

## Dataset

PhiUSIIL Phishing URL Dataset - 235,795 URLs (134,850 legitimate, 100,945 phishing), 55 features.
Source: https://archive.ics.uci.edu/dataset/967/phiusiil+phishing+url+dataset

The dataset loads directly via the `ucimlrepo` Python library (ID = 967), so no manual download is needed.

## Repo Contents

| File | Description |
|---|---|
| `Assignment2_COMP541.ipynb` | Statistical descriptions: central tendency, dispersion, five-number summary, skewness, correlation analysis |
| `Assignment3_COMP541.ipynb` | Exploratory visualizations: histograms, KDEs, boxplots, scatter, hexbin, correlation heatmap |
| `Assignment4_COMP541.ipynb` | Preprocessing pipeline: cleaning, transformation, feature selection, feature engineering, train/val/test split |
| `Assignment5_COMP541.ipynb` | Modeling, evaluation, deployment: six classifiers compared (LogReg, RBF SVM, KNN, RF, HistGB, MLP), ablations, SHAP analysis |

## How to Run

The notebooks are designed to run on Google Colab with the default Python 3 + T4 GPU environment. To run locally:

```bash
pip install ucimlrepo pandas numpy scikit-learn matplotlib seaborn scipy tensorflow shap imbalanced-learn
```

Each notebook is self-contained and re-fetches the dataset from UCI on first cell run. Run notebooks in order (A1 -> A5) for a full project walkthrough, or jump directly to A5 for the modeling and evaluation results.

## Reproducibility

All notebooks use fixed random seeds (42, 7, 123 for the three-seed runs in Assignment 5). Stochastic components in scikit-learn, NumPy, and TensorFlow are seeded explicitly so results match across re-runs.

## Final Model

MLP without `URLSimilarityIndex` and without PCA. Architecture: 128 -> dropout 0.2 -> 64 -> dropout 0.2 -> 32 -> sigmoid. Adam optimizer, learning rate 0.001, binary cross-entropy loss, batch size 256, early stopping with patience 3.

Test set performance (mean ± std over 3 seeds):
- F1: 0.9997 +/- 0.0001
- Recall: 0.9996 +/- 0.0000
- Precision: 0.9997 +/- 0.0001
- ROC AUC: 1.0000

## References

Prasad, A. and Chandra, S. (2024). "PhiUSIIL: A diverse security profile empowered phishing URL detection framework based on similarity index and incremental learning." *Computers & Security*, Vol. 136. https://doi.org/10.1016/j.cose.2023.103545
