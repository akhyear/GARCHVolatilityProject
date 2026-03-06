GARCH Volatility Research

This project explores volatility modeling for the S&P 500 using GARCH models and compares the forecasts with historical volatility and the VIX. The goal is to understand how different volatility estimates behave and whether model based forecasts can improve upon simple historical measures.

Volatility is a central concept in quantitative finance. Portfolio risk, derivative pricing, and many systematic trading strategies depend on reliable volatility estimates. In this project I build a small research pipeline that starts from raw market data and gradually moves toward model estimation and out of sample testing.

The project focuses on three volatility perspectives:

- Historical Volatility – backward looking estimate from past returns
- GARCH Volatility – conditional variance model estimated from data
- Implied Volatility (VIX) – market expectation of future volatility

The comparison between these three gives insight into how markets price risk.

---

Project Goals

- Study volatility clustering in financial returns
- Implement a full GARCH(1,1) model workflow
- Estimate the model using the "arch" library
- Implement GARCH from scratch using Maximum Likelihood
- Evaluate forecasts with out of sample backtesting
- Compare model forecasts with VIX implied volatility

---

Data

The project uses daily market data for:

- S&P 500 Index ("^GSPC")
- VIX – CBOE Volatility Index ("^VIX")

Data is downloaded using the "yfinance" Python package.

From the price data we compute log returns:

r_t = log(P_t / P_{t-1})

These returns are used for volatility estimation.

---

Project Structure

GARCHVolatilityProject
│
├── data
│   ├── raw
│   └── processed
│
├── notebooks
│   ├── 01_data_collection.ipynb
│   ├── 02_volatility_stylized_facts.ipynb
│   ├── 03_historical_volatility_benchmark.ipynb
│   ├── 04_garch_modeling_with_arch.ipynb
│   ├── 05_garch_from_scratch_mle.ipynb
│   └── 06_multistep_forecasting_backtesting.ipynb
│
├── src
│   ├── 
│   └──
│
├── main.py
└── README.md

---

Research Workflow

1. Data Pipeline

The project begins with downloading market data and computing daily log returns. Cleaned datasets are stored in the "data/processed" folder so experiments remain reproducible.

---

2. Stylized Facts of Financial Returns

Before building any model we examine common empirical properties of financial time series:

- volatility clustering
- heavy tails
- autocorrelation of squared returns

These properties motivate the use of conditional volatility models such as GARCH.

---

3. Historical Volatility Benchmark

A simple rolling standard deviation is used as a baseline volatility estimator.

This provides a benchmark against which GARCH forecasts can be evaluated.

---

4. GARCH(1,1) Model using "arch"

We estimate the standard GARCH(1,1) model:

σ²_t = ω + α ε²_{t−1} + β σ²_{t−1}

The model captures volatility clustering and persistence commonly observed in equity returns.

The estimated conditional volatility series is compared with:

- historical volatility
- VIX implied volatility

---

5. GARCH Implementation from Scratch

To understand the model deeply, the project reimplements GARCH estimation manually.

Steps include:

- variance recursion
- log likelihood construction
- parameter estimation via Maximum Likelihood
- numerical optimization with "scipy"

This step shows how volatility models are actually estimated in practice.

---

6. Forecasting and Backtesting

The final stage evaluates volatility forecasts using rolling out of sample testing.

Models compared:

- Historical Volatility
- GARCH(1,1)
- VIX implied volatility

Evaluation metrics:

- Mean Squared Error (MSE)
- QLIKE loss

This allows us to test whether the model improves volatility forecasting performance.

---

Example Insight

Financial markets usually show high volatility persistence.

In many GARCH estimates:

α + β ≈ 0.95

This means volatility shocks decay slowly and today's volatility strongly depends on yesterday's conditions.

---

Requirements

Main libraries used in the project:

numpy
pandas
matplotlib
scipy
arch
yfinance

Install them with:

pip install -r requirements.txt

---

Motivation

This project was built as part of a learning journey into quantitative finance and volatility modeling. The focus is not only on using models but also understanding the mathematics and estimation methods behind them.
