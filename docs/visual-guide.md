# Visual Guide

What every on-chart element in the suite means, at a glance.

## SMC Toolkit

| Element | Appearance | Meaning |
|---------|-----------|---------|
| **BoS label** | Green (above bar) / red (below bar), tiny | Close broke the last swing in the trend direction — continuation |
| **CHoCH label** | Same styling as BoS, text "CHoCH" | Close broke the last swing *against* the trend — potential reversal |
| **Bullish OB** | Green box, extends right | Last down-candle before an upside break; potential demand on retest |
| **Bearish OB** | Red box, extends right | Last up-candle before a downside break; potential supply on retest |
| **Bullish FVG** | Aqua box | 3-candle gap below price (low > high two bars back) |
| **Bearish FVG** | Orange box | 3-candle gap above price |
| **Gray frozen box** | Gray fill, no longer extending | Mitigated OB / filled FVG — the zone has been consumed |
| **Aqua dashed line** | Extends right | BSL — equal highs (buy-side liquidity pool) |
| **Orange dashed line** | Extends right | SSL — equal lows (sell-side liquidity pool) |
| **Gray frozen line** | Dashed, stops at its last bar | Swept or broken liquidity level — no longer live |
| **"BSL/SSL Swept" label** | Red above / green below | Wick beyond the level with a close back inside — stop-hunt event |

Reading the chart: **active** zones and levels are colored and project to the right edge; anything gray is history kept only for context.

## Pro Confluence Engine

| Element | Meaning |
|---------|---------|
| **Green triangle (below bar)** | Confirmed long signal (score, trigger, dominance, cooldown all passed) |
| **Red triangle (above bar)** | Confirmed short signal |
| **Gray dotted line** | Latest signal's entry price |
| **Red / green solid lines** | Latest signal's SL / TP |
| **Signal label** | Direction, score, SL/TP prices, and R:R for the latest signal |
| **Gray dotted horizontal** | Rolling POC (highest-volume price bin of the lookback window) |
| **Purple "Div" label** | Regular RSI divergence at a confirmed pivot |
| **Dashboard** | Score per side, 5-step bar per component, regime state, HTF bias, last signal, hypothetical stats (W/L/A/E) |

Dashboard component bars: `####-` means the component scores 0.8 in that direction. The score cell turns green/red once it clears the adaptive threshold.

## Screenshots

See [indicators/01-smc-toolkit/screenshots/](../indicators/01-smc-toolkit/screenshots/) for annotated examples (BTC 1D structure breaks, BTC 4H order block + liquidity).
