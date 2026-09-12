<div align="center">
<img src="assets/logo/t58-logo-horizontal-dark.png" alt="T58 Trading" width="280" />
</div>

# Proof & Testing Rigor

Anyone can put "backtested and validated" on a landing page. This page
exists so you don't have to take that on faith — here's what actually
stands behind it, and what specifically has been tested.

**Note:** this document describes the *testing methodology and history*.
It intentionally does not include source code, internal algorithms, or
proprietary implementation details — those are part of the closed-source
application available on Whop.

---

## The regression suite

The application ships with an internal automated test suite that has
grown from roughly 50 tests to **1,000+ tests** over the course of
development, covering the backtest engine, prop-firm simulator, Monte
Carlo engine, genetic-algorithm search and evolution loops, walk-forward
and CPCV validation, strategy import parsers (Python / PineScript /
MQL5), report generation, and the desktop/web UIs. Every release is
required to pass the full suite before it ships.

This isn't a marketing number — it reflects an actual engineering
practice: every non-trivial bug found during development gets a
regression test written *for that specific bug* before the fix is
considered done, so the same failure mode can't silently come back in a
later version.

## What's actually been stress-tested (and fixed)

Quant backtesters fail in specific, well-known ways. Here is a genuine,
non-exhaustive list of failure classes that have been found and fixed
during this platform's development — through independent re-verification
of its own results, not just "it looked profitable so we shipped it":

- **Lookahead bias / leakage** — signal generation being caught using
  information that wouldn't have been available at the time of the
  trade. This is now checked automatically for every strategy via a
  truncated-data re-run that flags the exact bar a leak first appears on.
- **Instrument scale / pip-size mismatches** — a notoriously easy trap on
  instruments like gold or indices, where a wrong pip-size assumption can
  silently inflate or deflate every P&L number in a backtest.
- **Position-sizing errors** — including cases where a small edge case
  produced dramatically oversized real-money-equivalent risk per trade.
- **Genetic-algorithm bounds bugs** — a GA that can technically wander
  outside a parameter's sane bounds will happily "discover" a strategy
  that only looks good because of an invalid configuration.
- **In-sample vs. out-of-sample gaps** — probability estimates computed
  against the same data a search optimized on will always look better
  than they perform live. The platform's optimizers are built to
  surface an honest, held-out validation estimate *alongside* the raw
  in-sample number, specifically so the two can be compared rather than
  the optimistic one shown alone.
- **Search diversity collapse** — an unattended search/evolution process
  can quietly converge onto the same 2-3 strategy shapes if nothing
  actively protects diversity across long runs; the platform enforces a
  minimum floor of active strategy families for exactly this reason.
- **Worker/thread stalls in long-running searches** — Search Lab and
  Evolution Lab runs are unattended for potentially hours; the platform
  includes stall-detection and automatic recovery so a hung worker
  doesn't silently kill an overnight run.

Each of the above corresponds to a real fix with a real regression test
attached, not a hypothetical risk being described defensively.

## Validation methodology, not just "it backtested well"

The platform doesn't rely on a single historical curve to call a
strategy good. Every "validated" strategy has been run through multiple,
independent statistical checks designed specifically to catch overfitting
and curve-fitting:

- **Monte Carlo simulation** across thousands of resampled account paths
  — a *distribution* of outcomes, not one lucky curve.
- **Walk-forward validation**, including a walk-forward-*aware* genetic
  search that is scored only on chained out-of-sample data, so the
  search itself can't just curve-fit harder to beat the metric.
- **Combinatorial Purged Cross-Validation (CPCV)** and **Probability of
  Backtest Overfitting (PBO)** — proper quant-research techniques for
  testing whether an apparent "best" strategy is actually better than
  chance, not just the winner of a lucky data split.
- **Cost-stress testing** — every strategy is also evaluated under
  inflated spread, slippage, and commission assumptions, to check whether
  its edge survives worse-than-expected execution conditions.
- **Regime attribution** — every trade a strategy makes is mapped back to
  the market regime it happened in, to surface exactly where losses
  concentrate rather than hiding them in an aggregate number.

## What a report actually shows you

Every run produces one self-contained report (HTML, print-to-PDF
friendly) that includes: the historical backtest, the prop-firm
simulation result under your exact rule set, the Monte Carlo probability
distribution, a plain-language pass/funded/payout probability funnel,
and — for optimized strategies — both the in-sample and held-out
out-of-sample estimates side by side, so you can see the gap between them
yourself rather than being handed one number to trust.

## Full disclaimer

Simulated results are estimates derived from historical data and
statistical resampling. A rigorous testing process reduces the risk of
*obviously broken* results — it does not, and cannot, guarantee future
performance. No backtester, however well-tested, can eliminate the
fundamental uncertainty of live markets. Past performance and simulated
outcomes do not guarantee future results.

---

<div align="center">

**[See it for yourself — start a free trial →](https://whop.com/t58-trading/t58-backtesting-engine/)**

</div>
