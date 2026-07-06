# Pro Confluence Engine

> All-in-one Smart Money Concepts signal system for TradingView — six weighted evidence components, an adaptive volatility-regime engine, honest hypothetical stats, and webhook-ready alerts. **Invite-only.**

---

## What it is

The Pro Confluence Engine (PCE) is the paid flagship of [SMC Pine Suite](../README.md). It combines the concept areas of the suite's four free indicators into a single weighted **0–100 confluence score** per direction, and fires discrete, non-repainting entry signals only when multiple independent pieces of evidence line up:

| # | Component | Evidence | Default weight |
|---|-----------|----------|:--:|
| 1 | **Structure** | BoS/CHoCH trend state + break recency | 25 |
| 2 | **Zones** | Price retesting an armed, unmitigated Order Block or unfilled FVG | 20 |
| 3 | **Liquidity** | Recency of a stop-hunt sweep through equal highs/lows | 15 |
| 4 | **Volume** | Direction-gated relative volume + rolling POC location | 15 |
| 5 | **HTF bias** | Higher-timeframe EMA-stack alignment (non-repainting) | 15 |
| 6 | **Divergence** | Regular RSI divergence at confirmed pivots | 10 |

Weights are user-tunable and auto-normalized — set any component to 0 to disable it. See [FEATURES.md](FEATURES.md) for the full breakdown.

## Highlights

- **Adaptive regime engine** — ATR-percentile classification (LOW / NORMAL / HIGH volatility) automatically adjusts the signal threshold, stop width, and cooldown.
- **Strictly non-repainting** — every state change, signal, and alert is finalized at bar close; higher-timeframe data uses the confirmed-bar `request.security` idiom (one HTF bar of lag, by design).
- **Honest hypothetical tracker** — every signal's SL/TP outcome is tracked and displayed as W/L/Ambiguous/Expired. Ambiguous bars (SL and TP touched in the same bar) are counted as **losses**, never wins. No survivorship filtering. Not a performance claim.
- **Risk module** — structural stop (last swing ± buffer) with a regime-scaled ATR floor, R:R-derived take-profit, optional position-size hint.
- **Preset modes** — Scalp / Intraday / Swing / Custom remap the core knobs; an asset-class selector calibrates volume thresholds for Crypto / Forex / Metals.
- **Alerts** — seven `alertcondition` events plus a dynamic JSON `alert()` payload (symbol, timeframe, direction, score, entry, SL, TP, regime) for webhook automation.
- **Dashboard** — component-by-component score breakdown, regime state, HTF bias, last signal, and rolling hypothetical stats.

## Access

- Published on TradingView as an **invite-only script** — the source code is never distributed and is **not** in this repository (see [LICENSE-PRO](../LICENSE-PRO)).
- For access, see [PRICING.md](PRICING.md) or contact [@btankutt](https://github.com/btankutt).

## Requirements

- A TradingView account (invite-only scripts require at least a free account; webhook alerts require a paid TradingView plan).
- Works on any symbol and timeframe; volume-based components degrade gracefully on tickers without volume data.

## Disclaimer

The Pro Confluence Engine is an **educational tool, not financial advice**. Past performance does not guarantee future results. The built-in outcome tracker reports **hypothetical**, close-based results that ignore fees, spread, slippage, and intrabar order. Always backtest, forward-test in a demo account, and use proper risk management.
