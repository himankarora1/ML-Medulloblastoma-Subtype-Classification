# Machine Learning-Based Classification of Medulloblastoma Subtypes

Classifies medulloblastoma molecular subgroups (**G3, G4, SHH, WNT**) from gene expression microarray data, comparing multiple feature selection strategies and machine learning models to identify what best separates these clinically distinct subtypes.

## Background

Medulloblastoma is classified into four molecular subgroups with distinct clinical outcomes and treatment implications. This project uses gene expression data (54,676 probe-level features per sample, Affymetrix microarray) to build classifiers that distinguish between subgroups — a classic high-dimensional, small-sample-size bioinformatics problem.

## Pipeline

### 1. Data Preprocessing & Feature Selection
Since the raw dataset has far more features (~54,676 genes) than samples, several dimensionality reduction strategies are compared:
- **Variance Thresholding** — remove low-variance/uninformative genes
- **LASSO Regression** (L1) — sparse feature selection across several alpha values
- **Random Forest feature importance** — tree-based feature selection across different ensemble sizes
- **PCA** — dimensionality reduction to principal components

Each strategy produces its own reduced dataset, saved to `data/preprocessed/` (generated automatically when the notebook runs — not included in the repo, since it's fully reproducible from the raw data).

### 2. Model Training & Evaluation
Four models are trained and compared **across every preprocessed dataset variant**:
- SVM (linear kernel, class-balanced)
- Random Forest
- XGBoost
- Logistic Regression (class-balanced)

Each is evaluated with accuracy, precision, recall, and F1-score (80/20 train/test split), with results aggregated to identify which combination of feature selection + model performs best.

## Tech Stack
- **Language:** Python
- **Core libraries:** scikit-learn, XGBoost, pandas, NumPy

## Getting Started

```bash
pip install -r requirements.txt
jupyter notebook main.ipynb
```

Run all cells top to bottom — Section 1 generates the preprocessed datasets from the raw data, Section 2 trains and evaluates all models on each.

## Repo Structure
```
├── main.ipynb                                                      # Full pipeline: preprocessing → training → evaluation
├── data/
│   └── medulloblastoma.tsv                                         # Raw gene expression data
├── Machine Learning-Based Classification of Medulloblastoma Using.pdf   # Full written report
└── requirements.txt
```

## Report
See the included PDF for full methodology, results tables, and discussion.
