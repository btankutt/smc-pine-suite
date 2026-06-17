# Changelog — Pro Confluence Engine

All notable changes to the Pro Confluence Engine are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

### Planned
- Backtest report with statistical evidence across crypto, forex, and metals
- Additional weight presets and an auto-tuning option
- Optional session/volatility filters to suppress signals in low-quality conditions

---

## [1.0.0] — 2026-06-17

### Added
- Initial release of the Pro Confluence Engine (Pine Script v6, invite-only).
- Six scoring modules: market structure, order blocks, fair value gaps, liquidity sweeps, volume profile, and MTF momentum divergence.
- Adaptive scoring: configurable per-module weights, normalized [−100, +100] score, and higher-timeframe trend-alignment scaling (boost/dampen).
- Threshold-crossing LONG/SHORT signals with on-chart labels.
- Live confluence dashboard showing each module's vote, HTF bias, and the final score.
- Three alert conditions: long signal, short signal, and any signal.
- Public documentation: [README](README.md), [FEATURES](FEATURES.md), [PRICING](PRICING.md).

---

[Unreleased]: https://github.com/btankutt/smc-pine-suite
[1.0.0]: https://github.com/btankutt/smc-pine-suite
