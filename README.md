# Bike Demand Forecasting

Time series forecasting project comparing naive baseline, ARIMA and ARIMAX models using walk-forward validation.

## Results

| Model | MAE |
|------|-----|
| Naive | 790 |
| ARIMA (1,1,1) | 770 |
| Seasonal ARIMA | 775 |
| ARIMAX (weather predictors) | 677 |

Including weather variables significantly improved predictive accuracy.

## Project Structure

data/ → raw dataset  
notebooks/ → full analysis workflow  
src/ → reusable modelling code  
results/ → plots and evaluation outputs  

## How to Run

pip install -r requirements.txt  
jupyter notebook


## Overview

In this project I evaluated time-series forecasting approaches for daily bike rental demand using Python. The goal was to try and improve predictive accuracy over simple models using statistical models.

All of the models were evaluated using walk-forward validation with one step ahead forecasts, meaning each prediction only used information which would've been available at the time.


## Dataset

Daily bike rental data including:
- total rentals (cnt)
- temperature (temp)
- humidity (hum)
- windspeed (windspeed)
- date (dteday)


## Modelling

### 1: Naive Basline

Prediction: Demand Today ≈ Demand Yesterday

This is quite a strong benchmark for short-term forecasting.

MAE: 790


### 2: ARIMA (1,1,1)

A basic autoregressive model using past demand only.

Purpose:
Model short term temporal structure
Provide a statistical benchmark

MAE: 770
- Outperformed naive baseline


### 3: Seasonal ARIMA (weekly seasonality)

Tested weekly seasonal structure with: seasonal_order = (0,1,1,7)

Result: Seasonality didn't provide additional predictive benefit

MAE: 775
- No improvement over non-seasonal ARIMA


### 4: ARIMAX

Extend ARIMA to include the external driving factors:
- Temperature
- Humidity
- Windspeed

Implemented SARIMAX without seasonal conditions

Purpose:
Capture causal drivers of demand rather than relying solely on historical patterns

MAE: 677
- Largest improvement across all models


## Evaluation Method

All models were compared using:
- Walk-forward validation
- One-step-ahead prediction
- Identical test window
- Mean Absolute Error (MAE)

This ensures a fair comparison between all models


## Conclusion

While simple time-series models can capture short term demand dynamics, including external driving factors provides even more meaningful predictive performance gains. This highlights the importance of combining temporal structure with relevant predictors in applied forecasting problems.
