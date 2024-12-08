# Airbnb Price Modelling: A Data Science Project

This project predicts Airbnb listing prices in New York City using machine learning. The process includes data preprocessing, exploratory data analysis, feature engineering, and model optimisation, showcasing a structured data science workflow.

---

## Table of Contents
1. [Introduction](#introduction)
2. [Data Preprocessing](#data-preprocessing)
   - [Identifying Missing Data](#identifying-missing-data)
   - [Observing Missing Data](#observing-missing-data)
   - [Recap: Data Preprocessing](#recap-data-preprocessing)
3. [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
   - [Univariate Analysis and Outlier Detection](#univariate-analysis-and-outlier-detection)
   - [Key Insights from Bivariate Analysis](#key-insights-from-bivariate-analysis)
4. [Feature Engineering](#feature-engineering)
   - [Recap: Feature Engineering](#recap-feature-engineering)
5. [Model Development](#model-development)
   - [Baseline Model Development](#baseline-model-development)
   - [Hyperparameter Tuning](#hyperparameter-tuning)
6. [Evaluation and Results](#evaluation-and-results)
7. [Conclusion](#conclusion)

---

## 1. Introduction

The goal of this project is to predict the price of Airbnb listings based on key features such as location, room type, availability, and reviews. By building a machine learning model, the project aims to:
- Understand which features drive Airbnb prices.
- Improve model accuracy iteratively through feature engineering.
- Provide actionable insights for optimising pricing strategies.

This iterative process of feature engineering and analysis refines the model's performance, with a particular focus on leveraging feature importance to guide enhancements.

---

## 2. Data Preprocessing

### Identifying Missing Data
- The dataset contains missing values in the following columns:
  - `last_review`: 10,052 missing entries.
  - `reviews_per_month`: 10,052 missing entries.

### Observing Missing Data
- Missing values in `last_review` and `reviews_per_month` correspond to properties with `number_of_reviews = 0`.

### Recap: Data Preprocessing
1. Removed irrelevant columns (e.g., `host_name`, `latitude`).
2. Handled missing data:
   - Filled `reviews_per_month` with `0`.
   - Dropped `last_review` as it was non-essential.
3. Final dataset shape: **48,895 rows and 10 columns.**

---

## 3. Exploratory Data Analysis (EDA)

### Univariate Analysis and Outlier Detection
- Identified skewed distributions in `price` and `availability_365`.
- Addressed extreme outliers in the `price` column.

### Key Insights from Bivariate Analysis
1. **Neighbourhood**:
   - Manhattan listings have the highest prices, while Bronx and Staten Island are the most affordable.
2. **Room Type**:
   - Entire homes/apartments are the most expensive, shared rooms are the least.

---

## 4. Feature Engineering

### Recap: Feature Engineering
1. Created new features:
   - `avg_price_neighbourhood`: Average price per neighbourhood.
   - `reviews_per_year`: Annualised review counts.
2. Log-transformed `minimum_nights` to reduce skewness.
3. Categorical encoding:
   - One-hot encoding for `room_type` and `neighbourhood_group`.
   - Target encoding for `neighbourhood` (high cardinality).

---

## 5. Model Development

### Baseline Model Development
- Built an initial **XGBoost Regressor** with default hyperparameters.
- Achieved an **R² score** of:
  - Training: **0.65**
  - Test: **0.56**

### Hyperparameter Tuning
- Used Bayesian optimisation to tune hyperparameters:
  - Best parameters: `eta = 0.0222`, `max_depth = 7`, `n_estimators = 470`, etc.
- Improved model performance to **R² = 0.57** on the test set.

---

## 6. Evaluation and Results

### Key Features:
1. `availability_365`
2. `number_of_reviews`
3. `avg_price_neighbourhood`

### Insights:
- The model generalises well, with minimal overfitting.
- Availability and reviews significantly impact pricing.

---

## 7. Conclusion

This project successfully demonstrated how feature engineering and machine learning techniques can predict Airbnb prices. While the model explains **57% of the variance**, opportunities for improvement include:
- Incorporating external data (e.g., socioeconomic factors, amenities).
- Experimenting with alternative models (e.g., LightGBM).

**Next Steps**:
- Further optimise feature engineering.
- Enhance interpretability using SHAP or PDP plots.
