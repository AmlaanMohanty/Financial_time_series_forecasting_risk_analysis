# Financial Time-Series Forecasting and Risk Analysis

An end-to-end financial analytics project focused on the Indian equity market. The project analyses NIFTY 50 and five large-cap Indian stocks, compares ARIMA and Prophet forecasting models, performs market regression, constructs an equal-weight portfolio, and estimates risk using Value at Risk and Monte Carlo simulation.

> This project is intended for educational and portfolio purposes only. It is not investment advice.

## Executive Summary

This project evaluates the performance and risk of five large-cap Indian stocks against NIFTY 50 using historical market data from January 2020 onwards. It combines exploratory analysis, portfolio construction, market regression, time-series forecasting and risk simulation in one reproducible workflow.

The analysis found that ICICI Bank delivered the strongest individual historical return, while NIFTY 50 provided better stability and risk-adjusted performance than the equal-weight portfolio. ARIMA(0,1,0) outperformed Prophet on the 60-trading-day holdout dataset, achieving a MAPE of 2.26%. A 10,000-path Monte Carlo simulation estimated a 42.34% probability that the portfolio would finish below its initial value after 30 trading days.

## Project Objectives

- Collect and clean historical Indian stock-market data
- Analyse adjusted prices, returns and volatility
- Compare stock performance with the NIFTY 50 benchmark
- Examine asset correlations and diversification opportunities
- Construct and evaluate an equal-weight portfolio
- Estimate alpha, beta and R-squared through regression analysis
- Test stationarity using the Augmented Dickey-Fuller test
- Compare ARIMA and Prophet forecasting performance
- Estimate Historical VaR, Parametric VaR and CVaR
- Simulate 10,000 possible portfolio outcomes over 30 trading days
- Prepare analysis-ready datasets for a Power BI dashboard

## Potential Business Applications

- Portfolio performance and benchmark monitoring
- Market-risk and management reporting
- Investment-research support
- Asset-allocation and diversification analysis
- Volatility and drawdown monitoring
- Forecast-model evaluation
- Interactive financial reporting through Power BI

## Assets Analysed

| Symbol | Asset |
|---|---|
| `^NSEI` | NIFTY 50 |
| `RELIANCE.NS` | Reliance Industries |
| `TCS.NS` | Tata Consultancy Services |
| `HDFCBANK.NS` | HDFC Bank |
| `INFY.NS` | Infosys |
| `ICICIBANK.NS` | ICICI Bank |

Historical adjusted prices were collected programmatically from Yahoo Finance using `yfinance`, beginning on 1 January 2020. The final observation changes whenever the notebook is refreshed.

## Tools and Technologies

- Python
- Pandas and NumPy
- SciPy and Statsmodels
- scikit-learn
- Prophet
- yfinance
- Matplotlib and Seaborn
- Jupyter Notebook / Google Colab
- Microsoft Power BI

## Analytical Workflow

1. Downloaded adjusted price history for NIFTY 50 and five Indian stocks.
2. Inspected missing observations and duplicate dates.
3. Calculated simple returns, log returns and normalised price performance.
4. Measured total return, CAGR, annualised volatility, Sharpe ratio and maximum drawdown.
5. Evaluated return correlations and constructed an equal-weight stock portfolio.
6. Estimated stock alpha, beta and R-squared against NIFTY 50.
7. Tested NIFTY 50 stationarity using the ADF test.
8. Evaluated ARIMA and Prophet on the same 60-trading-day holdout period.
9. Generated a final 30-business-day ARIMA forecast.
10. Estimated portfolio VaR and CVaR at 95% confidence.
11. Ran a 10,000-path correlated Monte Carlo simulation over 30 trading days.
12. Exported 13 structured tables for Power BI.

## Financial Measures

- **Daily return:** Percentage change in adjusted closing price from one trading day to the next.
- **CAGR:** Compounded annual growth rate over the complete analysis period.
- **Annualised volatility:** Daily return standard deviation multiplied by the square root of 252 trading days.
- **Sharpe ratio:** Annual return above the assumed 6% risk-free rate divided by annualised volatility.
- **Maximum drawdown:** Largest percentage decline from a previous asset or portfolio peak.
- **Beta:** Sensitivity of an individual stock's returns to NIFTY 50 returns.
- **Alpha:** Return not explained by movements in the NIFTY 50 benchmark.
- **Historical VaR:** Historical loss threshold at the fifth percentile of portfolio returns.
- **CVaR:** Average loss among observations exceeding the VaR threshold.

## Model Validation Approach

- The latest 60 trading observations were reserved as an unseen testing dataset.
- No random train-test split was used because it could disrupt chronological order and introduce future-data leakage.
- The Augmented Dickey-Fuller test confirmed that the original NIFTY 50 price series was non-stationary.
- First-order differencing produced a stationary series, supporting an ARIMA differencing parameter of `d = 1`.
- ARIMA parameters were selected using the lowest Akaike Information Criterion on the training data.
- ARIMA and Prophet were evaluated on the same testing dates.
- Model accuracy was compared using MAE, RMSE and MAPE.
- The final model was retrained on the full available NIFTY 50 series before producing the 30-business-day forecast.

