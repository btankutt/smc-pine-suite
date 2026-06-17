# Pro Confluence Engine — Features

> A detailed breakdown of what the invite-only Pro Confluence Engine does. Source is not published (see [LICENSE-PRO](../LICENSE-PRO)); this document describes the capabilities.

---

## At a glance

The Pro Confluence Engine fuses all four free SMC Pine Suite indicators into a single adaptive **confluence score** from −100 (strong bearish) to +100 (strong bullish), and emits discrete long/short signals when conviction crosses a threshold.

---

## Six scoring modules

| Module | Source concept | Vote |
|--------|----------------|------|
| **Market Structure** | SMC Toolkit | Current BoS/CHoCH trend direction |
| **Order Blocks** | SMC Toolkit | Price tagging an unmitigated OB |
| **Fair Value Gaps** | SMC Toolkit | Price entering an unfilled FVG |
| **Liquidity Sweeps** | SMC Toolkit | A stop-run that reversed back inside |
| **Volume Profile** | Volume Profile Plus | Premium vs discount relative to value |
| **Momentum Divergence** | MTF Divergence Scanner | RSI exhaustion against price |

Each module casts a bullish / neutral / bearish vote. Votes are weighted, summed, and normalized.

---

## The adaptive layer

What makes the engine *adaptive* rather than a static checklist:

1. **Configurable weights** — every module has its own weight, so the engine can be tilted toward the concepts you trust most (e.g. structure-heavy for trend traders, volume-heavy for range traders).
2. **Normalized score** — the weighted sum is divided by the maximum possible weight and scaled to [−100, +100], making the score comparable across instruments, timeframes, and weight presets.
3. **Higher-timeframe alignment** — the raw score is multiplied by a trend-alignment factor: **boosted** when it agrees with the higher-timeframe trend, **dampened** when it fights it. This is the layer that stops the engine from buying dips in a strong downtrend.
4. **Threshold-crossing signals** — discrete LONG/SHORT signals fire only when the adaptive score *crosses* the threshold, not on every bar it stays beyond it, which avoids signal spam.

---

## Live dashboard

A compact on-chart panel shows, updated each bar:

- Each module's current vote (bullish / neutral / bearish), colour-coded
- The higher-timeframe bias
- The final confluence score, highlighted when a signal threshold is met

A glance tells you whether the desk is aligned or conflicted.

---

## Signals & alerts

- **On-chart labels** — "LONG" / "SHORT" with the score at the signal bar
- **Score plot** — available in the data window for logging or further study
- **Alerts** — long-signal, short-signal, and a combined condition for automation or notifications

---

## What invited users receive

- `pro-confluence-engine.pine` — the full engine (Pine Script v6)
- Recommended weight presets for crypto, forex, and metals
- A short companion guide mapping score ranges to trade management
- Priority updates as the scoring model evolves (see [CHANGELOG](CHANGELOG.md))

---

## Design principles

- **Auditable foundations** — every concept the engine scores is implemented openly in the [free indicators](../indicators). The Pro value is the *fusion and adaptive weighting*, not secret signals.
- **No repainting of confirmed events** — structure, OB, FVG, and divergence votes are based on confirmed pivots and bar closes.
- **Bounded performance** — drawing and computation are capped so the engine stays responsive on long histories.

---

## Access

Invite-only via TradingView. See [PRICING](PRICING.md) for the access model, or [README](README.md) for the overview. Request access via GitHub: [@btankutt](https://github.com/btankutt).

---

## Disclaimer

This is an educational tool, not financial advice. A high confluence score measures agreement among independent signals — it is not a guarantee. Always backtest, forward-test, and manage risk with the [ATR Helper](../indicators/04-atr-helper) or equivalent.
