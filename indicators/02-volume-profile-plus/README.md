# Volume Profile Plus

> Session-based Volume Profile for TradingView — POC, Value Area (VAH/VAL), and HVN/LVN nodes in a single Pine Script v6 script.

---

## Overview

A standalone Volume Profile indicator that renders a horizontal volume histogram and the classic market-profile reference levels:

- **Point of Control (POC)** — the single price level that traded the most volume
- **Value Area High / Low (VAH / VAL)** — the price band containing a configurable share (default 70%) of total volume, expanded outward from the POC
- **High / Low Volume Nodes (HVN / LVN)** — price levels of unusually heavy or light participation, color-highlighted

The profile can be anchored to a higher-timeframe **session** (e.g. daily, weekly) or computed over a **fixed lookback** window. Each bar's volume is distributed evenly across every price row its high–low range spans, which approximates a true tick-volume profile from standard OHLCV data.

This indicator is part of [SMC Pine Suite](../../README.md). Built with Pine Script v6: arrays for the volume bins, methods (dot notation) for drawing handles, and `barstate.islast` recomputation for bounded loop cost.

---

## Features

### 1. Session or Fixed-Lookback Range

- **Session** mode anchors the profile to a higher timeframe via `input.timeframe`. A new profile begins each time the anchor period rolls over (new day, new week, etc.).
- **Fixed lookback** mode profiles a constant number of bars regardless of session, useful for continuous markets like crypto.

### 2. Point of Control

The row with the highest accumulated volume. Drawn as a solid horizontal line and labelled with its price. POC is the market's fairest-value reference and frequently acts as support/resistance on revisits.

### 3. Value Area (VAH / VAL)

Starting at the POC, the algorithm repeatedly absorbs the heavier of the two adjacent rows until the configured percentage of total volume is captured. The top and bottom of that band become VAH and VAL, optionally shaded.

### 4. Volume Nodes (HVN / LVN)

- **HVN** — rows at or above the HVN threshold (default 80% of POC volume). Price tends to consolidate around these.
- **LVN** — rows at or below the LVN threshold (default 20% of POC volume). Price tends to move quickly through these "gaps".

### 5. Alert

A single alert condition fires when price crosses the most recent POC.

---

## Installation

1. Open TradingView and navigate to any chart
2. Open the **Pine Editor** (bottom panel)
3. Copy the contents of [`volume-profile-plus.pine`](volume-profile-plus.pine)
4. Paste into Pine Editor, click **"Save"**, then **"Add to chart"**

---

## Configuration

### Calculation
- `Profile range` (default: Session) — Session vs Fixed lookback
- `Session anchor timeframe` (default: D) — Higher timeframe that defines one session
- `Fixed lookback (bars)` (default: 200) — Window size when using Fixed lookback
- `Number of rows` (default: 50) — Price resolution; higher = finer but slower
- `Value Area (%)` (default: 70) — Share of volume captured by the value area

### Volume Nodes
- `Highlight HVN / LVN` (default: true)
- `HVN threshold (% of POC volume)` (default: 80)
- `LVN threshold (% of POC volume)` (default: 20)

### Display
- `Profile width (bars)` (default: 80) — Maximum histogram bar length
- `Show POC line`, `Show Value Area`, `Shade Value Area`, `Show price labels`
- Colors for profile body, value area, HVN, LVN, and POC

---

## Pine Script v6 Implementation Notes

- **Array-backed bins** — `array<float>` holds per-row volume; the value-area walk and POC search are simple array scans
- **Volume distribution** — each bar's volume is split evenly across the rows between its low and high, not just assigned to its close
- **`barstate.islast` recompute** — the profile is rebuilt once per realtime update rather than on every historical bar, keeping the nested loops cheap
- **Handle arrays + `clear_drawings()`** — boxes, lines, and labels are tracked and deleted before each redraw, so profiles never stack

---

## How to Use

1. Identify the **POC** as the session's fair value. Mean-reversion setups target the POC; trend setups expect rejection from it.
2. Treat **VAH/VAL** as the edges of acceptance. A close back inside the value area after probing outside is a classic fade signal; acceptance outside signals continuation.
3. Expect price to **stall at HVNs** and **travel fast through LVNs** — useful for placing targets and anticipating gaps.
4. Combine with the [SMC Toolkit](../01-smc-toolkit) — an Order Block or FVG that aligns with a POC or value-area edge is a higher-confluence zone.

> ⚠️ This is an educational tool. Always backtest your strategy and use proper position sizing.

---

## Performance

- **Compile time:** ~1-2 seconds on most charts
- **Memory:** Bounded by `max_boxes_count=500`, `max_lines_count=500`, `max_labels_count=500`
- **Repainting:** The live session's profile updates as new volume arrives (expected for any session profile). Closed sessions and fixed-lookback ranges are stable once formed.

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
