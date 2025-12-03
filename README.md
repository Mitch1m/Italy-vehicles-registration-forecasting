# Car Registration Forecasting in Italy (Time Series Analysis)

## Project Goal
This project is a time series analysis designed to predict the monthly number of new car registrations in Italy. The primary objective is to build a robust model that accounts for strong seasonality and external economic factors, providing a reliable short-term forecast.

## Methodology & Model Summary

### 1. Data Preparation
*   **Source:** Monthly time series data (provided in `dataset.txt`).
*   **Preprocessing:**
    *   Applied a **Log Transformation** to stabilize the variance (common for count data).
    *   Applied **Seasonal Differencing (Lag 12)** to achieve stationarity by removing the annual seasonal trend.
*   **External Factors:** A **Dummy Variable** was introduced in the model to account for the major exogenous shock during the COVID-19 pandemic period.

### 2. ARIMA Model Specification
An ARIMA model was chosen due to the clear autoregressive and moving average characteristics observed in the ACF/PACF plots of the differenced series.

| Component | Order | Details |
| :--- | :--- | :--- |
| **Non-Seasonal** | `ARIMA(1, 0, 2)` | Selected based on initial ACF/PACF diagnostics. |
| **Seasonal** | `SARIMA(0, 0, 4)` | Models the remaining seasonal correlation. |

*Model in R:* `arima(data, order = c(1L, 0L, 2L), seasonal = list(order = c(0L, 0L, 4L), period = 3))`

### 3. Forecast
The model successfully predicts the one-step-ahead forecast for the next month's registrations, reverted back to the original scale (`ppred` in the script).

## Technology & Libraries
*   **Language:** R
*   **Libraries:** Standard R time series libraries (`stats` package for `arima`, `acf`, etc.).

## How to Run the Analysis
1.  Clone this repository.
2.  Ensure the data file (`dataset.txt`) is in the same directory as the script (`analysis.R`).
3.  Execute the `analysis.R` script in R or RStudio.
