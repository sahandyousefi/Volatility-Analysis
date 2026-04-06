# Netflix Stock Volatility Analysis and Risk Estimation

A quantitative finance project applying time series analysis techniques to Netflix historical stock data. The analysis covers exploratory data analysis, volatility measurement through rolling statistics and Bollinger Bands, downside risk estimation via Value at Risk (VaR), and short-term volatility forecasting using the GARCH(1,1) model.

---

## Overview

Understanding volatility is central to equity risk management, options pricing, and portfolio construction. This project analyzes Netflix (NFLX) stock price history to quantify how risk evolves over time, identify periods of elevated uncertainty, and forecast near-term volatility using industry-standard econometric methods.

The notebook is structured as a fully documented analytical pipeline, with mathematical formulations and interpretation provided alongside each technique. The dataset is sourced from the Netflix Stock Price History dataset on Kaggle.

---

## Dataset

The dataset (`Netflix_stock_data.csv`) contains daily OHLCV (Open, High, Low, Close, Volume) price data for Netflix stock.

| Feature | Description |
|---|---|
| `Date` | Trading date — used as the time series index |
| `Open` | Opening price for the trading session |
| `High` | Highest price reached during the session |
| `Low` | Lowest price reached during the session |
| `Close` | Closing price for the trading session — primary analysis variable |
| `Volume` | Number of shares traded during the session |

The `Date` column is set as the DataFrame index to enable time-aware operations throughout the analysis.

---

## Methodology

### 1. Exploratory Data Analysis

- Inspected dataset shape, descriptive statistics (`mean`, `std`, `min`, `max`, percentiles), and null value counts
- Verified data integrity before proceeding to feature engineering
- Plotted Netflix closing price over the full historical range to identify long-term price trends and structural breaks

### 2. Feature Engineering and Visualization

**Daily Returns**

Daily percentage returns were computed as:

    Return_t = (P_t - P_(t-1)) / P_(t-1)

A histogram with KDE overlay was plotted to assess the return distribution, revealing the degree of tail risk and whether returns approximate a normal distribution.

**Correlation Heatmap**

A Seaborn correlation heatmap was generated across all numeric features (Open, High, Low, Close, Volume) to identify collinearity and the relationships between price dimensions.

**Moving Averages**

50-day and 200-day simple moving averages (SMA) were overlaid on the closing price chart. The 50/200-day MA crossover is a widely used technical signal for identifying trend direction and potential regime changes.

---

### 3. Volatility Analysis

**Rolling Volatility (30-Day Window)**

Rolling standard deviation of daily returns over a 30-day window was computed to capture time-varying volatility:

    Volatility_t = STD(Return_(t-30) to Return_t)

This measure directly captures volatility clustering — the empirically observed tendency for high-volatility periods to be followed by further high-volatility periods, and vice versa.

**Bollinger Bands (20-Day Window)**

Bollinger Bands were constructed around the 20-day moving average using two standard deviations:

    Upper Band = MA_20 + 2 * STD_20
    Lower Band = MA_20 - 2 * STD_20

Price movements outside the bands signal statistically unusual deviations from the recent trend, useful for identifying breakout events and mean-reversion opportunities.

---

### 4. Value at Risk (VaR)

The parametric 95% Value at Risk was estimated using the normal distribution assumption:

    VaR_(95%) = mu - 1.65 * sigma

Where `mu` is the mean of daily returns and `sigma` is their standard deviation. The Z-score of 1.65 corresponds to the 5th percentile of the standard normal distribution.

**Result:**

| Confidence Level | VaR |
|---|---|
| 95% | -0.0555 (-5.55%) |

**Interpretation:** There is a 95% probability that Netflix's daily return will not fall below -5.55% on any given trading day. Equivalently, a daily loss exceeding 5.55% is expected to occur on approximately 1 in every 20 trading days — roughly 13 trading days per year.

---

### 5. GARCH(1,1) Volatility Modeling

**Motivation**

Standard statistical models assume constant variance. Financial return series, however, exhibit heteroskedasticity — variance changes over time and tends to cluster. The Generalized Autoregressive Conditional Heteroskedasticity (GARCH) model is the industry-standard approach to capturing this behavior.

**Model Specification**

The GARCH(1,1) model is defined as:

    sigma_t^2 = omega + alpha * epsilon_(t-1)^2 + beta * sigma_(t-1)^2

Where:
- `sigma_t^2` = conditional variance at time t
- `epsilon_(t-1)^2` = squared residual from the previous period (news/shock effect)
- `sigma_(t-1)^2` = previous period's conditional variance (persistence effect)
- `omega`, `alpha`, `beta` = parameters estimated via maximum likelihood

**Parameter Interpretation:**
- `alpha + beta < 1` indicates mean-reverting volatility
- High `alpha` implies rapid response to recent market shocks
- High `beta` implies persistent volatility with long memory

**5-Day Volatility Forecast Results:**

| Forecast Horizon | Forecasted Volatility (% per day) |
|---|---|
| Day 1 | ~2.42% |
| Day 2 | ~2.43% |
| Day 3 | ~2.43% |
| Day 4 | ~2.44% |
| Day 5 | ~2.45% |

**Interpretation:** The GARCH model forecasts stable, moderate volatility of approximately 2.42% to 2.45% per day over the next 5 trading sessions, indicating no imminent volatility spike in the short term at the time of analysis.

---

## Key Findings

- Netflix stock returns exhibit clear volatility clustering, validating the use of GARCH over constant-variance models.
- The 30-day rolling volatility chart reveals distinct periods of elevated risk corresponding to major market events and earnings surprises.
- Bollinger Band breaches identify moments of statistically significant price dislocation from the short-term mean.
- The 95% VaR of -5.55% establishes a practical daily loss threshold for risk management purposes.
- The GARCH(1,1) conditional volatility plot confirms that variance is time-varying — a critical insight for derivatives pricing, margin setting, and portfolio risk budgeting.
- The 5-day GARCH forecast of approximately 2.4% daily volatility signals moderate and stable short-term market uncertainty at the time of the analysis.

---

## Project Structure

    Netflix-Volatility-Analysis/
    |-- netflix-volatility-analysis.ipynb    # Full pipeline: EDA, volatility, VaR, GARCH
    |-- README.md

---

## Technologies Used

- Python 3
- Pandas, NumPy — data manipulation, return calculation, rolling statistics
- Matplotlib, Seaborn — time series plots, heatmaps, return distribution visualization
- arch — GARCH(1,1) model fitting and volatility forecasting
- Jupyter Notebook — interactive development and documentation
- Kaggle — dataset source and execution environment

---

## Getting Started

1. Clone the repository:

       git clone https://github.com/sahandyousefi/Netflix-Volatility-Analysis.git
       cd Netflix-Volatility-Analysis

2. Install dependencies:

       pip install pandas numpy matplotlib seaborn arch jupyter

3. Place `Netflix_stock_data.csv` in the input directory, or update the file path in the notebook to match your local setup.

4. Launch the notebook:

       jupyter notebook netflix-volatility-analysis.ipynb

---

## Author

Sahand Yousefi
[GitHub](https://github.com/sahandyousefi) | [LinkedIn](https://www.linkedin.com/in/sahand-yousefi/)

---

## License

This project is open-source and available for educational and reference purposes.
