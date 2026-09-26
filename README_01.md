# House Price Prediction

- This project predicts the sale price of a house using structural, quality, and location-related features from the Ames Housing dataset. It was done as part of my data science internship project (PRCP-1020).

## Problem Statement

- People usually price houses based on guesswork, which often leads to overpricing, underpricing, or confusion about real value. The goal here is to build a model that predicts a fair sale price for a house, explain which features actually drive that price, and suggest good-value homes for buyers working within a budget.

## Dataset

- The dataset has 1,460 houses with 79 features covering things like lot size, room counts, garage and basement details, build quality, and neighborhood, with `SalePrice` as the target. Two known outliers (very large homes that sold at unusually low prices) were removed, leaving 1,458 rows for modeling.

## What I did

* Removed 2 known outliers from the dataset before doing anything else.
* Handled missing values properly, columns like `PoolQC` and `FireplaceQu` don't mean "missing data", they mean the house doesn't have that feature, so these were filled with `'None'` instead of the mode.
* Did EDA to see which features actually relate to price, `OverallQual`, `GrLivArea`, and `Neighborhood` stood out early on.
* Noticed `SalePrice` was right-skewed and log-transformed it before training, this alone fixed Linear Regression's R² from 0.099 to 0.91.
* One-hot encoded categorical columns, taking the feature count from 79 to 259.
* Trained and compared 4 models: Linear Regression (plus Ridge and Lasso as a check), Random Forest, Gradient Boosting, and XGBoost.
* Tuned Random Forest and Gradient Boosting using RandomizedSearchCV.
* Checked train vs test R² for every model to catch overfitting, XGBoost turned out to overfit the most despite looking fine on paper.
* Looked at feature importance from the final model to see what actually drives price.

## Results

- Gradient Boosting (Tuned) gave the best overall result, with an R² of 0.9220 and MAE of about 14,979 on the test data. It also had one of the smallest gaps between train and test R², so it generalizes well instead of just memorizing the training data. XGBoost had the worst overfitting of all models, near-perfect on training data but the weakest on test data.

- The most useful features turned out to be `OverallQual`, `GrLivArea`, `YearBuilt`, `GarageArea`, and `TotalBsmtSF`.

## Business takeaway

- Predictions are most reliable for homes under $250,000, so that's where this model should be trusted the most. For homes above 300,000 dollers predictions get less accurate and should be treated with more caution. A simple "value score" (quality divided by price) was also built to help buyers spot high-quality homes at a lower cost, mostly found in areas like `IDOTRR` and `Edwards`.

## Tools used

- Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, XGBoost, joblib.

## Files

# House Price Prediction

- This project predicts the sale price of a house using structural, quality, and location-related features from the Ames Housing dataset. It was done as part of my data science internship project (PRCP-1020).

## Problem Statement

- People usually price houses based on guesswork, which often leads to overpricing, underpricing, or confusion about real value. The goal here is to build a model that predicts a fair sale price for a house, explain which features actually drive that price, and suggest good-value homes for buyers working within a budget.

## Dataset

- The dataset has 1,460 houses with 79 features covering things like lot size, room counts, garage and basement details, build quality, and neighborhood, with `SalePrice` as the target. Two known outliers (very large homes that sold at unusually low prices) were removed, leaving 1,458 rows for modeling.

## What I did

* Removed 2 known outliers from the dataset before doing anything else.
* Handled missing values properly, columns like `PoolQC` and `FireplaceQu` don't mean "missing data", they mean the house doesn't have that feature, so these were filled with `'None'` instead of the mode.
* Did EDA to see which features actually relate to price, `OverallQual`, `GrLivArea`, and `Neighborhood` stood out early on.
* Noticed `SalePrice` was right-skewed and log-transformed it before training, this alone fixed Linear Regression's R² from 0.099 to 0.91.
* One-hot encoded categorical columns, taking the feature count from 79 to 259.
* Trained and compared 4 models: Linear Regression (plus Ridge and Lasso as a check), Random Forest, Gradient Boosting, and XGBoost.
* Tuned Random Forest and Gradient Boosting using RandomizedSearchCV.
* Checked train vs test R² for every model to catch overfitting, XGBoost turned out to overfit the most despite looking fine on paper.
* Looked at feature importance from the final model to see what actually drives price.

## Results

- Gradient Boosting (Tuned) gave the best overall result, with an R² of 0.9220 and MAE of about 14,979 on the test data. It also had one of the smallest gaps between train and test R², so it generalizes well instead of just memorizing the training data. XGBoost had the worst overfitting of all models, near-perfect on training data but the weakest on test data.

- The most useful features turned out to be `OverallQual`, `GrLivArea`, `YearBuilt`, `GarageArea`, and `TotalBsmtSF`.

## Business takeaway

- Predictions are most reliable for homes under $250,000, so that's where this model should be trusted the most. For homes above 300,000 dollers predictions get less accurate and should be treated with more caution. A simple "value score" (quality divided by price) was also built to help buyers spot high-quality homes at a lower cost, mostly found in areas like `IDOTRR` and `Edwards`.

## Tools used

- Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, XGBoost, joblib.

## Files

* `House_Price_Prediction.ipynb` - full notebook with EDA, preprocessing, feature engineering, modeling, tuning, and conclusion.
