# grand-isle-water-level-ml
Machine learning models for one-hour-ahead coastal water-level prediction using NOAA data from Grand Isle, Louisiana.

# Grand Isle Coastal Water-Level Prediction Using Machine Learning

## Overview

This project uses NOAA hourly water-level observations from Grand Isle, Louisiana, to evaluate machine-learning approaches for short-term coastal water-level prediction.

The objective was to predict water level one hour ahead using recent historical water-level observations and compare the performance of three modeling approaches:

- Linear Regression
- Random Forest
- XGBoost

The project demonstrates an end-to-end environmental data science workflow, including data acquisition, time-series feature engineering, chronological model validation, predictive modeling, and model evaluation.

## Data

Data were obtained from the NOAA Tides and Currents station at Grand Isle, Louisiana (Station 8761724).

- Location: Grand Isle, Louisiana
- Station: 8761724
- Year: 2021
- Temporal resolution: Hourly
- Variable: Water level
- Datum: STND
- Units: Meters

The notebooks retrieve the data directly from NOAA using its public API.

## Methodology

Historical water-level observations were used to create lagged predictors representing conditions 1, 2, 3, 6, 12, and 24 hours previously.

The prediction target was the observed water level one hour into the future.

An 80/20 chronological train-test split was used to prevent future observations from being used to train the models.

### Models

1. Linear Regression
2. Random Forest Regression
3. XGBoost Regression

### Evaluation Metrics

Model performance was evaluated using:

- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)
- R²

## Results

| Model | MAE (m) | RMSE (m) | R² |
|---|---:|---:|---:|
| Linear Regression | 0.022 | 0.030 | 0.968 |
| Random Forest | 0.023 | 0.032 | 0.966 |
| XGBoost | 0.022 | 0.030 | 0.968 |

Linear Regression and XGBoost produced nearly identical predictive performance, while Random Forest performed slightly worse.

The results indicate that recent water-level observations contain substantial information for one-hour-ahead prediction at Grand Isle.

## Feature Analysis

The models placed substantial importance on the most recent water-level observation.

For Random Forest, the one-hour lag accounted for approximately 85.6% of total feature importance, while the 24-hour lag accounted for approximately 7.4%.

XGBoost also identified the one-hour and 24-hour lagged observations as the most influential predictors, although importance was distributed differently between the models.

## Error Analysis

The XGBoost model had:

- Mean residual: 0.0006 m
- Mean absolute error: 0.0219 m
- 95th percentile absolute error: 0.0595 m
- Maximum absolute error: 0.2132 m

The largest errors were concentrated during several short periods of unusual water-level variation.

## Limitations

This initial project uses a single monitoring station and one year of observations. The predictors are limited to historical water levels and therefore do not explicitly represent meteorological or storm-related drivers.

The results demonstrate short-term predictive capability but should not be interpreted as a general coastal water-level forecasting model.

## Future Work

Future development could incorporate:

- Wind speed and direction
- Atmospheric pressure
- Precipitation
- Multiple NOAA monitoring stations
- Longer observation periods
- Extreme-event analysis
- Storm-related water-level prediction

## Notebooks

| Notebook | Description |
|---|---|
| `NOAA_2021_LinearReg.ipynb` | Linear Regression model and coefficient analysis |
| `NOAA_2021_RandFor.ipynb` | Random Forest model and feature importance |
| `NOAA_2021_XGBoost.ipynb` | XGBoost model, feature importance, and residual analysis |
| `NOAA_2021_ModelComparison.ipynb` | Comparison of model performance |

## Data Source

NOAA Tides and Currents — Grand Isle Station 8761724.
