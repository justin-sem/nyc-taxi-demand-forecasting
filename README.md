# NYC Yellow Taxi Demand Forecasting

## 📌 Project Overview

This project focuses on forecasting **hourly yellow taxi demand across NYC taxi zones** using historical taxi trip data and external factors such as weather and holidays.

The objective is to build a machine learning model that can predict taxi demand **one hour ahead**, which could support better driver allocation, fleet planning, and operational decision-making.

## 🎯 Objectives

* Analyze historical NYC yellow taxi demand patterns
* Identify temporal and external factors affecting taxi demand
* Develop a baseline forecasting model
* Build an XGBoost-based demand forecasting model
* Evaluate model performance using MAE, RMSE, and MAPE
* Identify the most important factors influencing taxi demand

## 📊 Dataset

The project uses the **NYC Yellow Taxi Trip Record Data for 2023**, containing taxi trip information across NYC.

The original dataset consists of monthly Parquet files. Due to the large dataset size, the data was processed month-by-month before being combined for analysis.

Additional datasets used:

* **NYC Taxi Zone Lookup** – provides taxi zone information
* **NOAA Central Park Weather Data** – daily temperature and precipitation
* **US Holiday Calendar** – identifies holidays in 2023

## 🔧 Data Processing

The following preprocessing steps were performed:

1. Loaded the 2023 yellow taxi trip data month-by-month
2. Selected relevant fields, primarily pickup datetime and pickup location
3. Removed records outside the target 2023 period
4. Removed a suspected incomplete period from September 21–24, 2023
5. Aggregated taxi pickups into **hourly demand by taxi zone**
6. Integrated daily weather information
7. Added US holiday information
8. Created temporal and demand-based features
9. Created lag features for historical demand
10. Created a one-hour-ahead forecasting target

### Feature Engineering

The main features include:

* `PULocationID`
* `hour`
* `day_of_week`
* `month`
* `week_of_year`
* `is_weekend`
* `TMAX`
* `TMIN`
* `PRCP`
* `is_holiday`
* `rainy_day`
* `lag_1`
* `lag_2`
* `lag_24`

Lag features were included to capture recent demand patterns and daily seasonality.

## 🤖 Models

### 1. Linear Regression

A Linear Regression model was used as the baseline model.

### 2. XGBoost

An XGBoost regression model was developed to capture nonlinear relationships between taxi demand and the engineered features.

Key parameters included:

* `n_estimators = 200`
* `learning_rate = 0.05`
* `max_depth = 6`
* `subsample = 0.8`
* `colsample_bytree = 0.8`
* Early stopping

## 📈 Results

| Model             |       MAE |      RMSE |       MAPE |
| ----------------- | --------: | --------: | ---------: |
| Linear Regression |     22.18 |     37.08 |    171.51% |
| XGBoost           | **17.08** | **30.82** | **67.96%** |

XGBoost outperformed the Linear Regression baseline across all three evaluation metrics.

The results indicate that nonlinear machine learning methods can better capture the complex demand patterns present in taxi activity across different NYC locations and time periods.

## 💡 Key Insights

The analysis highlights several important characteristics of taxi demand:

* Taxi demand varies substantially by **time of day**
* Demand patterns differ across **taxi zones**
* Recent demand is an important predictor of near-term demand
* Daily seasonality can be captured through lagged demand features
* Weather and holidays provide additional contextual information
* XGBoost provides better predictive performance than the linear baseline

## ⚠️ Limitations

Several limitations should be considered:

* Only one year of taxi data was used
* Weather data was available at a **daily rather than hourly level**
* Major events such as concerts, festivals, sporting events, and conferences were not explicitly incorporated
* MAPE can be problematic for locations or periods with very low demand
* Further hyperparameter tuning and model experimentation could potentially improve performance

## 🚀 Future Improvements

Potential improvements include:

* Incorporating multiple years of historical taxi data
* Using hourly weather information
* Adding major NYC events and sporting events
* Incorporating public transportation and traffic information
* Testing LightGBM, CatBoost, and deep learning models
* Performing more extensive hyperparameter optimization
* Developing zone-specific forecasting models
* Creating an interactive dashboard for demand monitoring and forecasting

## 🛠️ Technologies

* Python
* Pandas
* NumPy
* Scikit-learn
* XGBoost
* Matplotlib
* Jupyter Notebook
* Parquet

## 📁 Project Structure

```text
NYC-Taxi-Demand-Forecasting/
│
├── taxi_demand_forecasting.ipynb
├── README.md
├── requirements.txt
├── .gitignore
└── data/
    └── README.md
```

## 👤 Author

**Justin Sem**

This project was developed as a machine learning and data analytics project focused on demand forecasting and operational decision-making.
