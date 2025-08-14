# Solar Forecasting with SARIMAX + Fourier Terms & ML Models

This project forecasts hourly solar power generation using historical production and weather data. It demonstrates seasonality modeling with SARIMAX + Fourier terms and compares the results with XGBoost and Random Forest regression models. The pipeline integrates real-world solar farm data from NREL (https://www.nrel.gov/grid/solar-power-data) and historical weather from Open-Meteo (https://open-meteo.com/).

## Project Objectives
- Forecast hourly solar energy output using historical production data.
- Capture strong daily and annual seasonality using Fourier terms in a SARIMAX framework.
- Incorporate weather features (cloud cover, temperature, wind speed) as exogenous regressors to improve prediction accuracy.
- Compare SARIMAX performance with XGBoost and Random Forest regression models.
- Provide a reproducible, end-to-end forecasting pipeline for solar generation.

## Data Sources
1. Solar Power Data  
   - Source: NREL Solar Power Data (https://www.nrel.gov/grid/solar-power-data)  
   - Example: Actual_42.55_-85.35_2006_DPV_15MW_5_Min.csv  
   - Location: Michigan (42.55, -85.35)  
   - Aggregated from 5-minute resolution to hourly sums.

2. Weather Data  
   - Source: Open-Meteo Historical API (https://open-meteo.com/)  
   - Hourly variables: cloudcover, temperature_2m, wind_speed_10m  
   - Used as exogenous variables in SARIMAX and input features for ML models.

## Methods

### 1. Data Preprocessing
- Convert timestamps to datetime format.
- Resample 5-minute solar data to hourly sums.
- Merge solar generation with weather data by timestamp.
- Split into training (Jan 1 – Nov 27, 2006) and test (Nov 27 – Dec 31, 2006) sets.

### 2. SARIMAX + Fourier Terms
- Model captures seasonal patterns using CalendarFourier.
- Weather variables can be added as exogenous regressors.
- Model: SARIMAX(order=(1,0,1), seasonal_order=(0,0,0,0), exog=X), where X includes Fourier terms and optional weather features.
- Performance: Test RMSE: 17.999 MW

### 3. XGBoost
- Gradient boosting regression to capture non-linear relationships.
- Parameters: n_estimators=75, learning_rate=0.03, max_depth=4, subsample=0.8, colsample_bytree=0.8
- Performance: Test RMSE: 23.616 MW

### 4. Random Forest
- Ensemble tree-based regression to model non-linear effects of weather features.
- Parameters: n_estimators=200, max_depth=4, random_state=42
- Performance: Test RMSE: 23.878 MW

## Results Summary
Model                  | RMSE (MW) | Notes
---------------------- | ---------- | --------------------------------------
SARIMAX + Fourier      | 17.999     | Explicitly models seasonality; best performance
XGBoost                | 23.616     | Needs engineered seasonal features for better performance
Random Forest          | 23.878     | Similar to XGBoost; seasonal structure not captured inherently

## Visualizations
- SARIMAX Forecast vs Actual: captures both daily and yearly seasonality.
- XGBoost & Random Forest Forecasts: good at short-term variations but may miss seasonality patterns.
- Feature Plots: show weather variable influence on solar output.

## Requirements
pandas  
numpy  
matplotlib  
statsmodels  
scikit-learn  
xgboost  
requests

## Key Insights
- Seasonality modeling is critical: SARIMAX + Fourier terms outperform ML models without explicit seasonal terms.
- Weather variables improve short-term forecasts but do not replace seasonal structure.
- ML models require feature engineering (e.g., Fourier or day-of-year features) to match SARIMAX performance.

