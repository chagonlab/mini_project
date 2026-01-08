### 1. Time Series Analysis Mini Projects
This repository contains two simple projects focused on time series data.

1. Achieving Stationarity
- Goal: Transform non-stationary data into stationary data for better analysis.
- Data: AirPassengers (Monthly airline passenger totals).
- Process:
1. Checked for trends and variance.
2. Applied Log Transformation to stabilize variance.
3. Applied Differencing to remove trends.

- Result: Successfully converted the raw data into a stationary time series.


### 2. Sensor Data Classification
- Goal: Classify time series data using automated feature engineering.
- Tools: tsfresh, XGBoost, Random Forest.
- Process:
1. Feature Extraction: Used tsfresh to automatically generate statistical features.
2. Data Cleaning: Imputed missing values created during extraction.
3. Modeling: Trained XGBoost and Random Forest models.

- Result: The XGBoost model achieved 100% accuracy (1.0 F1-score) on the test set.

### Conclusion
These projects show how to process time series data manually (Stationarity) and automatically (tsfresh) to build machine learning models.
