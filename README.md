# USD/ETB Exchange Rate Analysis & Forecasting

An end-to-end financial time-series analysis and forecasting project of the US Dollar to Ethiopian Birr (USD/ETB) exchange rate. This project analyzes the historical daily rate trend, maps a massive structural transition in volatility following major economic policy reforms, and implements an optimized ARIMA forecasting model on the market-driven, post-float data.

##  Financial & Economic Context
Prior to late July 2024, the National Bank of Ethiopia maintained a managed crawling peg for the Ethiopian Birr (ETB). On **July 29, 2024**, the central bank officially transitioned to a market-based, floating exchange rate system to address macroeconomic imbalances. 

This regulatory shift introduced a classic **structural break** in the exchange rate data:
*   **Pre-July 2024 (Pegged Era):** Extremely low volatility, artificially stabilized daily official rates.
*   **Post-July 2024 (Floating Era):** Free-floating, highly dynamic, and volatile daily market rates.

This dramatic shift makes USD/ETB an excellent time-series modeling case study, as models trained on the pre-float data are fundamentally incompatible with the current market regime.

## 🛠️ Project Workflow & Features
- **Live Data Pipeline:** Programmatic retrieval of live daily historical USD/ETB exchange rate data using `yfinance`.
- **Policy Shift Detection:** Visual identification of the July 2024 structural break where the currency transitioned from a peg to a market-driven float.
- **Volatility Analysis:** Calculated 30-day rolling standard deviations of daily percentage returns to mathematically prove and visualize the volatility shift.
- **Stationarity Testing:** Conducted an Augmented Dickey-Fuller (ADF) test to evaluate the statistical stationarity of the post-float time series.
- **Baseline Forecasting:** Built an intuitive 7-day and 30-day Simple Moving Average (SMA) baseline.
- **ARIMA Modeling:** Segmented the data to focus strictly on the post-float market and trained an Autoregressive Integrated Moving Average (ARIMA) model.
- **Hyperparameter Optimization:** Conducted an AIC-based Grid Search across $(p, d, q)$ parameters to mathematically identify the most accurate forecasting configuration.

## 📊 Performance & Optimization Results

We evaluated our models by training them on the post-float data and testing predictions against a 30-day holdout set of actual market prices. 

| Metric | Baseline Model `ARIMA(1, 1, 1)` | Optimized Model `ARIMA(2, 1, 3)` | Performance Improvement |
| :--- | :---: | :---: | :---: |
| **Mean Absolute Error (MAE)** | 1.7156 ETB | **1.1755 ETB** | **31.4% Error Reduction** |
| **Root Mean Squared Error (RMSE)** | 2.2031 ETB | **1.5227 ETB** | **30.8% Error Reduction** |
| **Average Percentage Deviation** | ~1.08% | **~0.74%** | — |

### Interpretation
The AIC-based grid search optimized our model from `ARIMA(1,1,1)` to `ARIMA(2,1,3)`. This means that predicting tomorrow's rate is highly dependent on looking at **two days of past prices** ($p=2$) and **three days of past prediction errors** ($q=3$). 

By tuning these parameters, our forecast error was reduced by over 30%, resulting in an average daily prediction error of just **0.74%** over a 30-day forecasting window.

## 📁 Repository Structure
```text
├── exchange_rate_analysis.ipynb   # Main Jupyter Notebook with all code & plots
├── README.md                      # Project documentation and results
└── requirements.txt               # Dependencies required to run the notebook
