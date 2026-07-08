### Building systematic trading infrastructure — from execution engines to numerical pricing tools to the risk layer that ties them together — with every claim backed by out-of-sample proof.

Five projects below cover the full stack: a live trading system, a statistical arbitrage research framework, a derivatives pricing engine, a risk-attribution dashboard that unifies the first two into a single book, and a text-analytics research framework testing whether Federal Reserve communications carry exploitable market signal. The common thread isn't the returns — it's the discipline: walk-forward validation, multiple-testing correction, and honest rejection when a hypothesis — or a statistic — doesn't survive contact with held-out data.

---

### [quantbot](https://github.com/BrandonKKY/quantbot) — Production C++ Algorithmic Trading System

A C++17 trading bot that runs the *same* engine live and in backtesting, so what gets measured offline is exactly what trades.

- Walk-forward validated (rolling 5y in-sample / 1y out-of-sample) on a SPY/QQQ/IWM/GLD trend-following rotation — **Variant H**: per-trade Sharpe **0.60**, max drawdown **22.6%**
- Parameter sweeps corrected with a **Bonferroni** hurdle, not picked from the top row of an uncorrected grid
- Every refactor must reproduce a **bit-exact regression gate** (471,874.87 final equity / 328 trades) before merging
- Live on Alpaca's paper-trading environment; background reconciliation daemon repairs orphaned positions and renews bracket orders before expiry

**The honest part:** five separate alpha extensions — volatility targeting, synthetic covered calls, managed-futures overlays, an ML regime classifier, universe expansion — were built, measured out-of-sample, and **all five rejected**. None beat the baseline on a walk-forward basis. That's not a stalled project; it's what happens when you actually check.

---

### [stat-arb-research](https://github.com/BrandonKKY/stat-arb-research) — Statistical Arbitrage Research Framework

A Python research framework testing pairs-trading and carry hypotheses across equities and crypto, with cointegration and cost-realism gates applied *before* any hypothesis is allowed to look promising.

- Six documented experiments, each run through the same gauntlet: Engle-Granger/Johansen cointegration, Bonferroni-corrected pair screening, realistic execution costs
- Equity ETF pairs, crypto L1 pairs, and spot/perpetual basis convergence: all **rejected** — respectively for no exploitable amplitude after costs, amplitude with no mean reversion, and reversion too small to clear round-trip cost
- The one surviving edge: **BTC funding-rate carry** (delta-neutral long-spot/short-perp) — ~12% gross annualized yield, **6–9% net** after realistic execution costs, clearing the 4.5% cash hurdle

**The honest part:** five of six hypotheses failed, and the report says so in as much detail as the one that worked. The funding-carry result survives specifically *because* it was tested with the same skepticism that killed the other five.

---

### [cpp-options-pricer](https://github.com/BrandonKKY/cpp-options-pricer) — Options Pricing Engine

A standalone C++17 derivatives pricing library, zero external dependencies, built to prove the numerics rather than assert them.

- Three independent, cross-validating pricers: closed-form Black-Scholes, a Cox-Ross-Rubinstein binomial tree with American early exercise, and Monte Carlo with antithetic variates plus a hand-rolled Longstaff-Schwartz regression for American options
- **47/47** convergence checks passing — Monte Carlo and tree prices independently agree with the closed form across five parameter regimes
- Closed-form Greeks verified against finite differences to **4.52e-8** (tolerance was 1e-4); Newton-Raphson implied-vol solver with a bisection fallback for near-zero-vega cases
- CI badge — GitHub Actions runs the full 47-check gate on every push

**The honest part:** the test suite caught a real bug — an early quadratic regression basis mispriced a deep-in-the-money American put by $0.086 against the tree's reference price. Moving to a cubic basis fixed it. That's the tests doing their job, not a footnote to skip.

---

### [portfolio-risk-dashboard](https://github.com/BrandonKKY/portfolio-risk-dashboard) — Portfolio Risk & Attribution Dashboard

A Python/Streamlit dashboard that ingests the real log files from the two live systems above — QuantBot's C++ trading logs and stat-arb-research's funding-carry forward-paper tracker — and computes unified risk statistics across them as a single book, not two disconnected P&L feeds.

- Historical and parametric VaR/CVaR at 95%/99% confidence, with a sample-size reliability flag attached to every figure rather than presented as a settled number
- Flow-adjusted drawdown attribution: a naive sum would let one strategy's incoming capital mask another's real loss; this correctly separates capital flows from P&L before attributing the combined book's drawdown to its source
- Factor exposure via OLS regression (beta/alpha/R² to SPY and BTC) — statistically verifies a "market neutral" claim instead of asserting it, the same check applied to stat-arb-research's funding-carry book
- **28/28** tests passing against closed-form statistical answers (known z-score VaR, exact drawdown attribution, hand-derived Sharpe), with a rolling-Sharpe formula that matches carry_metrics.py exactly so numbers reconcile across projects

