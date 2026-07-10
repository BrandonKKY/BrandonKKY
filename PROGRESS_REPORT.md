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

- ~~fed-sentiment-research repo is not yet on GitHub~~ — **RESOLVED** as of the 2026-07-09 session (§4 below): `git ls-remote` confirms the repo is live.

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

---

## 4. Session Update (2026-07-09) — Sixth Project Card Added

### What changed

Added `order-book-simulator` as the sixth featured project card, matching the
existing format exactly (title link + one-line descriptor, intro paragraph,
bullet list of technical highlights, bolded **"The honest part:"** closing
paragraph, `---` separator). Placed after the fed-sentiment-research card and
before Research Philosophy, since the project's own pitch — "different in
kind, not degree, from every other project here" — reads best as the closing
entry in the list rather than slotted in the middle.

Also updated, per instructions, every occurrence of "five projects" language
that actually referred to the project count (not the unrelated "five" counts
inside individual cards — QuantBot's five rejected alpha extensions, stat-arb's
five-of-six failed hypotheses, etc., which are correct as written and were
left untouched):
- Intro paragraph: "Five projects" → "Six projects," plus one added sentence
  acknowledging that the order book's validation is a correctness gate, not a
  walk-forward split — because forcing that framing onto a deterministic
  matching engine would have been dishonest.
- Research Philosophy: "these five projects" → "six projects," "the five
  repos" → "the six repos," and the order book's 12-test gate added alongside
  the pricing engine's convergence checks and QuantBot's regression gate as a
  third example of the same discipline. Left the "eleven-plus documented
  experiments" figure untouched — that count refers to narrative research
  experiments (QuantBot's 5 rejected extensions + stat-arb's 6 experiments =
  11), not raw test-assertion counts, and the order book's tests don't belong
  in that bucket.
- Technical Skills: added `market microstructure`, `order flow imbalance
  (OFI)` to Quantitative Methods; added `limit order book matching engine
  (price-time priority matching, self-trade prevention)` to Systems &
  Infrastructure — this phrasing embeds all four required terms from the task
  brief (market microstructure, limit order book, price-time priority
  matching, order flow imbalance) without a redundant fifth bullet.

### Numbers verified, not copied from the task brief

