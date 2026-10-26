# Forecasting Reliance Industries' Closing Stock Price (Time Series Analysis)

## Objective
Forecast the monthly closing price of Reliance Industries (RELIANCE.NS)
using exponential smoothing, ARIMA and SARIMA, and compare their accuracy.

## Data
Monthly OHLC prices and volume, [2000 to 2020/2023 - check], 252 rows,
no missing values. Source: [Yahoo Finance].

## Approach
1. Plotted the series: strong upward trend, non-stationary
2. Differencing was not enough to stabilise variance, so applied a
   **Box-Cox transform + differencing**; the ADF test confirmed stationarity (p < 0.001)
3. Seasonal decomposition (additive and multiplicative)
4. ACF/PACF to identify model orders
5. Fitted **Holt-Winters**, **ARIMA** and **SARIMA** on a train/test split
   ([state split, e.g. train to 2017, test 2018 onwards])
6. Residual diagnostics on the best model

## Results
| Model | RMSE | MAPE |
|---|---|---|
| Holt-Winters | 339.09 | 17.09% |
| ARIMA(0,1,0) with intercept | 464.18 | 24.43% |
| **SARIMAX(2,0,2)(1,1,2,12)** | **50.90** | **3.43%** |

SARIMA was clearly the best model. [State whether forecasts are one-step-ahead
or multi-step over the full test period.]

**Model adequacy (SARIMA):** residuals fluctuate around zero, and the
Ljung-Box test (10 lags, p = 0.194) finds no significant autocorrelation.
The residuals are somewhat heavy-tailed in the Q-Q plot.

## Limitations
Stock prices are affected by news and events that a univariate model cannot
see. This is an academic exercise and **not investment advice**.

## Run it
```bash
pip install -r requirements.txt
jupyter notebook notebooks/reliance-forecasting.ipynb
```

## Team
Carol Lopes, Mahika Panicker, Lakshay Singh.
Guided by Prof. Priyesh Tiwari, NMIMS.
My contribution: [write what you did].