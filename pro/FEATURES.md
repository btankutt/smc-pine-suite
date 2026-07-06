# Pro Confluence Engine — Feature Reference

This document describes the **behavior** of the Pro Confluence Engine v1.0.0. The source code is proprietary and distributed only via TradingView's invite-only system (see [LICENSE-PRO](../LICENSE-PRO)).

---

## 1. Confluence scoring

Each of the six components produces a sub-score in [0, 1] for **both** directions independently, every bar. The total score per side is the weight-normalized sum, scaled to 0–100:

```
score = 100 x sum(w_i x s_i) / sum(w_i)
```

- Weights are inputs (0–50 each, defaults 25/20/15/15/15/10). Setting a weight to 0 disables the component and removes it from both numerator and denominator, so the scale is always a true 0–100.
- The dashboard shows each component as a 5-step bar so you can see *which* evidence is loaded at a glance.

### Component details

| Component | Sub-score logic |
|-----------|----------------|
| **Structure** | Trend direction from the BoS/CHoCH state machine (same detection as the free SMC Toolkit). While the trend is aligned the score holds a 0.4 floor; a fresh structural break lifts it to 1.0 and decays linearly over `struct_decay` bars back to the floor. |
| **Zones (OB + FVG)** | Order Blocks (last opposite candle before a break, optional volume filter) and FVGs (ATR-filtered 3-bar gaps) are pooled per direction. A zone must first be **armed** — price has to leave it by `zone_arm_atr` ATRs — before it may score (arming takes effect the following bar, so one wide bar can never arm a zone and score its own touch). A **touch** is an *entry* event — the previous bar must have been outside the zone; consolidating inside does not re-trigger. A touch scores 1.0 and decays over 8 bars; mere proximity is capped at 0.3. Zones die on a close through the far edge or after `zone_max_age` bars. The component takes the **max** over live zones (OB and FVG never sum — one impulse usually prints both). |
| **Liquidity** | Equal highs/lows within an ATR tolerance form BSL/SSL pools. A sweep (wick through, close back inside) on the relevant side scores 1.0 and decays linearly over `sweep_decay` bars. A level that price cleanly *closes* through is silently invalidated — consumed pools can never fire stale sweeps later. |
| **Volume** | 60% direction-gated relative volume (only candles in the signal direction count; saturation point per asset class: Crypto 2.5x / Forex 1.8x / Metals 2.0x) + 40% rolling-POC location (close on the right side of the highest-volume price bin of the last N bars). Not a session volume profile. |
| **HTF bias** | One `request.security` call returns the last **confirmed** higher-timeframe close and EMA 21/50. Full EMA stack alignment = 1.0, close above/below the slow EMA only = 0.5. "Auto" maps chart TF to HTF (≤5m→1h, ≤1h→4h, ≤4h→D, else W). Optional hard filter blocks counter-HTF signals entirely. |
| **Divergence** | Regular RSI divergence measured at the same confirmed pivots the structure engine uses (price LL + RSI HL = bullish, mirrored for bearish), decaying over `div_decay` bars. |

## 2. Adaptive regime engine

ATR percentile over `regime_lookback` bars classifies volatility:

| Regime | Condition | Threshold | SL width | Cooldown |
|--------|-----------|:--:|:--:|:--:|
| LOW | ATR pct ≤ 30 | +8 | x0.85 | x1.0 |
| NORMAL | 30–70 | +0 | x1.0 | x1.0 |
| HIGH | ATR pct ≥ 70 | +5 | x1.3 | x1.5 |

Rationale: low volatility = chop, demand more confluence; high volatility = real moves but wickier noise — slightly higher bar, wider stops, slower cadence. Toggle off to freeze the regime at NORMAL. The effective threshold is clamped at 99 so regime bumps can never make signals mathematically unfirable, and signals stay locked until the ATR percentile itself is fully warmed up.

## 3. Signal engine

A signal fires **only on a confirmed bar** when ALL of the following hold:

1. Score ≥ adaptive threshold,
2. an event trigger occurred this bar (structural break, sweep, zone touch, or divergence — no drift-signals),
3. dominance gap: the signal side's score exceeds the other side by ≥ `dominance_gap` (default 20),
4. at least `min_active` components (default 3) score ≥ 0.6 in the signal direction,
5. cooldown elapsed (shared across directions, regime-scaled),
6. optional: session window, HTF hard filter, one-signal-at-a-time slot.

Warmup guard: no signals until the regime and POC windows are fully formed.

## 4. Risk module

- **Stop:** structural (last swing ± `sl_buf_atr` ATR buffer) with an ATR floor (`sl_atr_mult`, regime-scaled). Structural stops farther than 3 ATRs fall back to the ATR stop.
- **Target:** entry + R:R x stop distance (R:R per preset: 1.5 / 2.0 / 2.5).
- **Display:** entry/SL/TP lines + a compact label for the latest signal (fixed drawing budget — handles are reused).
- **Size hint:** `account x risk% / stop distance`, appended to the signal label and the webhook JSON when an account size is set. Informational only — raw units, ignores leverage/contract size/fees.

## 5. Hypothetical outcome tracker

- Entry = signal bar's close. Evaluation starts the **next** confirmed bar (the signal bar's own range is never inspected).
- Outcomes: **WIN** (TP touched), **LOSS** (SL touched), **AMBIGUOUS** (both in one bar — intrabar order is unknowable from OHLC, counted as a loss and displayed separately), **EXPIRED** (neither within `max_hold` bars — closed mark-to-market, excluded from win rate but included in the R sum).
- SL/TP are frozen at signal time; no trailing, no retro-editing, no survivorship filtering. Gaps are not fill-modeled.
- With "One signal at a time" off, a new signal closes the still-open tracked trade mark-to-market as EXPIRED — no fired signal ever silently vanishes from the stats.
- Dashboard line: `12W/9L/1A/2E - 54.5% - SumR +6.3` over the last 100 resolved signals.

## 6. Presets

| Preset | Swing len | Threshold | Cooldown | SL ATR | R:R | POC window | Max hold |
|--------|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| Scalp | 3 | 70 | 10 | 1.0 | 1.5 | 80 | 60 |
| Intraday | 5 | 65 | 8 | 1.2 | 2.0 | 150 | 100 |
| Swing | 8 | 60 | 5 | 1.5 | 2.5 | 200 | 150 |
| Custom | — all sliders live — | | | | | | |

## 7. Alerts

- `alertcondition`: Long Signal, Short Signal, Long Armed, Short Armed (score crosses threshold−10), Regime Change, Hypo TP Hit, Hypo SL Hit. All fire on confirmed bars only — any TradingView frequency is safe; recommended **Once Per Bar Close**.
- **Webhook JSON** via `alert()` on each signal: `{"engine":"PCE","ver":"1.0.0","sym":…,"exch":…,"tf":…,"dir":…,"score":…,"entry":…,"sl":…,"tp":…,"rr":…,"regime":…,"bar_time":…}` — prices formatted to the instrument's tick size. Create ONE alert with "Any alert() function call".

## 8. Non-repaint guarantees

- All `ta.*` calls run unconditionally at global scope; only state mutation is gated on `barstate.isconfirmed`.
- The single `request.security` call uses `expression[1]` + `lookahead_off` — values come from the last **closed** HTF bar and are identical on historical bars, realtime bars, and after a reload. Cost: one HTF bar of lag, by design.
- Objects (zones, levels) are never evaluated on their own creation bar.
- Fixed drawing budgets; no reliance on TradingView's silent garbage collection.

---

*Educational tool, not financial advice. Hypothetical tracker results ignore fees, spread, slippage, and intrabar order.*
