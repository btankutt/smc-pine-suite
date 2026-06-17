# Pro Confluence Engine 💎

> Invite-only, all-in-one Smart Money Concepts signal engine. Combines the four free SMC Pine Suite indicators into a single adaptive confluence score.

> **Proprietary — source not distributed.** This directory documents the Pro Confluence Engine. The source code is delivered exclusively through TradingView's invite-only system and is **not** published in this repository. See [LICENSE-PRO](../LICENSE-PRO).

---

## What It Does

The Pro Confluence Engine fuses every signal from the free suite into one decision layer. Instead of eyeballing four indicators and guessing whether they agree, you get a single normalized **confluence score** from −100 (strong bearish) to +100 (strong bullish), plus discrete long/short signals when conviction crosses a threshold.

The principle from the suite's [trading philosophy](../docs/trading-philosophy.md) is enforced mechanically: **no single indicator decides; convergence does.**

---

## The Six Modules

Each module casts a directional vote (bullish / neutral / bearish). Votes are weighted and combined.

| # | Module | Source | What the vote means |
|---|--------|--------|---------------------|
| 1 | **Market Structure** | SMC Toolkit | Current BoS/CHoCH trend direction |
| 2 | **Order Blocks** | SMC Toolkit | Price tagging an unmitigated OB |
| 3 | **Fair Value Gaps** | SMC Toolkit | Price entering an unfilled FVG |
| 4 | **Liquidity Sweeps** | SMC Toolkit | A stop-run that reversed back inside |
| 5 | **Volume Profile** | Volume Profile Plus | Premium vs discount relative to value area |
| 6 | **Momentum Divergence** | MTF Divergence Scanner | RSI exhaustion against price |

---

## Adaptive Scoring

What makes the engine "adaptive" rather than a static checklist:

1. **Weighted votes** — every module has a configurable weight, so you can tilt the engine toward the concepts you trust most.
2. **Normalized score** — the weighted sum is divided by the maximum possible weight and scaled to [−100, +100], so the score is comparable across instruments and settings.
3. **Higher-timeframe alignment** — the raw score is multiplied by a trend-alignment factor: **boosted** when it agrees with the higher-timeframe trend, **dampened** when it fights it. This is the layer that keeps the engine from buying dips in a strong downtrend.
4. **Threshold signals** — discrete LONG/SHORT signals fire only when the adaptive score *crosses* the threshold, not every bar it stays beyond it.

---

## Dashboard

A live panel shows each module's current vote, the higher-timeframe bias, and the final confluence score — color-coded so a glance tells you whether the desk is aligned.

---

## What's Included (for invited users)

- `pro-confluence-engine.pine` — the full engine (Pine Script v6)
- Recommended weight presets for crypto, forex, and metals
- A short companion guide mapping scores to trade management
- Priority updates as the scoring model evolves

---

## Access

The Pro Confluence Engine is **invite-only** via TradingView. The source is not part of the public repository.

For access or licensing inquiries, reach out via GitHub: [@btankutt](https://github.com/btankutt).

---

## Relationship to the Free Suite

Everything the Pro engine scores is implemented, open, and auditable in the free indicators:

- [SMC Toolkit](../indicators/01-smc-toolkit) — structure, Order Blocks, FVG, liquidity
- [Volume Profile Plus](../indicators/02-volume-profile-plus) — POC, value area, nodes
- [MTF Divergence Scanner](../indicators/03-mtf-divergence) — RSI/MACD divergence
- [ATR Helper](../indicators/04-atr-helper) — stops, targets, position sizing

The Pro engine's value is the **fusion and adaptive weighting**, not secret signals. You can study the building blocks for free.

---

## Disclaimer

This is an **educational tool**, not financial advice. A high confluence score is not a guarantee — it is a structured way to measure agreement among independent signals. Always backtest, forward-test in a demo account, and use the [ATR Helper](../indicators/04-atr-helper) (or equivalent) for position sizing and stops. Trading involves risk. Past performance does not guarantee future results.

---

## Author

**Barış Tankut** ([@btankutt](https://github.com/btankutt))
Algorithmic Trading Systems & IoT Embedded Engineer

Part of [SMC Pine Suite](../README.md) — production-grade Pine Script v6 indicators.
