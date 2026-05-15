# SMC Pine Suite

> Production-grade Pine Script v6 indicators for Smart Money Concepts traders.
> Built by an algorithmic trading systems developer with 12+ years of professional experience.

[![License: MPL 2.0](https://img.shields.io/badge/License-MPL_2.0-brightgreen.svg)](https://opensource.org/licenses/MPL-2.0)
[![Pine Script](https://img.shields.io/badge/Pine_Script-v6-2962FF.svg)](https://www.tradingview.com/pine-script-docs/welcome/)
[![TradingView](https://img.shields.io/badge/TradingView-Community-26a69a.svg)](https://www.tradingview.com)

🇹🇷 [Türkçe README](README.tr.md)

---

## Overview

A curated collection of professional Pine Script v6 indicators focused on Smart Money Concepts (SMC) and modern price action analysis. Each indicator is designed as a standalone tool with clear visual output, configurable parameters, and alert-ready logic.

This suite reflects real-world insights from operating production trading systems for cryptocurrency, forex, and metals markets. The code is open-source under MPL 2.0 — fork it, study it, adapt it to your strategy.

For a more comprehensive confluence system that integrates all four free indicators, see [Pro Confluence Engine](pro/README.md) (invite-only).

---

## Indicators

### 🆓 Free (Open Source)

| Indicator | Purpose | Status |
|-----------|---------|--------|
| [SMC Toolkit](indicators/01-smc-toolkit/) | Order Blocks, FVG, Liquidity Sweeps, BoS/CHoCH | ✅ Live |
| [Volume Profile Plus](indicators/02-volume-profile-plus/) | Session-based VP, POC, VAH/VAL, Volume Nodes | 🚧 Coming Soon |
| [MTF Divergence Scanner](indicators/03-mtf-divergence/) | Multi-timeframe RSI/MACD divergence detection | 🚧 Coming Soon |
| [ATR Helper](indicators/04-atr-helper/) | Dynamic SL/TP, R:R visualization, position sizing | 🚧 Coming Soon |

### 💎 Pro (Invite-Only)

| Indicator | Purpose | Status |
|-----------|---------|--------|
| [Pro Confluence Engine](pro/) | All-in-one signal system combining the 4 free indicators with adaptive scoring | 🚧 Coming Soon |

---

## Quick Start

Each indicator is a standalone `.pine` file. To use:

1. Copy the contents of any `.pine` file from this repo
2. Open TradingView Pine Editor (Charts → Pine Editor)
3. Paste the code, click **"Add to chart"**
4. Configure inputs in the indicator settings

For detailed documentation per indicator, see the README inside each folder.

---

## Pine Script v6

All indicators use Pine Script v6 — TradingView's current major version, released November 2024. Key v6 features used in this suite:

- **Dynamic `request.*()`** for multi-symbol/timeframe scanning
- **Short-circuit boolean evaluation** for efficient condition chains
- **User-defined types** for clean state management
- **Methods (dot notation)** for readable array/matrix operations
- **Built-in `log.*()`** for debugging without polluting charts

If you're still on v5, see TradingView's [official v6 migration guide](https://www.tradingview.com/pine-script-docs/migration-guides/to-pine-version-6/).

---

## Trading Philosophy

This suite is built around a few non-negotiable principles:

1. **Price action over lagging indicators** — SMC and volume context first
2. **Confluence over single signals** — no single indicator decides; convergence does
3. **Risk management is half the strategy** — every trade has a pre-defined SL/TP
4. **Backtesting is mandatory** — no live trading without statistical evidence
5. **Markets evolve, code should too** — these indicators are versioned and updated

See [docs/trading-philosophy.md](docs/trading-philosophy.md) for the full doctrine.

---

## Roadmap

Already implemented and shipped:

- [x] Repository structure and documentation framework
- [x] SMC Toolkit — Order Blocks, FVG, Liquidity Sweeps, BoS/CHoCH ([details](indicators/01-smc-toolkit/))

Planned future additions:

- [ ] Volume Profile Plus (Session-based with POC/VAH/VAL)
- [ ] MTF Divergence Scanner (RSI/MACD across timeframes)
- [ ] ATR Helper (Dynamic SL/TP and R:R visualization)
- [ ] Pro Confluence Engine (combines all four; invite-only)
- [ ] Comprehensive backtest results and statistical evidence
- [ ] Trading strategy companion guides (per indicator)

---

## Related Projects

- [rpi-rfid-access-control](https://github.com/btankutt/rpi-rfid-access-control) — Production-grade IoT access control system (Python + FastAPI + Raspberry Pi)

---

## License

This repository uses **two licenses**:

- **MPL 2.0** — All free indicators in `indicators/` (file-based copyleft)
- **Proprietary** — Pro Confluence Engine in `pro/` (invite-only access)

See [LICENSE-FREE](LICENSE-FREE) and [LICENSE-PRO](LICENSE-PRO) for full text.

---

## Author

**Barış Tankut** — Algorithmic Trading Systems & IoT Embedded Engineer
12+ years of professional software/hardware development experience.

- GitHub: [@btankutt](https://github.com/btankutt)
- Active in: Cryptocurrency · Forex · Metals · Algorithmic Strategy Development
- Open to consulting & freelance work in trading systems, Pine Script development, and IoT integration

---

## Disclaimer

These indicators are **educational tools**, not financial advice. Past performance does not guarantee future results. Always:

- Backtest thoroughly on historical data
- Forward-test in demo accounts before live trading
- Use proper risk management (position sizing, stop losses)
- Understand that no indicator is a substitute for trader judgment
