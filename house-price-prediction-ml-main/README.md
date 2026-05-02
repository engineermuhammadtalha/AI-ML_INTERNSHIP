# 🏠 House Price Prediction


A regression-based machine learning model that predicts house prices using property features such as location, size, income level, and age.

---

## 🎯 Objective

Preprocess real estate data, engineer meaningful features, and train regression models to accurately predict property prices — evaluating them with MAE, RMSE, and R².

---

## 📂 Dataset

- **Primary:** California Housing Dataset (built into `scikit-learn` — no download needed)
- **Alternative:** [Kaggle House Prices Dataset](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques) (`train.csv`)

### Features Used

| Feature | Description |
|---|---|
| `MedInc` | Median income in block group |
| `HouseAge` | Median house age |
| `AveRooms` | Average number of rooms per household |
| `AveBedrms` | Average number of bedrooms per household |
| `Population` | Block group population |
| `AveOccup` | Average household occupancy |
| `Latitude` | Geographic latitude |
| `Longitude` | Geographic longitude |
| `RoomsPerHousehold` | Engineered: AveRooms / AveOccup |
| `BedroomsPerRoom` | Engineered: AveBedrms / AveRooms |

**Target:** `Price` — Median house value (in USD)

---

## 🛠️ Models Applied

| Model | Type |
|---|---|
| Linear Regression | Baseline parametric regression |
| Gradient Boosting Regressor | Ensemble boosting regression |

---

## 📊 Key Results

| Model | MAE | RMSE | R² |
|---|---|---|---|
| Linear Regression | *(run to see)* | *(run to see)* | *(run to see)* |
| Gradient Boosting | *(run to see)* | *(run to see)* | *(run to see)* |

> Gradient Boosting consistently achieves a higher R² and lower error by modeling non-linear feature interactions.

---

## 📉 Visualizations

- Price distribution (raw and log-transformed)
- Median income vs price scatter plot
- Geographic price heatmap (Latitude × Longitude)
- Correlation heatmap of all features
- Actual vs Predicted price (scatter, both models)
- Residual analysis plots
- Gradient Boosting feature importance chart

---

## 🚀 How to Run

```bash
# 1. Clone the repo
git clone https://github.com/engineermuhammadtalha/house-price-prediction-ml
cd house-price-prediction-ml

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch the notebook
jupyter notebook House_Price_Prediction.ipynb
```

> No dataset download required — the California Housing dataset loads automatically via `sklearn`.

---

## 📦 Requirements

```
pandas
numpy
scikit-learn
matplotlib
seaborn
jupyter
```

Install all at once:
```bash
pip install pandas numpy scikit-learn matplotlib seaborn jupyter
```

---

## 📁 Project Structure

```
house-price-prediction-ml/
│
├── House_Price_Prediction.ipynb   # Main notebook
├── requirements.txt                     # Dependencies
└── README.md                            # This file
```

---

## 💡 Key Learnings

- **Median Income** is the single strongest predictor of house price in California
- **Geographic location** (Latitude, Longitude) carries significant predictive power — coastal areas command premium prices
- **Feature engineering** (rooms per household, bedrooms per room) improves model accuracy
- **Gradient Boosting** handles non-linear relationships and feature interactions far better than Linear Regression
- **Log-transforming** the target variable can improve Linear Regression performance on skewed price data

---

## 🔮 Future Improvements

- Try `XGBoost` or `LightGBM` for faster training and better performance
- Add neighbourhood/zip-code clustering as a categorical feature
- Use `GridSearchCV` for systematic hyperparameter tuning
- Build a Streamlit web app for interactive price prediction

---

## 👤 Author

MUHAMMAD TALHA

