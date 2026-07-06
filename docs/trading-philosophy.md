# Trading Philosophy

The full doctrine behind SMC Pine Suite. Every indicator in this repo is designed around these five principles.

## 1. Price action over lagging indicators

Moving-average crossovers tell you what already happened. Market structure (BoS/CHoCH), order blocks, fair value gaps, and liquidity levels describe *where participants are positioned* — which is what actually moves price next. Oscillators appear in this suite only as secondary evidence (divergence), never as a primary signal.

## 2. Confluence over single signals

No single indicator decides; convergence does. A BoS alone is noise on half of all charts. A BoS *plus* a retest of an unmitigated order block *plus* a liquidity sweep *plus* above-average volume is a trade. This is why the [Pro Confluence Engine](../pro/README.md) scores weighted evidence instead of firing on any one event — and why the free indicators are designed to be readable together on one chart.

## 3. Risk management is half the strategy

Every trade has a pre-defined invalidation (SL) and target (TP) *before* entry. Stops belong beyond structure (the last swing, the far edge of the zone), not at round numbers or fixed pips. Position size derives from the stop distance, never the other way around. A 45% win rate with 2R winners compounds; a 70% win rate with uncapped losers goes to zero.

## 4. Backtesting is mandatory

No live trading without statistical evidence. That means: walk-forward testing on the timeframes and symbols you actually trade, honest accounting (ambiguous bars where SL and TP are both touched count against you), and forward-testing in a demo account before real size. Tools in this suite deliberately avoid repainting so that what you backtest is what you would have seen live.

## 5. Markets evolve, code should too

Regimes change: volatility expands and compresses, correlations rotate, edges decay. These indicators are versioned, changelogged, and updated when evidence demands it. The Pro engine's adaptive regime layer exists precisely because one static parameter set does not survive both chop and expansion.

---

*None of this is financial advice. It is a description of the engineering assumptions behind the tools.*
