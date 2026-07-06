# MTF Divergence Scanner

> 🚧 **Planned — not yet released.**

Multi-timeframe RSI/MACD divergence detection for Pine Script v6.

Planned scope:

- Regular and hidden divergences at confirmed pivots (no repainting — pivot-lag by design)
- Chart timeframe + up to two higher timeframes via the non-repainting `request.security` idiom
- Divergence lines drawn between the two pivots, strength-graded
- Alert conditions per timeframe and direction

Until this ships, chart-timeframe regular RSI divergence is available inside the [Pro Confluence Engine](../../pro/README.md)'s divergence component.

Follow the [roadmap](../../README.md#roadmap) for status.
