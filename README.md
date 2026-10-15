# Time Series Analysis Project

Course project for Time Series Analysis. The goal is to model a real-world time series with two forecasting approaches, **interpret every step** (technically and in a business context), and compare the forecasts methodologically. It is not only about producing forecasts.

## Dataset

**US industrial production: electric and gas utilities (not seasonally adjusted)**, monthly, index 2017 = 100. It measures the real output of US electric and gas utilities.

- Source: [FRED, series `IPG2211A2N`](https://fred.stlouisfed.org/series/IPG2211A2N) (Board of Governors of the Federal Reserve System, G.17 Industrial Production and Capacity Utilization).
- File: [IPG2211A2N.csv](IPG2211A2N.csv) (columns `observation_date`, `IPG2211A2N`), January 1939 to August 2026.
- Analysis window: January 1995 to August 2026 (380 observations).

The series can be decomposed as:

**Yₜ = Tₜ + Sₜ + Rₜ** (trend + seasonality + residual)

Its yearly seasonality is driven by the weather, with two peaks: winter (heating, January about +15% above the average month) and summer (air conditioning, July and August about +8%), and lows in spring and autumn. The seasonal amplitude grows with the level, which makes the additive vs multiplicative choice a real question. The trend is not linear: output grows fast until 2006, stays nearly flat until 2016, then rises again more slowly. The residual is largely driven by unusually cold or hot months, while the COVID-19 shock (spring 2020) is small compared with other sectors.

## Approaches

### 1. ETS decomposition + ARIMA (understand and explore)

- Decompose Yₜ into trend (Tₜ), seasonality (Sₜ) and residual (Rₜ). Two trends are compared: a piecewise linear trend (breakpoints found by grid search) and a double exponential smoothing trend.
- Model the residual Rₜ with ARIMA:
  - stationarity checks (ADF / KPSS),
  - ACF / PACF analysis to choose the (p, d, q) orders,
  - residual diagnostics.
- Forecast by recombining the trend, the seasonality and the ARIMA forecast of Rₜ.
- Interpret each component, technically and in business terms.

### 2. Facebook Prophet (discover and compare)

- Understand how the method works: additive trend, seasonality, holidays, changepoints.
- Try different parameters (changepoint prior scale, seasonality mode, holidays, etc.) and interpret their effect.

## Forecast comparison

- Use the same train / test split for both approaches: train from January 1995 to December 2024 (360 months), test from January 2025 to August 2026 (20 months).
- Compare them with loss functions: MSE, RMSE, MAE, MAPE.
- Discuss when and why one approach performs better than the other.

## Report structure

The report is written in the Jupyter notebook `TSA-Project - Tanguy MANDRILLON.ipynb`:

1. Introduction
2. Data exploration
3. Approach 1: ETS decomposition + ARIMA
4. Approach 2: Prophet
5. Forecast comparison
6. Conclusion
7. AI-usage policy: the main prompts and how AI was used in the project

## Setup

Dependencies are managed with [uv](https://docs.astral.sh/uv/):

```bash
uv sync
```

Then open the notebook and select the `.venv` kernel.
