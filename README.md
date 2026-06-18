# Alpha Research Platform

A systematic equity research engine in Python. It builds alpha signals, scores them by
Information Coefficient, blends them by conviction, runs the blend through a risk model and a
constrained optimizer, and backtests the result walk-forward with realistic transaction
costs — the same pipeline a quant fund uses to turn raw data into a managed portfolio.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_USERNAME/alpha-research-platform/blob/main/Alpha_Research_Platform.ipynb)

> Replace `YOUR_USERNAME` in the badge link above with your GitHub username.

---

## Quick start

1. Click the **Open in Colab** badge above.
2. In Colab, go to **Runtime → Run all**.
3. That's it. The notebook runs end to end on free data and produces the charts below.

No API keys are required. To use live market data instead of the built-in fallback, see
[Using your own data](#using-your-own-data).

---

## What it does

The notebook walks through the full research loop, one section per step:

| Step | What happens |
|------|--------------|
| **Data** | Pulls daily prices (Yahoo Finance) with a synthetic fallback |
| **Alpha Library** | Builds 5 signals: momentum, reversal, low-vol, value, quality |
| **Signal Evaluation** | Scores each signal by Information Coefficient (predictive power) |
| **Combination** | Blends signals, weighting the most consistent ones more heavily |
| **Risk Model** | Estimates a stable covariance matrix (shrinkage) |
| **Optimizer** | Picks portfolio weights: maximize alpha, control risk and turnover |
| **Backtest** | Rebalances monthly, walk-forward, charging realistic costs |
| **Performance** | Reports Sharpe, CAGR, drawdown vs. an equal-weight benchmark |
| **Attribution** | Shows which signals actually drove the returns |
| **Dashboard** | Interactive performance + drawdown chart |

---

## Results

The notebook produces a full tearsheet and an interactive dashboard:

<!-- After your first run, screenshot the tearsheet and drop it in here:
1. Run the notebook, right-click the tearsheet image, "Save image as..."
2. Drag that file into this README while editing it on GitHub
3. GitHub uploads it and inserts a link like the line below -->

![Strategy Tearsheet](tearsheet.png)

| Metric | Strategy | Equal-Weight |
|--------|----------|--------------|
| Sharpe | _fill in after running_ | _fill in_ |
| CAGR | _fill in_ | _fill in_ |
| Max Drawdown | _fill in_ | _fill in_ |

---

## How it stays honest

A backtest is only as good as its assumptions. This one is built to avoid the common traps:

- **No look-ahead.** On every rebalance date, the covariance and the alpha use past data
  only — never information from the future.
- **Real costs.** Every rebalance is charged a turnover-based transaction cost.
- **A real benchmark.** Results are compared to an equal-weight portfolio, the honest hurdle
  any active strategy has to clear net of costs.

---

## Using your own data

The notebook runs on free synthetic data out of the box. Add API keys to upgrade each data
path. All keys are optional and free.

| Source | Unlocks | Where to get it |
|--------|---------|-----------------|
| SEC EDGAR | Real ROE from filings | No signup — just use `"Your Name your@email.com"` |
| FRED | Real risk-free rate | https://fred.stlouisfed.org/docs/api/api_key.html |
| Financial Modeling Prep | Clean fundamentals | https://site.financialmodelingprep.com/developer/docs |
| Alpha Vantage | Alternate data source | https://www.alphavantage.co/support/#api-key |

**Add keys safely (recommended):** in Colab, open the **Secrets** panel (key icon, left
sidebar) and add each key using the names `SEC_USER_AGENT`, `FRED_API_KEY`, `FMP_API_KEY`,
`ALPHA_VANTAGE_API_KEY`. The notebook loads them automatically and they never touch the
file. Never paste keys directly into the notebook if you plan to share it.

---

## Tech stack

Python · NumPy · pandas · SciPy · statsmodels · scikit-learn · Matplotlib · Plotly · yfinance

---

## Roadmap

- Point-in-time fundamentals from SEC EDGAR / FMP across the full universe
- A machine-learning alpha with purged, embargoed cross-validation
- Factor-based risk model with exposure constraints
- Market-impact-aware transaction costs
- Hosted interactive dashboard (Streamlit / Hugging Face Spaces)

---

## Disclaimer

This is a research and educational project, not investment advice. Past or simulated
performance does not predict future results.
