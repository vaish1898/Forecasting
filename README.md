# US Personal Consumption Expenditures Forecasting (1959–2023)

This repository contains a comprehensive time series analysis and forecasting project for U.S. Personal Consumption Expenditures (PCE). The objective is to identify the most effective forecasting method among Naïve, Exponential Smoothing, and ARIMA models, and to forecast expenditures up to October 2024.

---

## 📊 Dataset Description

- **File**: `PCE.csv`
- **Observations**: 779 (Monthly data)
- **Variables**:
  - `Date` (Character) — in MM/DD/YYYY format (Jan 1959 to Nov 2023)
  - `PCE` (Numeric) — Personal Consumption Expenditures

---

## 🧹 Data Preprocessing Steps

1. **Removed duplicates**
2. **Converted `Date` to Date type**
3. **Handled 43 missing values in `PCE` using Kalman filtering**
4. **Created time series object** with:
   - `start = c(1959, 1)`
   - `end = c(2023, 11)`
   - `frequency = 12` (monthly)

5. **Train-Test Split**:
   - Train: Jan 1959 to Dec 2009 (612 obs)
   - Test: Jan 2010 to Nov 2023 (167 obs)

---

## 📈 Forecasting Models Used

- **Naïve Method** (`naive()`)
- **Exponential Smoothing** (`ets()`)
- **ARIMA** (`auto.arima()`)

---

## 🧪 Accuracy Metrics Used

| Metric  | Description |
|---------|-------------|
| MAE     | Mean Absolute Error |
| MSE     | Mean Squared Error |
| MAPE    | Mean Absolute Percentage Error |
| MASE    | Mean Absolute Scaled Error |
| RMSE    | Root Mean Squared Error |

---

## 🏆 Model Performance Summary

| Metric | Naïve | Exponential Smoothing | ARIMA |
|--------|-------|------------------------|-------|
| MAE    | 3361.41 | 2236.39 | **1402.16** |
| MSE    | 17187778 | 8272435 | **3847873** |
| MAPE   | 22.75% | 14.93% | **9.13%** |
| MASE   | 171.23 | 113.92 | **71.43** |
| RMSE   | 4145.81 | 2876.18 | **1961.60** |

> **Best Model**: **ARIMA** (lowest errors across all metrics)

---

## 🎯 October 2024 Forecast

- **Model**: ARIMA fitted on full dataset
- **Horizon**: `h = 11` (from Nov 2023 to Oct 2024)
- **Forecasted PCE**: `$19,682.71 billion`

---

## 🔁 One-Step Ahead Rolling Forecast

| Model | MAE | RMSE | MSE | MAPE |
|-------|-----|------|-----|------|
| Naïve | 0.17 | 0.78 | 0.60 | 0.05 |
| Exponential Smoothing | 0.11 | 0.51 | 0.26 | 0.03 |
| **ARIMA** | **0.04** | **0.30** | **0.09** | **0.01** |

> ARIMA again outperformed the other models in rolling forecast evaluation.

---

## 📦 How to Run the Code

1. Clone this repository.
2. Place `PCE.csv` in the working directory.
3. Run the R script `forecasting_analysis.R`.
4. Required R packages:
   ```r
   install.packages(c("forecast", "imputeTS", "Metrics", "ggplot2"))
