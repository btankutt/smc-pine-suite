# Pro Confluence Engine — Changelog

## Unreleased — Planned

- Backtest report with statistical evidence across crypto, forex, and metals
- Additional weight presets and an auto-tuning option
- Session/volatility filter refinements

## v1.0.0 (2026-07-06)

Initial release.

- Six-component weighted confluence scoring (Structure / Zones / Liquidity / Volume / HTF bias / RSI divergence), 0–100 per direction, weight-normalized.
- Adaptive volatility-regime engine (ATR percentile → LOW/NORMAL/HIGH) driving threshold, stop width, and cooldown.
- Event-triggered, non-repainting signal engine with dominance gap, min-components-in-agreement, cooldown, optional session window and HTF hard filter.
- Zone arming rule prevents the creating impulse from double-counting with the structure break.
- Risk module: structural SL with regime-scaled ATR floor, R:R take-profit, entry/SL/TP lines, position-size hint.
- Honest hypothetical outcome tracker (W/L/Ambiguous-as-loss/Expired, rolling 100).
- Dashboard with component breakdown, regime, HTF bias, last signal, and stats.
- Seven alertconditions + dynamic JSON webhook payload.
- Preset modes (Scalp/Intraday/Swing/Custom) and asset-class volume calibration.
