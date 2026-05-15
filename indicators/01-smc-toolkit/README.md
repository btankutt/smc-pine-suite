# SMC Toolkit

> Smart Money Concepts indicator for TradingView — Order Blocks, Fair Value Gaps, Liquidity Sweeps, and Market Structure (BoS/CHoCH) in a single Pine Script v6 script.

🇹🇷 [Türkçe README](README.tr.md)

---

## Overview

A standalone SMC indicator implementing standard, public-domain concepts used by smart-money price-action traders:

- **Market structure** detection (Break of Structure & Change of Character)
- **Order Blocks** identified at structural breaks with optional volume filtering
- **Fair Value Gaps** with ATR-scaled minimum size filter
- **Liquidity** levels (equal highs/lows) with sweep detection

Each component runs independently — you can toggle features on/off via inputs. Mitigated Order Blocks and filled FVGs are automatically recolored gray so the chart stays uncluttered.

This indicator is part of [SMC Pine Suite](../../README.md). Built with Pine Script v6 features: user-defined types, methods (dot notation), and time-based xloc for zoom-stable drawings.

---

## Features

### 1. Market Structure (BoS / CHoCH)

Tracks swing highs and lows via configurable pivot length. When price closes beyond the most recent swing:

- **BoS (Break of Structure)** — price continues in the current trend direction
- **CHoCH (Change of Character)** — price breaks against the trend, signaling potential reversal

Labels appear at break points with directional styling (green/red).

### 2. Order Blocks

When a BoS occurs, the indicator scans backward for the last opposite-color candle — this becomes the Order Block. Optional volume filter excludes weak-volume candles (compared against 20-period volume SMA).

- Bullish OBs (formed before upside breaks) drawn in green
- Bearish OBs (formed before downside breaks) drawn in red
- Maximum displayed count is configurable (default: 5 per direction)
- OBs touched by price are marked as mitigated and recolored gray

### 3. Fair Value Gaps

Detects 3-candle gap patterns:

- **Bullish FVG** — current low above the high two bars back
- **Bearish FVG** — current high below the low two bars back

Filtered by minimum size (ATR multiplier) to skip noise-level gaps. Filled FVGs (price returns into the gap) are marked and recolored.

### 4. Liquidity Levels

Tracks equal-highs and equal-lows within an ATR-scaled tolerance, forming liquidity pools:

- **Buy-side liquidity (BSL)** — equal highs above price (short stops cluster here)
- **Sell-side liquidity (SSL)** — equal lows below price (long stops cluster here)

A sweep occurs when price wicks beyond a level then closes back inside. Sweep labels mark the event.

### 5. Six Alert Conditions

Each major event triggers a separate alert:

- BoS Bullish / BoS Bearish
- CHoCH Bullish / CHoCH Bearish
- BSL Swept / SSL Swept

Configure alerts via TradingView's "Create Alert" dialog after adding the indicator to your chart.

---

## Installation

1. Open TradingView and navigate to any chart
2. Open the **Pine Editor** (bottom panel)
3. Copy the contents of [`smc-toolkit.pine`](smc-toolkit.pine)
4. Paste into Pine Editor and click **"Save"** (give it a name)
5. Click **"Add to chart"**

The indicator will compile and overlay on your chart immediately.

---

## Configuration

All inputs are grouped in the indicator settings dialog:

### Structure
- `Swing detection length` (default: 5) — Pivot left/right length. Lower values = more sensitive, but noisier.
- `Show internal structure` (default: false) — Reserved for future use
- `Show external structure` (default: true) — Toggle BoS/CHoCH labels

### Order Blocks
- `Enable Order Blocks` (default: true)
- `Max OBs to display` (default: 5) — Older OBs auto-removed when limit reached
- `Filter by volume` (default: true) — Only OBs with above-average volume kept
- `Bullish/Bearish OB color` — Customize colors and transparency

### Fair Value Gaps
- `Enable FVG` (default: true)
- `Max FVGs to display` (default: 5)
- `Min FVG size (ATR multiplier)` (default: 0.5) — Lower to see more FVGs, higher to filter noise
- `Bullish/Bearish FVG color` — Customize

