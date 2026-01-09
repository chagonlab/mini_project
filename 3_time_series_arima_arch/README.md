# Time Series Analysis: ARIMA and ARCH/GARCH Modeling

This project explores the dual nature of time series data: modeling the **mean** using ARIMA and modeling the **volatility** (conditional variance) using ARCH/GARCH models. It specifically utilizes the classic AirPassengers dataset to demonstrate these statistical techniques.

## Project Overview
In financial and seasonal time series, predicting the value itself is only half the battle. Understanding the "risk" or "uncertainty" (volatility) is equally crucial. This project walks through the process of stabilizing a series, fitting an ARIMA model, and then analyzing the residual volatility clusters using GARCH.

## Key Features
- **Data Preprocessing**: Handling time-series indices and cleaning data.
- **Stationarity Analysis**: Using Log-transformation and Differencing to stabilize variance and mean.
- **ARIMA Modeling**: Finding the optimal orders for predicting the series mean.
- **Volatility Analysis (ARCH/GARCH)**: 
  - Capturing **Volatility Clustering** (where high-volatility periods follow high-volatility).
  - Evaluating model persistence using parameters ($\alpha, \beta$).
  - Analyzing the **Leverage Effect** (how bad news increases volatility more than good news).

## Workflow
1. **Exploratory Data Analysis (EDA)**: Visualizing trends and seasonal patterns.
2. **Stationarity Check**: Visualizing ACF/PACF plots to determine differencing requirements.
3. **Model Selection**: Using `pmdarima` for Auto-ARIMA and `arch` library for volatility modeling.
4. **Diagnostics**: Reviewing P-values, AIC, and BIC to validate the model's performance.

## Requirements
```bash
pip install pandas numpy matplotlib statsmodels pmdarima arch
