<div align="center">
<img src="assets/logo/t58-logo-horizontal-dark.png" alt="T58 Trading" width="280" />
</div>

# Recent Milestones

T58 is under active development. This page tracks major, customer-facing
milestones at a high level — not a line-by-line internal changelog.
Exact release notes and version numbers are shared with active customers
through the official support channel.

> **Template notice:** the entries below describe the general shape of
> recent development and should be refreshed with specific, current
> milestones as they ship. Keep entries customer-facing (what changed for
> you) rather than internal (what file changed).

---

### Held-out validation surfaced everywhere it matters

Every optimizer that searches for a strategy now shows an honest,
held-out out-of-sample estimate directly alongside its raw in-sample
result — instead of the optimistic number being the only one you see.
Promoting a "champion" strategy now includes a real confirmation step
when the gap between the two is large.

### Evolution Lab diversity floor

Long-running Evolution Lab searches now enforce a minimum floor of active
strategy families, preventing an unattended run from quietly converging
onto the same 2-3 strategy shapes over time.

### Stall detection & recovery for long unattended runs

Search Lab and Full Pipeline batch runs now detect a genuinely hung
worker and automatically recover, rather than requiring a manual restart
of an overnight search.

### Pip-size detection on both desktop and web

A "detect pip size from data" helper — previously desktop-only — is now
available on the web app as well, closing a gap that could otherwise
introduce scaling errors on instruments like gold or indices.

### Guided walkthroughs across every advanced lab

Step-by-step in-app guidance was extended to the Evolution Lab, Search
Lab, and Full Pipeline tabs on desktop, matching what was already
available on web.

---

## Looking ahead

Ongoing development continues to focus on three things: tightening the
statistical rigor of the validation tools (CPCV/PBO, walk-forward-aware
search), hardening the unattended search and evolution engines against
edge cases, and closing any remaining feature gaps between desktop, local
Python, and web.

**[See the full feature set →](FEATURES.md)**