**The honest part:** with only ten days of live QuantBot data, the current Sharpe computes to roughly 4.4 — and the dashboard's own UI flags that as statistically unreliable rather than presenting it with confidence. The same rejection discipline that killed five of QuantBot's alpha extensions and five of stat-arb-research's six hypotheses applies here to the risk metrics themselves.

---

### [fed-sentiment-research](https://github.com/BrandonKKY/fed-sentiment-research) — FOMC Sentiment Research

A Python research framework that extracts hawkish/dovish sentiment from all FOMC statements and meeting minutes (2006–2026) and tests whether that signal predicts anything in equity or bond markets. The only text-based project in this portfolio — every other entry works on price and volume.

- Two independent scoring methods: a direction-word × policy-noun lexicon transcribed from Apel & Blix Grimaldi (Riksbank WP 261, 2012), and PPMI-SVD word embeddings (Levy & Goldberg 2014) built from scratch in numpy and trained *only on pre-2015 text* — preventing the training-data look-ahead contamination a pretrained model would have carried
- Primary hypothesis and all hyperparameters pre-registered in code before any correlation was computed — the strictest available guard against p-hacking
- **Measurement validated:** extended-lexicon hawkishness co-moves with same-day 2y/10y Treasury yield changes in *both* the train and test split (test: r = +0.49 / +0.52), surviving Bonferroni correction — the market reaction to FOMC communication is real and replicable
- **Prediction null:** 0 of 108 forward-looking hypotheses survive correction in either split; the top-5 in-sample correlations fail to replicate out of sample (3 of 5 flip sign); the pre-registered primary hypothesis fails outright with a sign flip from train to test
- **34/34** tests passing; FOMC minutes timestamped by their verified public release date (19–24 days after the meeting), not the meeting date, closing a real look-ahead trap that a naive implementation would miss

**The honest part:** the null result is the point. The market prices FOMC communication within the trading day — the yield reaction is contemporaneous and complete. Nothing survives at 1/5/21-day forward horizons. That finding is reported as a rigorous null rather than retrofitted into a weaker positive claim.

---

### Research Philosophy

Every result across these five projects is walk-forward or convergence validated before it's called a result — nothing here is a single cherry-picked backtest presented as a finding. Multiple-testing correction (Bonferroni) is applied wherever a sweep or a pair-screen could otherwise mistake luck for edge. Failure is reported with the same rigor as success: eleven-plus documented experiments and numerical checks across the five repos — plus 108 pre-registered forward hypotheses in the sentiment project, all of which concluded "reject" — because that's what the out-of-sample data actually said. The pricing engine's cross-validated numerics and the trading system's bit-exact regression gate serve the same purpose from opposite directions — proving the math is right before trusting what it implies. The risk dashboard applies the identical standard to the reporting layer itself: a Sharpe ratio or VaR figure carries a sample-size verdict, not a confident number standing alone.

---

### Technical Skills Demonstrated

**Languages & Tooling:** C++17, Python, CMake, GitHub Actions/CI, Git, Streamlit

**Quantitative Methods:** Walk-forward validation, Bonferroni multiple-testing correction, pre-registered hypothesis testing, cointegration testing (Engle-Granger, Johansen), Monte Carlo variance reduction (antithetic variates), Longstaff-Schwartz least-squares regression, Newton-Raphson root-finding, VaR/CVaR methodology, OLS factor regression (beta/alpha/R²), event study methodology, lexicon-based sentiment scoring, word embeddings (PPMI-SVD)

**Systems & Infrastructure:** Live broker integration (Alpaca REST API), risk management systems (circuit breakers, position reconciliation, bracket-order management), bit-exact regression testing, cross-system risk attribution (flow-adjusted drawdown attribution across heterogeneous P&L feeds)

**Data & Analysis:** pandas, statsmodels, scipy, Jupyter, NLP/text analysis (BeautifulSoup, PPMI-SVD embeddings)

---

### Currently

Running QuantBot live in Alpaca's paper-trading environment, monitoring the Variant H configuration against the walk-forward baseline.

---

### Contact

LinkedIn: [linkedin.com/in/your-handle-here](https://linkedin.com/in/your-handle-here)
Email: your-email@example.com
