<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10-3776AB?logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/scikit--learn-1.x-F7931E?logo=scikit-learn&logoColor=white" alt="scikit-learn" />
  <img src="https://img.shields.io/badge/Pandas-2.x-150458?logo=pandas&logoColor=white" alt="Pandas" />
  <img src="https://img.shields.io/badge/Kaggle-Dataset-20BEFF?logo=kaggle&logoColor=white" alt="Kaggle" />
  <img src="https://img.shields.io/badge/Samples-1M-green" alt="1M Samples" />
</p>

# 🌾 Harvest Vision

**A machine learning pipeline for predicting crop yield classes** using an ensemble of classifiers on a 1,000,000-sample agricultural dataset. The project compares six models — from Decision Trees to a Stacking Classifier — with full preprocessing, class balancing, hyperparameter tuning, and learning-curve analysis.

> **Domain:** Precision Agriculture & Crop Yield Prediction  
> **Task:** Binary classification (High / Low yield) via median-split on tons-per-hectare  
> **Team:** [Mohamed Ayman El-Khatib](https://www.kaggle.com/code/mohamedaymanelkhatib/harvest-vision), Youssef Mohamed & Lauren Osama

---

## Problem Statement

Accurately forecasting crop yield helps farmers, agribusinesses, and policymakers make data-driven decisions about resource allocation, irrigation planning, and food security. **Harvest Vision** tackles this by converting a regression target (yield in tons/hectare) into a classification problem and benchmarking multiple ML approaches to find the best predictor.

---

## Dataset

| Property | Value |
|----------|-------|
| **Source** | [Agriculture Crop Yield — Kaggle](https://www.kaggle.com/datasets/samuelotiattakorah/agriculture-crop-yield) |
| **Total Samples** | 1,000,000 |
| **Working Sample** | 100,000 (stratified random) |
| **Features** | 9 (4 numerical, 5 categorical) |
| **Target** | `Yield_tons_per_hectare` → binary class (High / Low) |

### Features

| Feature | Type | Description |
|---------|------|-------------|
| `Region` | Categorical | Geographical location of data collection |
| `Soil_Type` | Categorical | Soil classification (sandy, clay, loamy, etc.) |
| `Crop` | Categorical | Crop type (wheat, corn, rice, etc.) |
| `Weather_Condition` | Categorical | Weather summary during the growing period |
| `Irrigation_Used` | Boolean | Whether irrigation was applied |
| `Fertilizer_Used` | Boolean | Whether fertilizer was applied |
| `Rainfall_mm` | Numerical | Total rainfall in millimeters |
| `Temperature_Celsius` | Numerical | Average temperature in °C |
| `Days_to_Harvest` | Numerical | Days between planting and harvesting |

---

## Methodology

### 1. Exploratory Data Analysis & Preprocessing

- **Distribution Analysis** — Histograms with KDE and box plots for all numerical features to assess normality and spread.
- **Outlier Removal** — IQR-based filtering on `Rainfall_mm`, `Temperature_Celsius`, `Days_to_Harvest`, and `Yield_tons_per_hectare`.
- **Encoding** — Label encoding for categorical variables (`Region`, `Soil_Type`, `Crop`, `Weather_Condition`).
- **Feature Scaling** — `StandardScaler` applied to all features post-split.
- **Class Balancing** — SMOTE oversampling on the training set to handle class imbalance.
- **Correlation Analysis** — Pearson correlation heatmap to identify feature relationships and guide feature selection.

### 2. Models Trained & Evaluated

| # | Model | Key Configuration |
|---|-------|-------------------|
| 1 | **Decision Tree** | `max_depth=3`, balanced via SMOTE |
| 2 | **Logistic Regression** | `max_iter=1000`, L2 regularization |
| 3 | **Linear SVM** | `LinearSVC`, `max_iter=1000` |
| 4 | **K-Nearest Neighbors** | `GridSearchCV` over `k ∈ {3, 5, 7}` and `weights ∈ {uniform, distance}`, `ball_tree` algorithm |
| 5 | **Random Forest** | 100 estimators, parallelized (`n_jobs=-1`) |
| 6 | **Stacking Classifier** | Random Forest + Linear SVM → Logistic Regression meta-learner |

### 3. Evaluation

- **Metrics:** Accuracy, Precision, Recall, F1-score (weighted), and per-class classification reports.
- **Confusion Matrices** for every model to inspect true/false positive rates.
- **Learning Curves** (3-fold CV) to diagnose overfitting vs. underfitting across all models.

---

## Tech Stack

| Layer | Technologies |
|-------|-------------|
| **Language** | Python 3.10 |
| **ML Framework** | scikit-learn (Decision Tree, Logistic Regression, SVM, KNN, Random Forest, Stacking) |
| **Data Handling** | Pandas · NumPy |
| **Visualization** | Matplotlib · Seaborn |
| **Class Balancing** | imbalanced-learn (SMOTE) |
| **Hyperparameter Tuning** | GridSearchCV (3-fold CV) |
| **Environment** | Jupyter Notebook · Kaggle Kernels |

---

## Quick Start

### Prerequisites

| Tool | Required For |
|------|-------------|
| Python 3.10+ | Runtime |
| Jupyter Notebook | Running the notebook |
| pip | Installing dependencies |

### Setup

```bash
# Clone the repository
git clone https://github.com/your-username/Harvest-Vision.git
cd Harvest-Vision

# Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn graphviz pydotplus

# Launch the notebook
jupyter notebook harvest-vision.ipynb
```

### Running

1. Open `harvest-vision.ipynb` in Jupyter Notebook
2. Update the dataset path in the data loading cell to point to your local copy of [`crop_yield.csv`](https://www.kaggle.com/datasets/samuelotiattakorah/agriculture-crop-yield)
3. **Run All Cells** — the pipeline will preprocess, train, visualize, and evaluate automatically
4. Generated plots are saved to the working directory

---

## Project Structure

```
Harvest-Vision/
├── harvest-vision.ipynb    # Main notebook — full ML pipeline
└── README.md               # This file
```

---

## Key Takeaways

- **Ensemble methods** (Random Forest, Stacking) consistently outperform single models on this dataset.
- **SMOTE** is critical — without class balancing, models exhibit strong bias toward the majority class.
- **KNN** benefits significantly from hyperparameter tuning (`distance` weighting over `uniform`).
- **Learning curves** confirm that most models have converged and do not benefit from additional training data beyond ~60k samples.
- **Feature correlation** analysis reveals that no single feature dominates yield prediction — the problem is inherently multi-variate.
