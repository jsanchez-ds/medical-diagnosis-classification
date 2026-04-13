# Medical Diagnosis Classification — Breast Cancer Detection

Binary classification on the **Wisconsin Breast Cancer** dataset (569 records, 30 features) to distinguish malignant from benign tumors. The analysis compares **SVM**, **Decision Tree** and **Naive Bayes** under two class-imbalance strategies (under-sampling and over-sampling), with hyperparameter tuning via GridSearchCV and 5-fold cross-validation.

[![Render Notebook](https://github.com/jsanchez-ds/medical-diagnosis-classification/actions/workflows/render.yml/badge.svg)](https://github.com/jsanchez-ds/medical-diagnosis-classification/actions/workflows/render.yml)
[![View Report](https://img.shields.io/badge/View_Report-GitHub_Pages-2ea44f?logo=github)](https://jsanchez-ds.github.io/medical-diagnosis-classification/)
![Python](https://img.shields.io/badge/Python-3.11-3776AB?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-SVM%20%7C%20DT%20%7C%20NB-F7931E?logo=scikitlearn&logoColor=white)

> **[→ Read the full rendered report](https://jsanchez-ds.github.io/medical-diagnosis-classification/)** — every plot, table, and model output, no installation required.

---

## Research Question

> Can we reliably classify breast tumors as malignant or benign using cell-nucleus measurements from fine-needle aspirates, and how sensitive are the results to the class-imbalance correction strategy?

---

## Dataset

The **Wisconsin Diagnostic Breast Cancer (WDBC)** dataset contains 569 observations with 30 real-valued features computed from digitized images of fine-needle aspirates. Each feature describes characteristics of cell nuclei (radius, texture, perimeter, area, smoothness, compactness, concavity, concave points, symmetry, fractal dimension) with mean, standard error and worst-case statistics.

- **357 benign** (62.7%) / **212 malignant** (37.3%)
- Source: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Breast+Cancer+Wisconsin+(Diagnostic))

---

## Methodology

### 1. EDA
- Descriptive statistics and missing-value check
- Correlation heatmap → feature selection (drop 14 highly-correlated features)
- Class distribution analysis

### 2. Preprocessing
- MinMaxScaler normalization to [0, 1]
- Train/test split (80/20, stratified)

### 3. Class Imbalance Handling
| Strategy | Approach | Effect |
|---|---|---|
| **Under-sampling** | `RandomUnderSampler` | Reduces majority class to match minority |
| **Over-sampling** | `RandomOverSampler` | Duplicates minority class to match majority |

### 4. Models (GridSearchCV + 5-fold CV)
| Model | Under-sampling CV | Over-sampling CV |
|---|---|---|
| **SVM** | **97.6%** | **98.1%** |
| Decision Tree | 92.9% | 93.7% |
| Naive Bayes | 92.0% | 92.7% |

### 5. Evaluation
- ROC curves and AUC scores (SVM AUC: 0.992 / 0.996)
- Confusion matrices on held-out test set
- Classification reports (precision, recall, F1)

---

## Key Findings

1. **SVM dominates** across both imbalance strategies with 97% test accuracy and AUC > 0.99.
2. **Over-sampling slightly outperforms under-sampling** — preserving all majority-class information yields marginally better generalization.
3. **Feature selection via correlation** reduced dimensionality from 30 to 16 features without performance loss.
4. **Decision Tree and Naive Bayes** achieve ~93% accuracy but are substantially less robust than SVM on this dataset.

---

## Tech Stack

`Python` `scikit-learn` `imbalanced-learn` `XGBoost` `seaborn` `matplotlib` `pandas`

---

## Project Structure

```
medical-diagnosis-classification/
├── README.md
├── analysis.ipynb                  # Full analysis notebook
├── data/
│   ├── README.md                   # Schema reference
│   └── data.csv                    # Wisconsin WDBC dataset (569 rows)
└── .github/workflows/
    └── render.yml                  # CI: execute notebook → HTML → Pages
```

---

## How to Reproduce

### Option A — Read the rendered report (no install)

Just open <https://jsanchez-ds.github.io/medical-diagnosis-classification/>. The CI re-executes and re-renders the notebook on every push to `main`.

### Option B — Run locally

```bash
pip install pandas numpy scikit-learn matplotlib seaborn xgboost imbalanced-learn jupyter
jupyter notebook analysis.ipynb
```

---

## Author

**Jonathan Sánchez**
- GitHub: [@jsanchez-ds](https://github.com/jsanchez-ds)
- Universidad de Chile — Industrial Engineering
