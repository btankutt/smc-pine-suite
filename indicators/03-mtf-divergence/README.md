# MTF Divergence Scanner

> Multi-timeframe RSI / MACD divergence detector for TradingView — regular and hidden divergences across up to three timeframes in a single Pine Script v6 script.

---

## Overview

A standalone divergence scanner that compares price swings against an oscillator (RSI or MACD histogram) and flags both **regular** (reversal) and **hidden** (continuation) divergences. It evaluates up to three timeframes at once via `request.security`, so you can watch the chart timeframe while higher timeframes are scanned in the background.

Signals are derived from **confirmed oscillator pivots** — a divergence only prints once its pivot is locked (`piv_right` bars after it forms). This confirmation step removes most of the repaint risk that naive MTF divergence scripts suffer from.

This indicator is part of [SMC Pine Suite](../../README.md). Built with Pine Script v6: tuple-returning functions, `request.security` for MTF evaluation, and a `table` for the status panel.

---

## Features

### 1. Two Oscillators

- **RSI** — momentum oscillator; divergences mark exhaustion of a move
- **MACD histogram** — `macd line − signal line`; divergences on the histogram are often earlier than on the line itself

Switch between them in one input; the pivot logic is identical for both.

### 2. Regular vs Hidden Divergence

- **Regular bullish** — price makes a lower low, oscillator makes a higher low → potential reversal up
- **Regular bearish** — price makes a higher high, oscillator makes a lower high → potential reversal down
- **Hidden bullish** — price makes a higher low, oscillator makes a lower low → uptrend pullback (continuation)
- **Hidden bearish** — price makes a lower high, oscillator makes a higher high → downtrend pullback (continuation)

Toggle regular and hidden independently.

### 3. Up to Three Timeframes

Each of the three timeframe slots has an on/off toggle and a timeframe selector. Leave a slot blank to use the chart's own timeframe. Defaults: chart, 60m, 240m.

### 4. On-Chart Labels + Status Table

Detected divergences print labels at the bar (below for bullish, above for bearish), tagged with the type (`Reg`/`Hid`) and the timeframe. A compact table in the top-right corner shows the most recent divergence direction per timeframe.

### 5. Three Alert Conditions

- Bullish divergence (any timeframe)
- Bearish divergence (any timeframe)
- Any divergence (either direction, any timeframe)

---

## Installation

1. Open TradingView and navigate to any chart
2. Open the **Pine Editor** (bottom panel)
3. Copy the contents of [`mtf-divergence.pine`](mtf-divergence.pine)
4. Paste into Pine Editor, click **"Save"**, then **"Add to chart"**

---

## Configuration

### Oscillator
- `Oscillator` (default: RSI) — RSI or MACD
- `RSI length` (default: 14)
- `MACD fast / slow / signal length` (default: 12 / 26 / 9)

### Pivots
- `Pivot left` (default: 5) — bars required to the left of a pivot
- `Pivot right` (default: 5) — bars required to the right; this is the confirmation delay

### Divergence Types
- `Regular divergence (reversal)` (default: true)
- `Hidden divergence (continuation)` (default: false)

### Timeframes
- `Timeframe 1 / 2 / 3` — each with an on/off toggle and a timeframe (blank = chart)

### Display
- `Show on-chart labels`, `Show status table`
- Bullish / bearish colors

---

## Pine Script v6 Implementation Notes

- **Tuple-returning engine** — `calc_div()` returns `[regular_bull, regular_bear, hidden_bull, hidden_bear]` and is evaluated inside each `request.security` call so all pivot math runs in the target timeframe's context
- **Confirmed pivots only** — `ta.pivothigh`/`ta.pivotlow` with a right offset means signals appear after confirmation, not on the forming bar, which suppresses repaint
- **`var` state inside the function** — previous pivot price and oscillator values persist per security context for the swing-to-swing comparison
- **`table` status panel** — a single persistent table is updated on `barstate.islast`

---

## How to Use

1. Set your trading timeframe as the chart and pick two higher timeframes for context.
2. Favour signals where a **lower-timeframe regular divergence aligns with a higher-timeframe trend** — e.g. a regular bullish divergence on the chart while the 4H is in an uptrend.
3. Use **hidden divergence** to add to trend positions on pullbacks rather than to call tops/bottoms.
4. Combine with the [SMC Toolkit](../01-smc-toolkit): a regular divergence into an unmitigated Order Block or a liquidity sweep is a strong confluence entry.

> ⚠️ Divergence is a context tool, not a standalone trigger. A divergence can persist for many bars before price reacts. Always wait for a price-action confirmation and use stops.

---

## Repainting Notes

- Signals are based on **confirmed pivots**, so a printed label will not disappear.
- Higher-timeframe values update as the HTF bar develops; the divergence itself still requires `piv_right` closed HTF bars to confirm, so the flag does not flicker intrabar.
- `lookahead` is disabled (`barmerge.lookahead_off`) — no future data is used.

---

## License

This indicator is open source under the **Mozilla Public License 2.0** (MPL 2.0). See [LICENSE-FREE](../../LICENSE-FREE) for full text.

---

## Disclaimer

This indicator is provided **as is**, without any guarantee of profitability or accuracy. Always backtest on historical data, forward-test in a demo account, and use position sizing and stop-losses appropriate to your account. Trading involves risk. Past performance does not guarantee future results.

---

## Author

**Barış Tankut** ([@btankutt](https://github.com/btankutt))
Algorithmic Trading Systems & IoT Embedded Engineer

Part of [SMC Pine Suite](../../README.md) — production-grade Pine Script v6 indicators.
