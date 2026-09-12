<div align="center">
<img src="assets/logo/t58-logo-horizontal-dark.png" alt="T58 Trading" width="280" />
</div>

# Features

A full breakdown of what's inside T58 Quant Algo Backtester, organized by
workflow stage. Get access: **[whop.com/t58-trading/t58-backtesting-engine](https://whop.com/t58-trading/t58-backtesting-engine/)**

---

## The core loop

Every feature in the app ultimately feeds one loop:

```
Market Data + Strategy + Risk + Prop-Firm Rules
        → Historical Backtest
        → Prop-Firm Simulation
        → Monte Carlo Simulation (thousands of simulated accounts)
        → Probability of Success
        → Comprehensive Report
```

**1. Upload market data** — CSV / TSV / Parquet / compressed archives,
with automatic column mapping and gap/duplicate detection. A sample
dataset is included to get started immediately; broader instrument data
(majors, gold, indices) is also bundled. Live data fetch for US
equities/crypto is supported for accounts connected to a brokerage feed.

**2. Import or build a strategy** in any of four formats, all reduced to
the same standardized signal series:

- **Manual Builder** — a full no-code visual strategy builder. Entry
  conditions across price, EMA/SMA/WMA/VWAP, RSI, MACD, ATR, Bollinger
  Bands, and market-structure concepts (swing highs/lows, liquidity
  sweeps, break of structure, fair value gaps, order blocks, session
  ranges). Exits via fixed or ATR-based stops/targets, trailing stops,
  break-even, and time-based exits.
- **Python** — bring your own signal-generation code.
- **PineScript** — a real parser for a tested subset of PineScript v5,
  including common indicators, crossover/crossunder logic, and
  strategy entry/exit calls.
- **MQL5** — a real parser for a tested subset of MQL5, including common
  indicator calls, trade execution calls, and standard order logic.

Both PineScript and MQL5 parsing **fail loudly** on anything unsupported
rather than silently producing an inaccurate backtest — you'll never get
a false "it worked" on a strategy that wasn't actually understood
correctly.

Every strategy can be checked for **lookahead bias** — the engine re-runs
signal generation on progressively truncated data and flags the exact bar
where a leak would first appear, before you ever trust a result built on
it.

**3. Enter your prop-firm's exact rules** — account size, profit target,
daily loss limit, max drawdown (trailing or static, intrabar or
end-of-day), consistency rules, and payout thresholds. Built-in
quick-fill presets for major prop firms save you from re-entering rules
by hand (dated, with a reminder to re-verify — firms change terms often).

**4. Configure risk and execution realism** — fixed-dollar or
percent-of-equity position sizing, commission, slippage, spread, and pip
size (with an automatic "detect from data" helper so you're not guessing).

**5. One click: backtest → prop simulation → Monte Carlo → report.**

---

## Create

- **Speed Run** — an all-in-one discover-to-verdict tool built for a hard
  deadline: a fast, wide multi-family search that feeds its best
  survivors straight into full validation, returning the strongest
  READY/MARGINAL candidate it can find. If nothing clears the bar, it
  turns the run's own rejection reasons into concrete next steps instead
  of leaving you guessing.
- **AI-Assisted Strategy Generation** — an optional local AI model drafts
  a new strategy from a plain-language description of an idea, saved into
  your strategy library for testing.
- **Research Agent** — a tool-calling AI assistant that investigates a
  strategy across several reasoning steps, calling only into the app's
  own validated engine (backtest, prop-sim, Monte Carlo, walk-forward,
  regime, sensitivity) — it reports what the engine actually found, never
  an invented number.

## Test

- **Run & Report** — the core workflow above, producing one
  comprehensive, shareable report (self-contained HTML, print-to-PDF
  friendly).
- **Payout Probability** — a full lifecycle simulation carrying a
  strategy through funding milestones (eval pass → funded → payout 1 →
  payout 2 → …), reporting a probability at *each* stage instead of one
  flat number. Includes an account-scaling stress test for firms that
  scale funded accounts up after consecutive payouts.
- **Prop-Firm Recommender** — flips the usual question around: given your
  strategy's actual trade sequence, ranks every supported prop firm's
  rule set by how well your strategy fits it, instead of checking firms
  one at a time by hand.

## Optimize

- **Search Lab** — a 5-stage funnel that generates and validates *many*
  candidates from a chosen strategy family in one run: candidate
  generation → cheap first-pass filter → genetic-algorithm refinement →
  full validation gate (Monte Carlo + walk-forward holdout + robustness +
  Deflated Sharpe) → ranked leaderboard with one-click champion promotion.
- **Iterative Refinement** — genetic-algorithm parameter search across
  every strategy source, toward a fitness metric you choose.
- **Full Pipeline** — one button chaining baseline backtest → lookahead
  check → walk-forward-aware GA → re-validated report → out-of-sample /
  holdout checks → a plain-language READY / MARGINAL / NOT READY verdict
  with the actual reasons behind it. Winners save themselves to your
  strategy library automatically.
- **Quick Optimize** — a lighter, single-strategy version of Full
  Pipeline for fast iteration.
- **Multi-Objective Optimization** — a genuine Pareto-front search (NSGA-II)
  across several objectives at once — e.g. Sharpe ratio, drawdown, and
  eval-pass probability — instead of collapsing everything into one
  score and losing the trade-offs.
- **Evolution Lab** — a full, unattended genetic-algorithm research loop:
  generate → filter → validate → keep winners → mutate, for as long as
  you leave it running. Candidates are ranked by a composite **Prop
  Fitness** score (pass probability × payout probability × robustness ×
  out-of-sample consistency — penalized for thin sample sizes,
  overfitting signals, and concentration risk, not raw net profit).
  Every candidate's backtest runs under your real daily-loss and
  drawdown circuit breakers, so an account-blowing candidate gets
  stopped inside its own evaluation rather than only being caught
  afterward. Checkpoints after every generation — stop and resume a run
  exactly where it left off.

## Validate

Five statistical-rigor tools that each answer a different "how much
should I actually trust this backtest?" question:

- **Walk-Forward Optimization** — rolling or anchored folds, a fresh
  optimization per fold, chained into one continuous out-of-sample
  equity curve.
- **Walk-Forward-Aware GA** — the same genetic search, but scored *only*
  on chained out-of-sample data so it can't just curve-fit harder — and
  it reports the overfitting gap explicitly.
- **CPCV / PBO** — Combinatorial Purged Cross-Validation stress-tests a
  single strategy across many train/test partitions; Probability of
  Backtest Overfitting checks a whole *pool* of candidates for whether
  the apparent best one is genuinely better than chance out-of-sample.
- **Parameter Sensitivity** — sweeps every tunable parameter individually
  with automatic cliff detection, plus an optional 2D heatmap for
  parameter interactions.
- **Regime Survival Matrix** — classifies every bar into a market regime
  (trend, volatility, session, environment) and attributes your
  strategy's actual trades to whichever regime was active — so you can
  see exactly where its losses concentrate.

## Champion

- **Multi-Asset Portfolio** — runs a strategy across several instruments,
  computes their correlation, re-weights risk accordingly, and merges the
  legs into one shared account curve.
- **Multi-Strategy Ensemble** — combines several weakly-correlated
  strategies on the same instrument via blending or voting logic.
- **Family Diversity** — reports per-family performance from a Search Lab
  run, so you can confirm a leaderboard is genuinely diverse rather than
  three variations of the same idea.
- **Automated Portfolio Composer** — searches your entire strategy
  library for the best-performing N-strategy combination automatically.

Cost-stress-adjusted fitness (re-backtesting every candidate at inflated
spread/slippage/commission) and a declarative adaptive-risk layer
(de-risk after a losing streak, cut size on a bad day, coast near a
profit target) apply across every optimizer in the platform.

## Deployment

- **Forward Test (MT5 demo)** — deploys any strategy from your library to
  a free MT5 demo account and watches it trade forward against real
  broker prices, using the exact same signal and sizing engine as the
  backtester. Journals every trade, flags win-rate drift, and ships with
  a kill switch. Demo accounts only.
- **Overnight Autopilot** — chains Speed Run discovery straight into a
  live demo forward test of the winning strategy, so a search that ran
  overnight has a candidate already live on your demo account by morning
  instead of needing to be found, loaded, and started by hand.
- **Auto-Retune** — automatically checks a running forward test against
  its predicted performance band; if realized results have drifted
  outside it, re-runs optimization and shows you a clear before/after.
- **Deploy Live** — connection and credential management for a real,
  funded prop-firm account (live order placement is intentionally staged
  behind additional safeguards).
- **Live Market Monitor** — a read-only view of live bars and trades over
  your connected broker feed.

## Quant Lab

A dozen standalone analysis tools bundled in: a Universal Strategy
Translator (turn a Manual Builder config into clean PineScript v5 or
MQL5), an Auto Regime Selector, a Strategy Health / Drift Monitor, the
Automated Portfolio Composer, a Pairs Screener & Backtester, an Options
Pricing Calculator, an Order Book Simulator, Sentiment-Price Correlation
analysis, a Markowitz Portfolio Optimizer, a Volatility Surface tool, and
a Factor Model.

## Options Outlook & AI Assistant

**Options Outlook** generates deterministic call/put candidates via
Black-Scholes pricing, with an optional AI-ranked narrative layer on top.
The **AI Assistant** dashboard combines a live news panel, a best-markets
scanner, and chat — reading live bars from your connected broker feed.

## Optional local AI assist

Several tools can optionally call a locally-run AI model — Full
Pipeline's search, the Research Agent, AI-assisted strategy generation,
and the Options Outlook / AI Assistant narrative layer. Every
AI-suggested value still passes through the exact same backtest →
prop-sim → Monte Carlo pipeline as anything else in the app: the model
proposes numbers for already-discovered tunable parameters, it never
writes strategy logic, and it can never override a genuinely better
candidate the search already found on its own. Off by default; an
unreachable AI model degrades quietly rather than breaking a feature.

## Runs everywhere

- **Windows desktop app** — full native experience, no Python required.
- **Local Python app** — the same engine on macOS/Linux/Windows.
- **Mobile-friendly web app** — check a search, an Evolution Lab run, or
  a report from your phone, with near-total feature parity to desktop.

---

<div align="center">

**[Get access on Whop →](https://whop.com/t58-trading/t58-backtesting-engine/)**

</div>
