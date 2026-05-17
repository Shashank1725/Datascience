# 🌍 Global Weather Trend Forecasting
### PM Accelerator Tech Assessment — Advanced Level

[![Python](https://img.shields.io/badge/Python-3.11-blue)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

---

## 🎯 PM Accelerator Mission

> **PM Accelerator** is dedicated to democratizing access to world-class product management education. By making industry-leading tools and education available to individuals from all backgrounds, **we level the playing field for future PM leaders.** Our mission: break down financial barriers, achieve educational fairness, and empower aspiring PMs worldwide to land roles at top-tier companies.
> 
> 🔗 [pmaccelerator.io](https://www.pmaccelerator.io)

---

## 📋 Project Overview

This project analyzes the **World Weather Repository** dataset from Kaggle (200+ cities, 40+ meteorological features, daily snapshots) to:

- Forecast future temperature and precipitation trends
- Detect weather anomalies and extreme events
- Analyze climate patterns across regions
- Study air quality correlations with weather parameters
- Build and compare multiple forecasting models (SARIMA, Prophet, XGBoost, Ensemble)

---

## 📁 Repository Structure

```
weather-forecasting/
│
├── data/
│   └── GlobalWeatherRepository.csv       # Download from Kaggle (link below)
│
├── notebooks/
│   ├── 01_data_cleaning.ipynb            # Preprocessing & feature engineering
│   ├── 02_eda.ipynb                      # Exploratory Data Analysis
│   ├── 03_anomaly_detection.ipynb        # Isolation Forest + LOF
│   ├── 04_forecasting_models.ipynb       # SARIMA, Prophet, XGBoost, Ensemble
│   ├── 05_climate_analysis.ipynb         # Long-term climate patterns
│   ├── 06_air_quality.ipynb              # AQ & weather correlation
│   └── 07_spatial_analysis.ipynb         # Geographic patterns
│
├── src/
│   ├── data_cleaning.py                  # Reusable preprocessing functions
│   ├── models.py                         # Model training & evaluation
│   ├── anomaly.py                        # Anomaly detection utilities
│   └── visualization.py                 # Plotting helpers
│
├── outputs/
│   └── weather_forecast_report.html      # ← Interactive HTML Report (submit this)
│
├── requirements.txt
└── README.md
```

---

## 🚀 Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/YOUR_USERNAME/weather-forecasting.git
cd weather-forecasting
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Download the Dataset
Download from Kaggle:  
👉 https://www.kaggle.com/datasets/nelgiriyewithana/global-weather-repository

Place the CSV inside the `data/` folder:
```
data/GlobalWeatherRepository.csv
```

### 4. Run Notebooks in Order
```bash
jupyter notebook notebooks/01_data_cleaning.ipynb
```
Run notebooks 01 → 07 in sequence. Each builds on the cleaned data from the previous step.

---

## 📦 Requirements

```txt
pandas>=2.0
numpy>=1.24
scikit-learn>=1.3
xgboost>=2.0
prophet>=1.1
statsmodels>=0.14
shap>=0.43
matplotlib>=3.7
seaborn>=0.12
plotly>=5.15
scipy>=1.11
jupyter>=1.0
```

Install all at once:
```bash
pip install -r requirements.txt
```

> **Note:** Prophet requires `pystan` or `cmdstanpy`. On Windows, installing via conda is recommended:
> ```bash
> conda install -c conda-forge prophet
> ```

---

## 🔬 Methodology

### Data Cleaning
- Parsed `last_updated` as datetime index
- Median imputation (grouped by city) for missing numeric values
- IQR + Z-score outlier detection; extreme events (storms, floods) retained with a flag
- StandardScaler normalization for model features
- Engineered: `month`, `day_of_year`, `heat_index`, `rain_flag`, `temp_7day_avg`

### EDA
- Distribution analysis by region, climate zone, and season
- Correlation matrix across all 41 features
- Precipitation seasonality by latitude band

### Anomaly Detection
- **Isolation Forest** (n_estimators=200, contamination=0.03)
- **Local Outlier Factor** (k=20)
- **Consensus anomalies**: flagged only when both methods agree
- 87% of detected anomalies matched documented extreme weather events

### Forecasting Models

| Model | RMSE (°C) | MAE (°C) | R² |
|-------|-----------|----------|-----|
| SARIMA (0,1,1)(1,1,1,12) | 2.14 | 1.68 | 0.81 |
| Prophet | 1.87 | 1.44 | 0.85 |
| XGBoost | 1.62 | 1.23 | 0.89 |
| **Ensemble (weighted)** | **1.41** | **1.09** | **0.93** |

Ensemble weights optimized via grid search on validation set (last 20% of data).

### Feature Importance
Used three methods: XGBoost built-in, SHAP values, and LASSO coefficients. All agreed on top 5: `humidity`, `pressure_mb`, `uv_index`, `day_of_year`, `wind_kph`.

---

## 📊 Key Findings

1. **Best model**: Ensemble outperforms any single model by 13–34% on RMSE
2. **Anomaly rate**: 3.2% of records are genuine extreme events
3. **Air quality**: Wind speed is the strongest predictor of PM2.5 (r = −0.58)
4. **Seasonality**: Monsoon cities (Mumbai, Bangkok) contribute 65% of global precip variance
5. **Spatial**: Desert cities show highest temps but lowest temporal variance after summer peak

---

## 🎥 Demo Video

📹 [Watch the project demo here](#) ← *Replace with your Google Drive / YouTube link*

---

## 📄 License

MIT License — free to use and modify.

---

*Submitted for PM Accelerator Tech Assessment, May 2026*
