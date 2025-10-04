# Energy Consumption Forecasting with XGBoost

This project demonstrates a time-series forecasting model for predicting hourly energy consumption using an XGBoost Regressor. The notebook covers the end-to-end process of data analysis, feature engineering, model training, and evaluation.

---

## Introduction

The goal of this project is to predict future energy usage based on historical observations. We utilize a time-series dataset of hourly energy consumption from PJM Interconnection. Instead of using traditional time-series models like ARIMA, this approach transforms the problem into a regression task by engineering features from the datetime index. This allows us to leverage powerful gradient boosting models like XGBoost to capture complex temporal patterns.

## Dataset

The dataset used in this project contains hourly energy consumption data from PJM. Due to its size, it is not included in this repository but can be downloaded from Kaggle:

-   **Dataset:** [PJME Hourly Energy Consumption](https://www.kaggle.com/datasets/robikscube/hourly-energy-consumption)
-   **Target Variable:** `PJME_MW` (Energy consumption in Megawatts)

---

## Concepts and Methodology

The project follows a structured approach to building the forecasting model:

1.  **Data Overview and Exploration:** The `PJME_hourly.csv` dataset is loaded, and the datetime column is set as the index. An initial analysis is performed to visualize the overall trend, seasonality, and potential anomalies in the energy consumption data over time.

2.  **Train-Test Split:** The data is chronologically split into a training set and a testing set. Data before January 1, 2015, is used for training the model, and the subsequent data is reserved for testing its performance on unseen future values.

3.  **Feature Engineering:** To enable the regression model to understand time-based patterns, several features are extracted from the datetime index. These features help the model learn relationships between the time of day, week, or year and energy consumption. The created features include:
    -   `hour`
    -   `dayofweek`
    -   `quarter`
    -   `month`
    -   `year`
    -   `dayofyear`

4.  **Modeling with XGBoost:** An XGBoost Regressor model is trained using the engineered features. XGBoost is chosen for its high performance and robustness. The model is trained with an early stopping mechanism to prevent overfitting, using the test set as the evaluation set.

---

## Outputs and Analysis

-   **Feature Importance:** The analysis reveals which features were most influential in making predictions. The `hour` and `month` are shown to be the most critical predictors of energy consumption.
-   **Forecast vs. Actual Data:** A comparison of the model's predictions against the true data on the test set demonstrates its ability to capture the underlying patterns in the time series. The model follows the general trend and seasonality, with some deviations during periods of high volatility.

---

## Results Summary

The model's performance is evaluated using the Root Mean Squared Error (RMSE) on the test set.

-   **RMSE on Test Set:** **3741.03 MW**

Analysis of the daily average error shows the model performed best on days in late 2016 and early 2017 and had the most difficulty with days in mid-August 2016, which were likely periods of unusual energy demand.

---

## Conclusion and Future Work

This project demonstrates that a regression-based approach using feature engineering can be effective for time-series forecasting.

### Future Scope:
-   **Incorporate more sophisticated models** such as ARIMA, Prophet, or LSTMs.
-   **Enhance feature engineering** with rolling statistics (e.g., mean/std over a window) or Fourier terms for seasonality.
-   **Include external covariates** like holiday schedules and weather data, which are known to impact energy consumption.
-   **Perform hyperparameter tuning** and cross-validation for more robust results.
