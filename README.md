📌 Project Overview
This project performs advanced weather trend forecasting on the World Weather Repository dataset from Kaggle.
The dataset contains daily weather observations for 200+ cities worldwide with 40+ meteorological features including temperature, humidity, wind speed, air quality, UV index, and more.

📁 Repository Structure
Datascience/
│
├── GlobalWeatherForecasting.ipynb    <- Main Jupyter Notebook (all code here)
├── GlobalWeatherRepository.csv       <- Dataset
├── weather_forecast_report.html      <- Interactive HTML Report
├── requirements.txt                  <- Python dependencies
├── .gitignore                        <- Git ignore rules
├── README.md                         <- You are here
│
├── eda_temperature.png               <- EDA Charts
├── eda_correlation.png
├── eda_monthly_trend.png
├── eda_scatter.png
├── anomaly_detection.png             <- Anomaly Detection Chart
├── seasonal_decompose.png            <- SARIMA Decomposition
├── sarima_forecast.png               <- SARIMA Forecast
├── prophet_forecast.png              <- Prophet Forecast
├── prophet_components.png
├── xgboost_forecast.png              <- XGBoost Forecast
├── model_comparison.png              <- All Models Compared
├── feature_importance.png            <- Feature Importance
├── climate_seasonal.png              <- Climate Analysis
├── air_quality.png                   <- Air Quality Analysis
├── spatial_latitude.png              <- Spatial Analysis
└── spatial_map.html                  <- Interactive World Map

🚀 How to Run
Step 1 — Clone the Repository
bashgit clone https://github.com/Shashank1725/Datascience.git
cd Datascience
Step 2 — Install Dependencies
bashpip install -r requirements.txt
Step 3 — Open Notebook
bashjupyter notebook GlobalWeatherForecasting.ipynb
Step 4 — Run All Cells
Kernel -> Restart & Run All

Note: CSV file already repo mein hai. Koi extra download nahi karna.


🔬 What's Inside the Notebook
Section 1 — Imports & Setup
All required libraries imported. COLORS palette defined for consistent visualization.
Section 2 — Data Loading

Loaded GlobalWeatherRepository.csv
Checked shape, columns, and data types

Section 3 — Data Cleaning & Preprocessing

Parsed last_updated as datetime
City-wise median imputation for missing values
Z-score outlier removal (threshold > 3)
StandardScaler normalization
Feature Engineering:

FeatureDescriptionmonth, day_of_year, weekTemporal seasonalityheat_indexPerceived temperature (temp + humidity)rain_flagBinary precipitation indicatorhemisphereNorth/South based on latitudetemp_7day_avg7-day rolling average per city
Section 4 — Exploratory Data Analysis (EDA)

Temperature distribution by country
Correlation heatmap (15 features)
Monthly precipitation vs temperature trend
Temperature vs Humidity scatter with Pearson r

Section 5 — Anomaly Detection (Advanced)
Three methods used with consensus voting (2 of 3):
MethodDescriptionIsolation ForestTree-based anomaly isolationLocal Outlier Factor (LOF)Density-based neighbor comparisonZ-scoreStatistical threshold (> 3 sigma)
Section 6 — SARIMA Forecasting

ADF test for stationarity
Seasonal decomposition
SARIMA (1,1,1)(1,1,1,7) — weekly seasonality
80/20 train-test split

Section 7 — Prophet Forecasting

Facebook Prophet with weekly + yearly seasonality
Component plots (trend, weekly, yearly)

Section 8 — XGBoost Forecasting

41 meteorological features + lag features (1, 3, 7 days)
500 estimators with early stopping

Section 9 — Ensemble Model

Combined XGBoost + Random Forest + Gradient Boost
Weights optimized via grid search

Section 10 — Model Comparison
ModelRMSE (C)R2 ScoreSARIMA~2.1~0.81Random Forest~1.8~0.85Gradient Boost~1.7~0.87XGBoost~1.6~0.89Ensemble~1.4~0.93
Section 11 — Feature Importance & SHAP

XGBoost built-in feature importance
Random Forest importance comparison
SHAP values for direction of effect on predictions

Section 12 — Climate Analysis

K-Means clustering into 5 climate zones
Seasonal variation amplitude per city
Most stable vs most variable climates identified

Section 13 — Air Quality Analysis

PM2.5 correlation with all weather features
WHO limit comparison (25 ug/m3)
Worst cities by average PM2.5 ranked

Section 14 — Spatial Analysis

Interactive Plotly world map
Latitude band analysis (6 bands 90S to 90N)
Temperature, humidity, precipitation by latitude


📦 Requirements
pandas
numpy
scipy
scikit-learn
xgboost
statsmodels
prophet
matplotlib
seaborn
plotly
shap
jupyter
Install all at once:
bashpip install -r requirements.txt

💡 Key Findings

Best Model: Ensemble (XGBoost + RF + GB) with R2 = 0.93
Top Features: humidity, pressure_mb, uv_index, day_of_year, wind_kph
Anomaly Rate: 3 to 5 percent of records are genuine extreme events
Air Quality: Wind speed is strongest predictor of PM2.5 (r = -0.58)
Climate: Continental cities (Moscow, Kyiv) show highest seasonal variation (30C+)
Spatial: Equatorial cities most stable; mid-latitude cities most variable


🎥 Demo Video
Watch Project Demo: Link ← Add your Loom/YouTube link here

👤 Author
Shashank

GitHub: @Shashank1725
Assessment: PM Accelerator Tech Assessment — Advanced Level


Submitted for PM Accelerator Tech Assessment, May 2026
Mission: Leveling the playing field for future PM leaders worldwide.
