# ATR Helper

> ATR-based trade planning tool for TradingView — dynamic stop-loss, R-multiple targets, risk/reward zones, and position sizing in a single Pine Script v6 script.

---

## Overview

A standalone trade-planning overlay. You set a direction and an entry; the script derives a volatility-adjusted **stop-loss** from an ATR multiple, projects up to three **take-profit** targets as multiples of the risk distance (R multiples), shades the **risk and reward zones**, and computes the **position size** that keeps your loss at a fixed percentage of the account if the stop is hit.

This turns the three hardest parts of any trade — where the stop goes, where the targets go, and how big the position should be — into one consistent, ATR-driven calculation.

This indicator is part of [SMC Pine Suite](../../README.md). Built with Pine Script v6: `switch` for ATR smoothing selection, handle arrays for clean redraws, and a `table` for the trade summary.

---

## Features

### 1. Dynamic ATR Stop

The stop distance is `ATR × multiple`, so it widens in volatile conditions and tightens in quiet ones. ATR smoothing is selectable (RMA, SMA, EMA, WMA).

### 2. R-Multiple Targets

Each take-profit is defined as a multiple of the risk distance, not a fixed price. A 2R target is always twice as far from entry as the stop, regardless of instrument or volatility — so R:R is fixed by design (TP1 = 1R, TP2 = 2R, TP3 = 3R by default, all configurable).

### 3. Risk / Reward Visualization

The entry-to-stop band is shaded red and the entry-to-furthest-target band is shaded green, with horizontal lines and price labels for entry, stop, and every enabled target.

### 4. Position Sizing

From `account size`, `risk per trade (%)`, and the stop distance, the script computes the position size that risks exactly the chosen percentage if stopped out:

```
risk amount   = account × risk%
risk per unit = stop distance × value-per-point
position size = risk amount ÷ risk per unit
```

The `value per 1.0 price move` input handles instruments where one price unit is not one account-currency unit (futures, FX). Leave it at 1 for crypto and most stocks.

### 5. Summary Table + Alerts

A bottom-right table lists ATR, entry, stop, risk distance, R:R for each target, risk amount, and position size. Alerts fire when price crosses the planned stop or the first target. The alerts compare price to the **planned** levels, so use a **Manual** entry price — with `Current close` the levels trail every close and can never be crossed.

---

## Installation

1. Open TradingView and navigate to any chart
2. Open the **Pine Editor** (bottom panel)
3. Copy the contents of [`atr-helper.pine`](atr-helper.pine)
4. Paste into Pine Editor, click **"Save"**, then **"Add to chart"**

---

## Configuration

### ATR
- `ATR length` (default: 14)
- `ATR smoothing` (default: RMA) — RMA / SMA / EMA / WMA
- `Stop-loss ATR multiple` (default: 1.5)

### Trade Setup
- `Direction` (default: Long) — Long or Short
- `Entry price` (default: Current close) — Current close or Manual
- `Manual entry price` — used when Entry price = Manual

### Take Profit (R multiples)
- `TP1 / TP2 / TP3` — each with an on/off toggle and an R multiple (default 1 / 2 / 3)

### Position Sizing
- `Show position sizing` (default: true)
- `Account size` (default: 10000)
- `Risk per trade (%)` (default: 1.0)
- `Value per 1.0 price move (per unit)` (default: 1.0)

### Display
- `Show summary table`, colors, and `Zone transparency`
- Entry / stop / target lines extend to the right as stable horizontal rays (no scroll/zoom drift)

---

## Pine Script v6 Implementation Notes

- **`switch` for smoothing** — ATR smoothing method is chosen with a `switch` over `ta.tr(true)`
- **R-multiple math** — targets are derived from the stop distance, so the displayed R:R is exact by construction
- **Handle arrays + `clear_plan()`** — lines, boxes, and labels are tracked and deleted before each redraw on `barstate.islast`
- **Sizing guard** — position size is `na`-guarded against a zero stop distance to avoid divide-by-zero

---

## How to Use

1. Pick your **direction** and either accept the current close as entry or type a **manual entry** at the level you intend to trade.
2. Tune the **ATR multiple** so the stop sits beyond the noise — past a recent swing or Order Block, not inside it.
3. Read the **position size** from the table and use it as your order quantity; this is what keeps every loss the same fraction of the account.
4. Pair with the [SMC Toolkit](../01-smc-toolkit): place the entry at an Order Block / FVG, set the ATR stop beyond the zone, and target the next liquidity pool with the R targets.

> ⚠️ Position sizing assumes the stop is honoured at the planned price. Slippage, gaps, and fees mean realized risk can exceed the planned amount. Size conservatively.

---

## License

This indicator is open source under the **Mozilla Public License 2.0** (MPL 2.0). See [LICENSE-FREE](../../LICENSE-FREE) for full text.

---

## Disclaimer

This indicator is provided **as is**, without any guarantee of profitability or accuracy. Nothing here is financial advice. Always backtest on historical data, forward-test in a demo account, and use position sizing and stop-losses appropriate to your account. Trading involves risk. Past performance does not guarantee future results.

---

## Author

**Barış Tankut** ([@btankutt](https://github.com/btankutt))
Algorithmic Trading Systems & IoT Embedded Engineer

Part of [SMC Pine Suite](../../README.md) — production-grade Pine Script v6 indicators.