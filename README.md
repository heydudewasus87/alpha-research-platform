# Alpha Research Platform

A Python project that tries to build a smart stock portfolio and then tests how it
would have performed in the past. It scores stocks using several proven strategies,
combines those scores, decides how much money to put in each stock, and checks the
results, similar to how quant investment funds work.

---

## Background

A real fund doesn't pick stocks on gut feeling. It uses rules, tests them on history, and
measures everything. This project does the same thing in nine steps:

| Step | In plain words |
|------|----------------|
| **1. Get data** | Download daily stock prices |
| **2. Build signals** | Score every stock using 5 classic strategies (explained below) |
| **3. Test the signals** | Measure how good each strategy actually is at predicting |
| **4. Combine them** | Blend the strategies, trusting the better ones more |
| **5. Measure risk** | Figure out how the stocks move together (so we don't over-concentrate) |
| **6. Choose amounts** | Decide how much money goes into each stock |
| **7. Backtest** | Replay history month by month and track the results |
| **8. Score it** | Report how it did, compared to a simple "buy everything" benchmark |
| **9. Explain it** | Show which strategies actually earned the money |

---

## The 5 strategies ("signals")

Each one is a rule for ranking stocks from most to least attractive:

- **Momentum** — stocks that have been going up tend to keep going up for a while.
- **Reversal** — stocks that dropped very recently often bounce back a little.
- **Low volatility** — calmer, less jumpy stocks tend to do better than you'd expect.
- **Value** — cheap stocks (relative to their actual worth) tend to outperform over time.
- **Quality** — profitable, well-run companies tend to outperform weak ones.

These are well-documented patterns that real funds (like AQR and
Dimensional) build entire products around.

---

## Understanding the numbers

You'll see a results table. Here's what each number means and whether
it's good:

| Term | What it means | Rough guide |
|------|---------------|-------------|
| **Sharpe ratio** | How much return you got for the risk you took. The single most important number in investing. | Under 1 = okay · 1–2 = good · Over 2 = excellent · Over 3 = be suspicious (probably too good to be true) |
| **CAGR** | Your average growth per year, smoothed out. "10%" means it grew about 10% a year on average. | Higher is better, but only alongside the risk numbers |
| **Max drawdown** | The worst drop from a peak. "-30%" means at the lowest point you were down 30% from your previous high. | Closer to zero is better. Big losses are painful and hard to sit through |
| **Volatility** | How bumpy the ride is. High volatility = big swings up and down. | Lower is calmer |
| **Sortino ratio** | Like Sharpe, but it only counts the *downside* swings (ignores good surprises). | Higher is better |
| **Calmar ratio** | Yearly return divided by the worst drawdown. Reward vs. worst-case pain. | Higher is better |
| **Hit rate** | The fraction of days that ended positive. | Above 0.50 means more up days than down |

---

## Two terms you'll see in the charts

- **Information Coefficient (IC):** a score from -1 to +1 for how well a strategy's ranking
  matched what the stocks actually did next. **0 means no skill (a coin flip).** Here's the
  surprising part: in real quant investing, even an IC of **0.02 to 0.05 is considered
  genuinely useful**, because you're making thousands of small bets and the tiny edge adds
  up. So don't be alarmed that these numbers look small — that's completely normal.

- **Turnover:** how much of the portfolio gets traded at each rebalance. More trading means
  more cost, so lower is generally better.

---

## Why you can trust the results

- **No peeking at the future.** When deciding what to buy on a given day, it only ever uses
  information that existed *up to that day* — never tomorrow's prices.
- **It pays to trade.** Every time it buys or sells, it subtracts a realistic trading cost,
  just like in real life.
- **It compares to a fair benchmark.** Results are shown next to a simple "own a bit of
  everything" portfolio — the honest bar any strategy has to beat.


---

## Built with

Python, with NumPy, pandas, SciPy, statsmodels, scikit-learn, Matplotlib, and Plotly.

---

## A quick disclaimer

This is a learning and research project, not financial advice. Results based on past or
simulated data don't guarantee anything about the future.
