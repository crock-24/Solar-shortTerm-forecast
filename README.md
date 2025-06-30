# Solar Output Forecasting with XGBoost, Random Forest, and SARIMAX

This project builds and compares models to forecast **hourly solar power output** using weather data and time-based features. It combines both **machine learning** and **statistical time series modeling** approaches.

---

## Models Used

### XGBoost Regressor
A high-performance gradient boosting model trained on weather-based features.

### Random Forest Regressor
A simpler, interpretable ensemble of decision trees used as a baseline.

- Bootstrap aggregation
- Low tuning requirements
- Good for quick, robust models

### SARIMAX with Fourier Seasonality
A statistical time series model with:
- Autoregressive and moving average terms
- Fourier-transformed daily seasonality
- Weather features as exogenous regressors
  
---

## Features Used

- `temperature_2m`: Hourly air temperature  
- `cloudcover`: Cloud cover percentage  
- `wind_speed_10m`: Wind speed at 10 meters  
- `hour`: Hour of day (cyclical pattern)  
- Fourier terms (`sin/cos`) for daily cycles (SARIMAX only)

---

## Data Processing

- Datetime indexed at hourly frequency
- Clipped negative forecasts to zero (non-physical values)

---

## Evaluation

Models were evaluated on a holdout test set using:

- **Root Mean Squared Error (RMSE)**
- **Visual inspection** of predicted vs. actual values