Before writing the card, I re-read `order-book-simulator/README.md` directly
(not the task brief) to confirm the 12/12 test result and the specific bug
story (stress test's vacuous audit — caught and fixed by auditing at three
phases). The three benchmark numbers quoted (**3.4M** insertions/sec, **2.2M**
cancellations/sec, **3.1M** crossing-limit matches/sec) match the raw
`benchmark_main` output in that repo's own README (3,402,815 / 2,203,162 /
3,142,549 per second) — rounded the same way the other cards round their
numbers (e.g., "~12%" for stat-arb's 11.84%).

### Link verification — all six resolve

Ran `git ls-remote` against all six project repos plus the special `BrandonKKY`
profile repo itself:

```
quantbot: LIVE
stat-arb-research: LIVE
cpp-options-pricer: LIVE
portfolio-risk-dashboard: LIVE
fed-sentiment-research: LIVE
order-book-simulator: LIVE
BrandonKKY: LIVE
```

All seven resolve on GitHub. This also closes the prior session's open flag
about fed-sentiment-research not yet being published (§2, now struck through).

Additionally confirmed `order-book-simulator`'s local git HEAD
(`512e8e8`) matches its `origin` HEAD — the verified 12/12 gate output and
real benchmark numbers referenced in the new card are the same content
already live on GitHub, not numbers sitting only in an unpushed local copy.

### Flags before publishing this update

- **This repo's `README.md` change is staged locally but not committed or
  pushed.** Prior sessions committed each card addition individually (see
  `git log`: "Add fed-sentiment-research as fifth featured project", etc.) —
  if that pattern should continue, this needs a commit ("Add
  order-book-simulator as sixth featured project") and a push. Left
  uncommitted deliberately: git pushes are the kind of action this assistant
  confirms before taking, not something to do silently.
- **LinkedIn URL and email are still placeholders** (`linkedin.com/in/your-handle-here`,
  `your-email@example.com`) — carried over from the prior session's flag,
  still unresolved, still needs real values before this goes live.
- **cpp-options-pricer's CI badge** (unrelated repo, flagged in a prior
  session) — not re-checked this session; still worth confirming the badge
  URL matches the actual repo name before treating the whole portfolio as
  publish-ready.
- **"Currently running QuantBot live"** line (Currently section) — not
  re-verified this session; same caveat as before, confirm the bot is still
  active or soften the line.

---

## 5. Session Update (2026-07-10) — Eighth Project Card Added

### What changed

Added `cross-sectional-momentum` as the eighth featured project card, matching
the existing format exactly (title link + one-line descriptor, intro
paragraph, bullet list of technical highlights, bolded **"The honest part:"**
closing paragraph, `---` separator). Placed it **between ml-alpha-research and
order-book-simulator**, not appended at the end — continuing the placement
pattern from the prior session (§4): order-book-simulator's own pitch ("different
in kind, not degree, from every other project here") reads best as the closing
entry in the list, so new cards slot in before it rather than after.

Updated every "seven projects" occurrence that referred to the project count:
- Intro paragraph: "Seven projects" → "Eight projects," with one clause added
  describing cross-sectional-momentum as "an academic-style cross-sectional
  factor study testing the classic Jegadeesh-Titman momentum anomaly across
  100+ US equities" — placed in the list in the same position as its card
  (between the ml-alpha description and the order-book description).
- Research Philosophy: "these seven projects" → "these eight projects," "the
  seven repos" → "the eight repos." Added cross-sectional-momentum's
  walk-forward result alongside ml-alpha-research's in the Bonferroni sentence
  (both are five-window walk-forwards that fail to clear the bar — genuinely
  parallel structure, not a stretch to pair them). Extended "four different
  angles" → "five different angles" and added the project's 14-test integrity
  suite to that list. Left "eleven-plus documented experiments" untouched —
  per the existing convention (§4 of this report), that count is QuantBot's 5
  rejected extensions + stat-arb's 6 experiments, and neither ml-alpha-research
  nor cross-sectional-momentum's test suites belong in that bucket.
- Technical Skills (Quantitative Methods): added `Fama-MacBeth regression` and
  `factor decay analysis`. **Did not** add a separate `cross-sectional factor
  research` term as literally listed in the task brief — `cross-sectional
  alpha research` is already present in that line (added when ml-alpha-research
  was carded) and putting a near-synonymous phrase directly next to it would
  read as padding rather than a distinct skill. Confirmed `Newey-West standard
  errors` was already present (also from the ml-alpha-research addition) — no
  change needed there, per the brief's own instruction to confirm rather than
  duplicate.

### Numbers verified, not copied from the task brief

Every figure in the new card was grepped out of the actual repo files in this
session before writing the card, not taken from the task instructions on
faith:

- **Root-commit claim**: `git log --oneline --reverse` on
  `cross-sectional-momentum` confirms `6b321fb "Pre-registration: hypothesis,
  timeline, look-ahead risks (before any code)"` is genuinely the first commit,
  predating `d241fb7` (the first commit containing any `.py` file). The card's
  claim that git history proves the pre-registration is literal fact, not
  marketing language.
- **Fama-MacBeth t-stat**: `RESEARCH_REPORT.md` line 197 shows `mom_12_1` NW
  t = **−0.67** in-sample — matches the card exactly.
- **OOS net Sharpe**: line 246, stitched OOS net Sharpe **+0.02** — matches.
- **Skip-1 IC**: line 298 and line 331, `mom_1_0` IC = **−0.020** — matches
  the card's "reversal, not continuation" claim word for word.
- **Crash months**: line 299, worst months Feb-09 (−28%), Jan-09 (−21%),
  Aug-02 (−19%) — the card quotes these three (of five reported) as the most
  recognizable crash dates.
- **Kellanova delisting**: confirmed in `data/loader.py` line 54, an inline
  comment documenting the ticker was delisted in the 2025 Mars acquisition
  before the initial data download — this happened live during the build
  session, not a hypothetical example.
- **14/14 tests**: re-ran `pytest tests/ -q` in this session — **14 passed**,
  0 failed, confirming the count independently rather than trusting the prior
  session's report.

### Link verification — all nine resolve

Ran `git ls-remote` against all eight project repos plus the special
`BrandonKKY` profile repo:

```
quantbot: LIVE
stat-arb-research: LIVE
cpp-options-pricer: LIVE
portfolio-risk-dashboard: LIVE
fed-sentiment-research: LIVE
order-book-simulator: LIVE
ml-alpha-research: LIVE
cross-sectional-momentum: LIVE
BrandonKKY: LIVE
```

All nine resolve on GitHub, including `cross-sectional-momentum` — the repo
was pushed to GitHub at some point after the local build session that created
it (this session found it already live; no push was performed as part of this
update).

### Flags before publishing this update

- **This session's `README.md` change IS committed locally**
  (`3a160a9 "Add cross-sectional-momentum as eighth featured project"`) but
  **has not been pushed**, per explicit instruction not to push. Run `git push`
  from `C:\Users\Acer\OneDrive\Desktop\BrandonKKY-profile` when ready to
  publish.
- **LinkedIn URL and email**: these are now real values
  (`linkedin.com/in/brandon-kky/`, `brandonkky@gmail.com`), not the placeholders
  flagged in §2 — that flag is now stale and can be considered resolved, though
  it was resolved in an earlier session, not this one.
- **cpp-options-pricer's CI badge** — not re-checked this session; carried
  forward from §4, still worth a final look before treating the whole
  portfolio as publish-ready.
- **"Currently running QuantBot live"** line — not re-verified this session;
  same standing caveat as §4.
- **Editorial judgment call flagged above** (skipping the redundant
  `cross-sectional factor research` skill term): if a literal 1:1 match to the
  task brief's wording is wanted instead, that's a one-line addition to the
  Quantitative Methods line — flagging it here rather than silently deciding
  and moving on.