## Key Results

### Asset performance

- ICICI Bank recorded the strongest historical performance: 180.21% total return, 16.92% CAGR and a 0.38 Sharpe ratio.
- NIFTY 50 generated an 11.17% CAGR with the lowest annualised volatility, 17.89%.
- NIFTY 50 also produced the smallest individual-asset maximum drawdown, -38.44%.
- TCS recorded the largest maximum drawdown, -53.39%.

### Portfolio analysis

The five-stock portfolio assigned a 20% weight to each company.

| Metric | Equal-Weight Portfolio | NIFTY 50 |
|---|---:|---:|
| Total return | 96.36% | 100.89% |
| Annual return | 10.78% | 11.17% |
| Annual volatility | 19.76% | 17.89% |
| Sharpe ratio | 0.24 | 0.29 |
| Maximum drawdown | -37.31% | -38.44% |

The portfolio had a slightly smaller drawdown, but NIFTY 50 produced stronger overall and risk-adjusted performance.

### Correlation and regression

- Infosys and TCS had the strongest stock-to-stock return correlation, 0.73.
- HDFC Bank and TCS had the lowest selected-stock correlation, 0.29.
- ICICI Bank recorded the highest market beta, 1.24.
- TCS recorded the lowest beta, 0.76.
- The beta coefficients were statistically significant in the analysed sample.

### Forecasting comparison

| Model | MAE | RMSE | MAPE |
|---|---:|---:|---:|
| ARIMA(0,1,0) | 544.30 | 626.68 | 2.26% |
| Prophet | 1,705.80 | 1,735.80 | 7.14% |

ARIMA(0,1,0) produced the lowest error across all three measures. Prophet overestimated the holdout-period values by projecting a stronger upward trend.

The final ARIMA point forecast remained at 24,624.65, with a 30-business-day 95% confidence range of approximately 22,680.66 to 26,568.65. Because ARIMA(0,1,0) is a random-walk model without drift, the central forecast remains close to the latest observed value while uncertainty expands over time.

### Risk analysis

For an illustrative portfolio value of ₹10,00,000:

- One-day Historical VaR at 95% confidence: ₹17,075
- Historical CVaR: ₹28,569
- Parametric VaR: ₹19,975
- 30-day Monte Carlo VaR: ₹92,650
- 30-day Monte Carlo CVaR: ₹1,18,592
- Mean simulated terminal value: ₹10,15,399
- Probability of finishing below the initial value: 42.34%

VaR is not a maximum-loss guarantee. Extreme market events can create losses beyond the estimated thresholds.

## Repository Structure

```text
Financial-Time-Series-Forecasting-Risk-Analysis/
├── notebook/
│   └── Indian_Stock_Market_Forecasting_and_Risk_Analysis.ipynb
├── data/
│   ├── Indian_Financial_Time_Series_Dashboard_Data.xlsx
│   └── CSV_Files/
├── dashboard/                 # Added after Power BI development
├── images/                    # Dashboard previews and project visuals
├── README.md
└── requirements.txt
```

## Running the Project

1. Clone or download this repository.
2. Install the required libraries:

   ```bash
   pip install -r requirements.txt
   ```

3. Open the notebook in Jupyter Notebook or Google Colab.
4. Run all cells in order.
5. Historical values and model results may change when newer market data is downloaded.

## Power BI Dashboard

The `data` directory contains the Excel workbook and CSV tables required for the Power BI dashboard. The completed `.pbix` file and dashboard preview will be added to the `dashboard` and `images` directories.

### Power BI Data Dictionary

| Table | Purpose |
|---|---|
| `Historical_Prices` | Adjusted closing prices by date and asset |
| `Daily_Returns` | Daily simple returns for all analysed assets |
| `Portfolio_Performance` | Portfolio and NIFTY 50 returns and investment values |
| `Asset_Metrics` | Total return, CAGR, volatility, Sharpe ratio and drawdown |
| `Correlations` | Asset-to-asset daily-return correlations |
| `Regression_Results` | Alpha, beta, R-squared and residual volatility |
| `Forecast_Evaluation` | Actual test values and ARIMA/Prophet predictions |
| `Model_Metrics` | MAE, RMSE and MAPE comparison |
| `Future_Forecast` | Final 30-business-day ARIMA forecast |
| `Risk_Summary` | Historical VaR, CVaR and Parametric VaR |
| `Monte_Carlo_Summary` | Principal 30-day simulation outcomes |
| `Monte_Carlo_Distribution` | Terminal value and profit/loss for each simulation |
| `Portfolio_Weights` | Equal 20% allocations across the five stocks |

## Limitations

- Historical performance does not guarantee future performance.
- Yahoo Finance data may be revised or temporarily unavailable.
- ARIMA and Prophet rely primarily on historical price patterns and do not incorporate news, valuation, macroeconomic or sentiment variables.
- The Monte Carlo simulation assumes that historical means, covariances and return relationships provide a reasonable approximation of future behaviour.
- Transaction costs, taxes, liquidity constraints and portfolio rebalancing costs are excluded.

## Author

**Amlaan Mohanty**  
GitHub: [AmlaanMohanty](https://github.com/AmlaanMohanty)
