# Volatility-Analysis
Analyzed Netflix stock data with Bollinger Bands, Value at Risk (VaR), and GARCH(1,1) to understand trends, volatility, and short-term risk.

# 📈 Netflix Stock Time Series Analysis and Volatility Modeling

This project is a complete time series analysis of Netflix stock data using Python. It covers Exploratory Data Analysis (EDA), risk estimation, and volatility modeling using traditional and statistical techniques including GARCH.

---

## 📁 Dataset

- `Netflix_stock_data.csv`
- Columns: `Date`, `Open`, `High`, `Low`, `Close`, `Volume`

---

## 🔍 Project Goals

1. Perform professional-grade **EDA** on Netflix stock data.
2. Visualize stock price behavior and key technical indicators.
3. Analyze **volatility** using Rolling Std Dev and Bollinger Bands.
4. Estimate **Value at Risk (VaR)**.
5. Model and forecast **volatility using GARCH(1,1)**.

---

## 🧠 Techniques Used

### ✅ Exploratory Data Analysis (EDA)
- Line plot of Close prices
- Correlation heatmap
- Daily returns histogram
- 50-day and 200-day moving averages

### ✅ Volatility Analysis
- 30-day Rolling Standard Deviation
- Bollinger Bands (20-day MA ± 2×STD)
- Value at Risk (VaR) at 95% confidence:
  - Formula: `VaR_95% = μ - 1.65 × σ`

### ✅ GARCH Modeling
- Applied **ARCH package**
- Fitted **GARCH(1,1)** on percentage returns
- Forecasted 5-day volatility
- Plotted **conditional volatility**

---

## 📊 Results

- VaR (95% confidence): ~**-5.55%**
- GARCH(1,1) forecasted daily volatility: **~2.42%–2.45%**
- Conditional volatility plot shows clear **volatility clustering**

---

## 📌 Skills Demonstrated

- Time Series Modeling
- Risk Management Concepts (VaR, Volatility)
- GARCH Modeling
- Python Data Analysis (Pandas, Matplotlib, Seaborn, Plotly)
- Statistical Thinking

---

## 🚀 Future Work

- Add GARCH-based VaR estimation
- Forecast price using Prophet or LSTM
- Build a **Streamlit dashboard** for interactive risk analytics

---

## 🧑‍💻 Author

**Sahand** – Data Analyst | Aspiring Data Scientist  
**Focus:** Time Series, Machine Learning, Risk Modeling  
[LinkedIn] | [Portfolio] | [GitHub Profile]

---

## 📎 License

This project is for educational and portfolio use.
