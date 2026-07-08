# GitHub Profile README — Progress Report

## 1. Claim Verification

Every technical claim in the profile README was cross-checked against actual
source files in this session (not taken from the task brief on faith):

- **quantbot**: verified against `my-quant-bot/README.md` directly. "WF
  per-trade Sharpe 0.60" and "22.6% max drawdown" for Variant H are exact
  quotes from that README's own tables (lines 79, 98-99). The five rejected
  extensions (volatility targeting, synthetic covered calls, managed-futures
  proxies, ML regime classifier, universe expansion) are the exact five
  listed in that README's Research Results table — confirmed count and
  names, not assumed. Bonferroni sweep, bit-exact regression gate
  (471,874.87/328 trades), and walk-forward (5y IS/1y OOS) language all
  quoted from the same source.
- **stat-arb-research**: verified against `my-quant-bot/stat_arb/RESEARCH_REPORT.md`
  directly (63KB, six dated experiment sections). Confirmed verdicts:
  equity ETF pairs "DO NOT PROCEED" (cointegrated fallback pair, but "no
  exploitable spread amplitude after costs"); crypto L1 pairs "DO NOT
  PROCEED" (amplitude confirmed, but not cointegrated / "amplitude but no
  reversion"); spot/perp basis "reversion is confirmed" but amplitude too
  small to clear cost threshold. Funding carry: report states gross yield
  "~11.8% annualized annualized" and a cost-aware version delivering
  "~6-9% net annualized, beating cash" — I used "~12%" as a rounding of
  11.84%, matching the brief.
- **cpp-options-pricer**: this is the project I built and tested directly in
  prior sessions in this conversation — the 47/47 convergence result, the
  4.52e-8 Greeks disagreement, and the $0.086 LSM quadratic-basis bug are
  all numbers I generated and verified myself via actual re-runs, not
  secondhand claims.

- **fed-sentiment-research**: built and verified directly in the prior session that produced this card. The r = +0.49/+0.52 test-set announcement-day correlations, the 0/108 forward Bonferroni result, the 19-24 day minutes release lag, the 34/34 test count, and the pre-2015 embedding cutoff are all numbers generated from the actual validation run — not secondhand claims.

**All four repos' claims check out against their actual source material.**

## 2. Claims to Double-Check Before Publishing

- **fed-sentiment-research repo is not yet on GitHub** — the new card links to `https://github.com/BrandonKKY/fed-sentiment-research`, but the repo has not been git-initialized or published. The link will 404 until the repo is live. Publish it before pushing this profile update, or push both simultaneously.

- **LinkedIn URL and email are placeholders** (`linkedin.com/in/your-handle-here`,
  `your-email@example.com`) — must be replaced with real values before this
  goes live. Left as placeholders per the task brief, not an oversight.
- **cpp-options-pricer's own CI badge** (in that repo's README, added in a
  prior session) assumes the GitHub repo is named exactly
  `BrandonKKY/cpp-options-pricer`. If the actual repo name differs, that
  badge URL needs a one-line fix — unrelated to this profile README, but
  worth remembering since this profile page also links to that repo.
- **"Currently running QuantBot live in Alpaca's paper-trading environment"**
  — this reflects the state as of the my-quant-bot README and prior session
  notes (bot was deployed and RiskDaemon healthy as of the last recorded
  check). I have not re-verified the bot is running *right now* — confirm
  it's still active before publishing, or soften the line if it's since
  been stopped.
- **stat-arb-research's funding-carry number** — the report shows gross
  11.84% and a maker-fee scenario reaching net 8.6%, with a net-1.45%
  figure under a different (taker-fee) cost assumption. "6-9% net" is the
  report's own stated range for a cost-aware implementation, but it depends
  on which fee assumption is used — worth being ready to explain that
  nuance if a recruiter asks for the number behind the number.

## 3. Creating the Special "BrandonKKY" Repo

GitHub renders a repo's README on the profile page automatically only if
the repo name matches the account username exactly. Steps:

1. On GitHub, create a **new public repository** named exactly `BrandonKKY`
   (must match the account name character-for-character).
2. Initialize it with a README when prompted, or leave it empty — either
   way, the file that needs to end up at the repo root is `README.md`.
3. Push the content from `C:\Users\Acer\OneDrive\Desktop\BrandonKKY-profile\README.md`
   as that repo's root `README.md` (this folder contains only the README
   and this report — the report itself should NOT be pushed, only
   `README.md` belongs in the profile repo).
4. GitHub detects the username match automatically — no special settings
   or flags needed. The README appears on `github.com/BrandonKKY` (the
   profile page) within a minute or two of the push.
5. Optional: GitHub also shows a prompt on the repo's own page ("Add a
   README to your profile!") the first time this special repo is created,
   confirming it's been recognized.

This repo should contain **only `README.md`** (and optionally a LICENSE if
desired, though not required for a profile repo) — no source code, no other
project files.
