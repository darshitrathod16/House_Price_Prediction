# 🏠 House Price Prediction

Predicting house sale prices in Ames, Iowa using machine learning, based on structural, quality, and location-related features. This project covers the full pipeline — cleaning, EDA, feature engineering, model building, hyperparameter tuning, and a business-focused final recommendation.

## 📌 Problem Statement

Home buyers and sellers often rely on guesswork or rough comparisons to decide on a price, which leads to overpricing, underpricing, and confusion in negotiations. This project uses historical sales data to build a model that estimates a fair price for a house and identifies which features actually drive that price.

## 📊 Dataset

- **1,460 houses**, **79 features**, target variable: `SalePrice`
- Features span lot size, building quality, room counts, garage/basement details, and neighborhood
- Source: Ames Housing Dataset (Kaggle)

## 🛠 Tech Stack

- Python, Pandas, NumPy
- Matplotlib, Seaborn
- Scikit-learn (Linear Regression, Random Forest, Gradient Boosting)
- XGBoost

## 🔍 Project Workflow

1. **Outlier Removal** — dropped 2 well-documented Ames outliers (very large `GrLivArea`, unusually low `SalePrice`)
2. **Missing Value Treatment** — semantic imputation: columns like `PoolQC`, `FireplaceQu`, and `GarageType` were filled with `'None'` (missing means the feature doesn't exist), not the column mode; `LotFrontage` filled with the neighborhood-wise median
3. **Exploratory Data Analysis** — distribution checks, correlation heatmap, neighborhood and quality vs. price comparisons
4. **Feature Engineering** — one-hot encoding of categorical variables, log-transform of `SalePrice` to correct right-skew
5. **Model Building** — Linear Regression, Random Forest, Gradient Boosting, XGBoost
6. **Hyperparameter Tuning** — `RandomizedSearchCV` for Random Forest and Gradient Boosting
7. **Evaluation** — MAE, R², and a train/test R² gap check to screen for overfitting
8. **Business Insights** — budget-based home filtering and a quality-per-price "value score" to support buyer decisions

## 📈 Model Performance

| Model | MAE | R² |
|---|---|---|
| Gradient Boosting (Baseline) | 17,467.78 | 0.9003 |
| XGBoost | 17,301.80 | 0.8982 |
| Random Forest (Tuned) | 17,132.92 | 0.8943 |
| Gradient Boosting (Tuned) | 17,161.62 | 0.8942 |
| Random Forest (Baseline) | 17,566.91 | 0.8899 |
| Linear Regression | 23,942.15 | 0.0994 |

*Note: these figures are from the pre-log-transform run and will be updated once the final rerun (outlier removal + log-transformed target) completes.*

## 🏆 Recommended Model

**Gradient Boosting (Baseline)** — selected for production. It has the highest test R² and the smallest train/test gap among all models tested, making it the most reliable choice for generalizing to new data, even though a couple of tuned models had a marginally lower MAE.

## 💡 Key Insights

- `OverallQual` and `GrLivArea` are the strongest price drivers
- Neighborhood alone can shift price by 2–3x — `NoRidge`, `NridgHt`, and `StoneBr` are premium areas; `MeadowV`, `IDOTRR`, and `BrDale` are the most affordable
- Plain Linear Regression struggles badly (R² ≈ 0.10) due to multicollinearity from one-hot encoded features — confirmed by comparing against Ridge/Lasso
- A simple value score (quality ÷ price) surfaces good-value homes that aren't in the cheapest neighborhoods

## 🚀 How to Run

```bash
git clone https://github.com/darshitrathod16/house-price-prediction.git
cd house-price-prediction
pip install -r requirements.txt
jupyter notebook House_Price_Prediction.ipynb
```

## 📁 Repository Structure

```
├── House_Price_Prediction.ipynb   # Full analysis and modeling notebook
├── data.csv                       # Dataset
└── README.md
```

## 🙋 Author

**Darshit Rathod**
[GitHub](https://github.com/darshitrathod16)
