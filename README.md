### Building systematic trading infrastructure — from execution engines to numerical pricing tools, with every claim backed by out-of-sample proof.

Three projects below cover the full stack: a live trading system, a statistical arbitrage research framework, and a derivatives pricing engine. The common thread isn't the returns — it's the discipline: walk-forward validation, multiple-testing correction, and honest rejection when a hypothesis doesn't survive contact with held-out data.

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

### Research Philosophy

Every result across these three projects is walk-forward or convergence validated before it's called a result — nothing here is a single cherry-picked backtest presented as a finding. Multiple-testing correction (Bonferroni) is applied wherever a sweep or a pair-screen could otherwise mistake luck for edge. Failure is reported with the same rigor as success: eleven-plus documented experiments and numerical checks across the three repos, six of which concluded "reject," because that's what the out-of-sample data actually said. The pricing engine's cross-validated numerics and the trading system's bit-exact regression gate serve the same purpose from opposite directions — proving the math is right before trusting what it implies.

---

### Technical Skills Demonstrated

**Languages & Tooling:** C++17, Python, CMake, GitHub Actions/CI, Git

**Quantitative Methods:** Walk-forward validation, Bonferroni multiple-testing correction, cointegration testing (Engle-Granger, Johansen), Monte Carlo variance reduction (antithetic variates), Longstaff-Schwartz least-squares regression, Newton-Raphson root-finding

**Systems & Infrastructure:** Live broker integration (Alpaca REST API), risk management systems (circuit breakers, position reconciliation, bracket-order management), bit-exact regression testing

**Data & Analysis:** pandas, statsmodels, Jupyter

---

### Currently

Running QuantBot live in Alpaca's paper-trading environment, monitoring the Variant H configuration against the walk-forward baseline.

---

### Contact

LinkedIn: [linkedin.com/in/your-handle-here](https://linkedin.com/in/your-handle-here)
Email: your-email@example.com
