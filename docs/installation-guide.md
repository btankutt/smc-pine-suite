# Installation Guide

## Free indicators (open source)

Each free indicator is a standalone `.pine` file under [indicators/](../indicators/).

1. Open [TradingView](https://www.tradingview.com) and load any chart.
2. Open the **Pine Editor** (bottom panel toolbar).
3. Copy the full contents of the indicator's `.pine` file from this repository (e.g. [`smc-toolkit.pine`](../indicators/01-smc-toolkit/smc-toolkit.pine)).
4. Paste into the Pine Editor, press **Save**, give it a name.
5. Click **Add to chart**.
6. Open the gear icon on the indicator to configure inputs — every input is grouped and documented in the indicator's README.

### Updating

When a new version is released (see each indicator's Changelog section), repeat the steps above — paste the new source over the old script and save. Your chart-level input settings are preserved as long as input names match.

### Alerts

All alert flags in this suite fire on **confirmed bars only**. When creating alerts, choose **"Once Per Bar Close"** as the trigger frequency.

## Pro Confluence Engine (invite-only)

The Pro engine is **not** installed from source — it is granted to your TradingView account:

1. Arrange access per [pro/PRICING.md](../pro/PRICING.md).
2. On TradingView: **Indicators → Invite-only scripts → Pro Confluence Engine**.
3. Add to chart and pick a preset (Scalp / Intraday / Swing) plus your asset class — see [pro/FEATURES.md](../pro/FEATURES.md) for every input.
4. For webhook automation, create one alert with **"Any alert() function call"** and paste your webhook URL; the JSON payload format is documented in [pro/FEATURES.md](../pro/FEATURES.md).

## Troubleshooting

- **"Script could not be compiled"** after pasting a free indicator: make sure you copied the entire file including the `//@version=6` line, with no truncation.
- **No drawings appear:** check the indicator's Enable toggles, and remember pivots confirm `swing_length` bars late by design.
- **Alerts fire and then conditions "disappear":** you selected an intrabar frequency. Use "Once Per Bar Close".
