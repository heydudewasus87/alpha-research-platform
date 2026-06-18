# Results

A breakdown of what the Alpha Research Platform found when run on real market data. The
goal of the project is simple: can a rules-based strategy beat the lazy approach of just
owning every stock equally? 

**Setup:** 40 large US stocks · daily data from Yahoo Finance · Jan 2015 – Dec 2024 ·
results are net of trading costs · the strategy was rebalanced monthly using only
information available at each point in time.

---

## Results

The strategy (blue) turned **\$1 into about \$7.50** over ten years. Simply owning all 40
stocks equally (the dashed "benchmark") turned \$1 into about \$4.50. The strategy also fell
*less* during the bad stretches.


<img width="1314" height="581" alt="image" src="https://github.com/user-attachments/assets/233d6fac-c511-4044-b46a-33d8a0de0566" />


*Top: growth of \$1, strategy vs. benchmark. Bottom: drawdown (how far below its peak the
strategy was at any time).*

---

## Performance vs. benchmark

Every number that matters came out ahead of the benchmark.

| Metric | Strategy | Benchmark | What it means |
|--------|----------|-----------|---------------|
| **Sharpe ratio** | **1.15** | 0.93 | Return per unit of risk, the higher the better. |
| **CAGR** | **23.0%** | 16.7% | Average growth per year. |
| **Max drawdown** | **−29.5%** | −34.4% | Worst peak-to-trough drop. Closer to zero is better. |
| **Sortino** | **1.42** | 1.12 | Like Sharpe, but only penalizes downside swings. |
| **Calmar** | **0.78** | 0.49 | Yearly return vs. worst-case loss. |
| **Hit rate** | **57.1%** | 55.8% | Share of days that ended positive. |

The notable part: the strategy delivered **more return *and* less drawdown** at the same
time. You normally only get more return by taking more risk, so improving both is an ideal result.

---

## What drove the returns

The strategy blends five classic signals. Each is scored by **Information Coefficient
(IC)** which I made a measure of predictive skill where, in this field, even 0.02–0.05 is useful.

<img width="1080" height="435" alt="image" src="https://github.com/user-attachments/assets/de574bbd-5835-45d2-bf71-857eafd92af0" />


- **Momentum** (IC +0.07) and **Quality** (IC +0.09) were the strongest, positive
  predictors. Quality was the most *consistent* (highest ICIR).
- **Short reversal** was weakly positive.
- **Low volatility** (−0.02) and **Value** (−0.13) had *negative* predictive value over this
  period, so the system automatically dropped them from the blend.

The big negative on **Value** makes economic sense because cheap stocks badly lagged expensive tech
from 2015–2024. The platform correctly detected this and excluded value rather than letting
it drag on returns.

The final blend therefore used **quality + momentum + a little short-reversal.**

---

## The full tearsheet

<img width="848" height="639" alt="image" src="https://github.com/user-attachments/assets/ac4b734f-9213-43b7-ac25-095c275d03ae" />


The **rolling 1-year Sharpe** panel is the most honest chart here. It dips below zero in
2019 and again in 2022–23 meaning there were full years where the strategy underperformed
or lost money. The headline 1.15 Sharpe is the *average*.

---

## Limitations

Even though the project had a good backtest, there are three things to keep in mind before
reading too much into the results:

**1. The universe is a small set of known winners.** These 40 stocks (AAPL, MSFT, NVDA, …)
were excellent performers no matter what and that's why even the do-nothing benchmark returned
16.7% a year. A lot of the absolute return reflects a great decade for US mega-caps, not
pure strategy skill. The honest measure of skill is the *edge over the benchmark* (1.15 vs.
0.93 Sharpe), which is real but small.

**2. The attribution analysis is unreliable in this version.** The return-attribution
regression below reports an **R-squared of 0.01**, meaning it explains almost nothing about
the strategy's returns and it contradicts the IC analysis (it labels momentum as negative
even though momentum had positive predictive skill and earned a place in the blend).

<img width="196" height="149" alt="image" src="https://github.com/user-attachments/assets/5fca45f2-33da-4554-9742-384345a778ba" />


The cause is that this regression uses a simplified version of each signal that differs from
how the signal is actually used by the optimizer. I treat this table as noise, not signal.


**3. Value and quality use proxy data.** Without a fundamentals data feed connected, the
value and quality signals are approximated from price behavior rather than real company
financials (ROE, book value). So I leaned on **momentum and quality** as the trustworthy
drivers and don't over-claim the value finding. Connecting real fundamentals (via FMP or SEC
EDGAR) is the top item on the roadmap.

---

## Bottom line

On real data, net of costs, with no look-ahead, the strategy beat a passive equal-weight
benchmark on every risk-adjusted metric. That's a solid result for a research prototype. 

*This is a research and educational project, not investment advice. Past or simulated
performance does not predict future results.*
