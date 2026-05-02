# 📊 Customer Churn Prediction – End-to-End ML Pipeline


![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat-square)
![sklearn](https://img.shields.io/badge/scikit--learn-Pipeline-green?style=flat-square)
![joblib](https://img.shields.io/badge/Export-joblib-lightgrey?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

---

## 📌 Objective

Build a production-ready, reusable ML pipeline using the scikit-learn `Pipeline` API to predict whether a telecom customer will churn. The final pipeline is exported with `joblib` for drop-in deployment.

---

## 📂 Dataset

| Property | Details |
|----------|---------|
| Name | Telco Customer Churn |
| Source | [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn) |
| Records | 7,043 customers |
| Features | 19 (demographics, services, contract, charges) |
| Target | Churn (Yes / No) — ~26% positive rate |

---

## 🧠 Methodology / Approach

```
Raw CSV
    │
    ▼
ColumnTransformer
  ├── Numeric cols  →  SimpleImputer(median)  →  StandardScaler
  └── Categorical cols  →  SimpleImputer(mode)  →  OneHotEncoder
    │
    ▼
Model Training
  ├── Logistic Regression
  └── Random Forest  ←  Best performer
    │
    ▼
GridSearchCV  (5-fold StratifiedKFold · scoring = ROC-AUC)
    │
    ▼
Evaluate: Accuracy · F1 · ROC-AUC · PR Curve · Feature Importance
    │
    ▼
Export: joblib  →  churn_pipeline.joblib
```

### Hyperparameter Search Space

| Model | Parameter | Values Tried |
|-------|-----------|-------------|
| Logistic Regression | C | 0.01, 0.1, 1, 10 |
| Logistic Regression | solver | lbfgs, liblinear |
| Random Forest | n_estimators | 100, 200 |
| Random Forest | max_depth | None, 10, 20 |
| Random Forest | min_samples_split | 2, 5 |

---

## 📊 Key Results

| Model | Accuracy | F1-Score | ROC-AUC |
|-------|----------|----------|---------|
| Logistic Regression | ~80% | ~0.60 | ~0.85 |
| **Random Forest** | **~82%** | **~0.62** | **~0.87** |

---

## 🔍 Observations

1. **Contract type** is the strongest single predictor — month-to-month customers churn 3× more than annual subscribers
2. **Tenure** is strongly inversely correlated with churn — customers past 24 months rarely leave
3. Class imbalance (~26% churn rate) makes ROC-AUC and F1 more informative than raw accuracy
4. The entire preprocessing + inference chain is encapsulated in one `.joblib` file — zero code changes needed for new data
5. Gradient Boosting can push AUC to ~0.90 with further tuning (included as bonus in notebook)

---

## 🗂️ Project Structure

```
churn-prediction-pipeline/
├── task2_churn_pipeline.ipynb     ← Main notebook
├── churn_pipeline.joblib          ← Exported production pipeline
├── outputs/
│   ├── task2_eda.png
│   └── task2_evaluation.png
├── requirements.txt
└── README.md
```

---

## ⚙️ Setup & Run

```bash
# 1. Clone the repo
git clone https://github.com/engineermuhammadtalha/churn-prediction-pipeline
cd churn-prediction-pipeline

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the notebook
jupyter notebook task2_churn_pipeline.ipynb

# 4. Use the exported pipeline on new data
python -c "
import joblib, pandas as pd
pipeline = joblib.load('churn_pipeline.joblib')
df = pd.read_csv('new_customers.csv')
print(pipeline.predict_proba(df)[:, 1])   # churn probability
"
```

---

## 🛠️ Tech Stack

`Python` · `scikit-learn` · `pandas` · `NumPy` · `Matplotlib` · `Seaborn` · `joblib`
