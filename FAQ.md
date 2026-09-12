<div align="center">
<img src="assets/logo/t58-logo-horizontal-dark.png" alt="T58 Trading" width="280" />
</div>

# Frequently Asked Questions

### What exactly am I buying?

Access to the T58 Quant Algo Backtester application — a strategy import,
optimization, and validation platform — through the official Whop
listing. You get the working software (desktop app, local Python app,
and mobile-friendly web app, sharing one engine), not this documentation
repo, which is informational only.

### Is this a signal service or an auto-trading bot?

No. T58 is a research and validation tool. It helps you build, test, and
statistically stress-test a trading strategy — it does not hand you
trade signals to follow, and live order placement to a real funded
account is intentionally locked behind additional safeguards rather than
offered as a one-click feature.

### Do I need to know how to code?

No. The Manual Builder is a full no-code visual strategy builder covering
common indicators and market-structure concepts. If you do have code
already, the platform also accepts Python, PineScript (a tested subset of
v5), and MQL5 (a tested subset).

### Does this guarantee I'll pass a prop-firm evaluation?

No tool can guarantee that, and any tool that claims otherwise should be
treated with skepticism. What T58 gives you is an honest, statistically
grounded *probability estimate* — built from Monte Carlo simulation,
walk-forward validation, and out-of-sample checks — instead of a single
optimistic backtest curve. It reduces the chance you're fooled by an
overfit result; it can't remove the inherent uncertainty of live markets.

### What prop firms are supported?

Built-in quick-fill presets are included for several major prop firms
(rules like account size, profit target, daily loss limit, drawdown type,
consistency requirements, and payout thresholds). Presets are dated with
a reminder to re-verify current terms, since firms change their rules
over time. Any firm's rules can also be entered manually if a preset
isn't available.

### What platforms does the app run on?

- A **Windows desktop app** (no Python required)
- A **local Python app** (Windows, macOS, or Linux)
- A **mobile-friendly web app** for checking runs and reports from a
  phone

All three share the same underlying engine, so results are consistent
across them.

### Do I get the source code?

No. The application is closed-source and proprietary. This public
repository exists to document what the product does and how it's been
tested — not to distribute its implementation.

### What data do I need to bring?

Your own historical price data (CSV/TSV/Parquet, or common compressed
formats) for the instrument(s) you want to test. A sample dataset ships
with the app so you can try the full workflow immediately, and broader
instrument data is bundled as well. Live data fetch is also available for
accounts connected to a supported brokerage feed.

### What's the AI Assist feature, exactly?

An optional integration with a locally-run AI model that can draft
strategy ideas, help investigate a strategy's own validated results, or
propose numeric values for parameters a search has already discovered.
It never writes strategy logic itself and never overrides a genuinely
better result the search already found — every suggestion still passes
through the same backtest → prop-sim → Monte Carlo pipeline as anything
else. It's off by default.

### What if I want to cancel?

Billing, trial length, and cancellation are all handled directly through
Whop — see the listing for current terms.

### How do I get support?

See **[SUPPORT.md](SUPPORT.md)** for how to reach us once you're a
customer.

---

<div align="center">

**[Still have questions? Start with the free trial →](https://whop.com/t58-trading/t58-backtesting-engine/)**

</div>