### Liquidity
- `Enable Liquidity` (default: true)
- `Equal highs/lows lookback` (default: 50) — Historical bars to scan
- `Tolerance (ATR multiplier)` (default: 0.2) — How close must highs/lows be to count as equal

### Display
- `Show event labels` (default: true) — Toggle BoS, CHoCH, sweep labels
- `Box transparency` (default: 70) — Box fill transparency

---

## Screenshots

### BoS / CHoCH Detection
![BTC Daily — BoS detection example](screenshots/btc-1d-bos-example.png)

The indicator marks structural breaks with clear directional labels.

### Order Block + Liquidity
![BTC 4H — Order Block with liquidity context](screenshots/btc-4h-bos-example.png)

Order Blocks appear at structural break origins, with liquidity levels showing equal-high pools.

---

## Pine Script v6 Implementation Notes

This indicator uses several Pine Script v6 features that improve over v5:

- **User-defined types** — `OrderBlock`, `FVG`, `LiquidityLevel` structs keep logical state organized
- **Method syntax (dot notation)** — `arr.push()`, `box.delete()`, `ref.set_bgcolor()` for cleaner code
- **Time-based xloc** — Drawings remain anchored when zooming (uses `xloc.bar_time` instead of bar indices)
- **Strict boolean typing** — `trend_initialized` flag pattern avoids Pine v6's bool-cannot-be-na rule
- **Magic numbers in constants** — All thresholds named: `ATR_LENGTH`, `VOLUME_SMA_LENGTH`, `OB_LOOKBACK_BARS`, `PIVOT_BUFFER_SIZE`

If you're migrating from Pine v5, see [TradingView's official migration guide](https://www.tradingview.com/pine-script-docs/migration-guides/to-pine-version-6/).

---

## How to Use

### Conservative trading setup

1. Wait for **CHoCH** in your higher timeframe (e.g., 4H or daily)
2. Drop to lower timeframe (e.g., 15M or 1H)
3. Wait for price to retrace into an **unmitigated Order Block** or **unfilled FVG**
4. Look for **liquidity sweep** at structural support/resistance for confirmation
5. Enter with stop-loss beyond the OB/FVG, target the next liquidity pool

### Aggressive setup

1. After **BoS** (continuation signal), enter on the first retracement
2. Use the most recent OB as your invalidation level
3. Manage risk based on R:R ratio

> ⚠️ This is an educational tool. Always backtest your strategy and use proper position sizing.

---

## Pivot Confirmation Delay

The indicator uses `ta.pivothigh(swing_length, swing_length)` which requires `swing_length` bars to confirm a pivot. This means:

- Structural breaks are detected `swing_length` bars **after** they form
- This eliminates lookahead bias but introduces a small delay
- Adjust `swing_length` to balance responsiveness vs reliability

Default `swing_length = 5` works well on 1H and higher timeframes. For 15M or lower, consider reducing to 3.

---

## Performance

- **Compile time:** ~1-2 seconds on most charts
- **Memory:** Bounded by `max_boxes_count=500`, `max_lines_count=500`, `max_labels_count=500`
- **Repainting:** None. Pivot-based detection waits for confirmation, drawings use time-based coordinates.

---

## License

This indicator is open source under the **Mozilla Public License 2.0** (MPL 2.0). See [LICENSE-FREE](../../LICENSE-FREE) for full text.

You may use, modify, fork, and adapt this code for your own strategies. If you redistribute modifications, attribution and same-license terms apply per MPL 2.0.

---

## Disclaimer

This indicator is provided **as is**, without any guarantee of profitability or accuracy. Smart Money Concepts are interpretive — different traders apply them differently. Always:

- Backtest your strategy thoroughly on historical data
- Forward-test in a demo account before live trading
- Use position sizing and stop-losses appropriate to your account
- Remember that no indicator removes the need for trader judgment

Trading involves risk. Past performance does not guarantee future results.

---

## Author

**Barış Tankut** ([@btankutt](https://github.com/btankutt))
Algorithmic Trading Systems & IoT Embedded Engineer

Part of [SMC Pine Suite](../../README.md) — production-grade Pine Script v6 indicators.
