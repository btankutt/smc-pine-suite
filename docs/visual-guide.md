# Visual Guide

> How to read what each indicator draws on the chart. A reference for the colors, lines, boxes, and labels you'll see.

🇹🇷 Türkçe sürüm bu dosyanın [ikinci yarısındadır](#görsel-kılavuz-türkçe).

> 📷 Annotated screenshots are added per indicator over time. Until an indicator's images land, use the descriptions below — they map one-to-one to what the code draws.

---

## SMC Toolkit

| Element | Appearance | Meaning |
|---------|-----------|---------|
| **BoS label** | Small green/red label at a break | Break of Structure — trend continuation |
| **CHoCH label** | Small green/red label at a break | Change of Character — possible reversal |
| **Order Block** | Green (bullish) / red (bearish) box | Last opposite candle before a break; an entry zone |
| **Mitigated OB** | Box recolored gray | Price has tagged the zone; it's "used up" |
| **Fair Value Gap** | Aqua (bull) / orange (bear) box | 3-candle imbalance |
| **Filled FVG** | Box recolored gray | Price has returned into the gap |
| **Liquidity line** | Dashed aqua/orange line | Equal highs (BSL) / equal lows (SSL) |
| **Sweep label** | "BSL/SSL Swept" | A stop-run that closed back inside |

## Volume Profile Plus

| Element | Appearance | Meaning |
|---------|-----------|---------|
| **Histogram bars** | Horizontal bars to the right | Volume traded at each price row |
| **POC line** | Solid orange line + label | Point of Control — highest-volume price |
| **VAH / VAL lines** | Dashed lines + labels | Top/bottom of the value area |
| **Value area shading** | Light band between VAH and VAL | The configurable % of volume around the POC |
| **HVN bars** | Green | High-volume nodes — price tends to stall here |
| **LVN bars** | Red | Low-volume nodes — price tends to move fast here |

## MTF Divergence Scanner

| Element | Appearance | Meaning |
|---------|-----------|---------|
| **Bull label** | Green label below the bar | "Reg/Hid Bull" + timeframe; bullish divergence |
| **Bear label** | Red label above the bar | "Reg/Hid Bear" + timeframe; bearish divergence |
| **Status table** | Top-right panel | Last divergence direction per timeframe |
| **"Reg"** | In the label text | Regular divergence (reversal) |
| **"Hid"** | In the label text | Hidden divergence (continuation) |

## ATR Helper

| Element | Appearance | Meaning |
|---------|-----------|---------|
| **Entry line** | Blue line + label | Your planned entry price |
| **Stop line** | Red line + label | ATR-based stop-loss |
| **Risk zone** | Red shaded band | Entry → stop region |
| **Target lines** | Green lines + "TP1/2/3 (xR)" labels | R-multiple take-profit targets |
| **Reward zone** | Green shaded band | Entry → furthest target region |
| **Summary table** | Bottom-right panel | ATR, entry, stop, R:R, risk amount, position size |

---

## Reading confluence

The point of the suite is overlap. A high-probability long, for example, looks like:

- A higher-timeframe **CHoCH/BoS** to the upside (structure)
- Price retracing into an **unmitigated bullish Order Block** or **unfilled FVG** (location)
- That zone aligning with the **Value Area Low** or a **POC** from below (value)
- A **regular bullish divergence** or a **sell-side liquidity sweep** there (trigger)
- A clean **ATR stop** beyond the zone with a favourable R-multiple to the next liquidity pool (risk)

When several of these line up at the same price, the [Pro Confluence Engine](../pro/README.md) surfaces it as a single high score.

---

<a name="görsel-kılavuz-türkçe"></a>

# Görsel Kılavuz (Türkçe)

> Her göstergenin grafiğe çizdiğini nasıl okuyacağın. Göreceğin renkler, çizgiler, kutular ve etiketler için bir referans.

> 📷 Açıklamalı ekran görüntüleri zamanla gösterge başına eklenir. Bir göstergenin görselleri gelene kadar aşağıdaki açıklamaları kullan — kodun çizdiğiyle birebir eşleşir.

## SMC Toolkit
- **BoS etiketi** — kırılımda küçük yeşil/kırmızı etiket: Yapı Kırılımı, trend devamı.
- **CHoCH etiketi** — kırılımda küçük etiket: Karakter Değişimi, olası dönüş.
- **Order Block** — yeşil (bullish) / kırmızı (bearish) kutu: kırılım öncesi son ters mum; giriş bölgesi.
- **Mitige OB** — gri kutu: fiyat bölgeye dokundu, "tükendi".
- **FVG** — aqua (bull) / turuncu (bear) kutu: 3-mum dengesizliği. Dolunca gri olur.
- **Likidite çizgisi** — kesikli aqua/turuncu: eşit highs (BSL) / eşit lows (SSL).
- **Sweep etiketi** — "BSL/SSL Swept": içeri geri kapanan stop-run.

## Volume Profile Plus
- **Histogram barları** — sağa yatay barlar: her fiyat satırında işlem gören hacim.
- **POC çizgisi** — düz turuncu çizgi + etiket: en yüksek hacimli fiyat.
- **VAH / VAL çizgileri** — kesikli çizgiler + etiketler: değer alanının üst/alt sınırı.
- **Değer alanı gölgesi** — VAH ile VAL arası bant: POC çevresindeki yapılandırılabilir hacim oranı.
- **HVN barları** (yeşil) — fiyat burada duraksar. **LVN barları** (kırmızı) — fiyat buradan hızlı geçer.

## MTF Divergence Scanner
- **Bull etiketi** — barın altında yeşil: "Reg/Hid Bull" + zaman dilimi.
- **Bear etiketi** — barın üstünde kırmızı: "Reg/Hid Bear" + zaman dilimi.
- **Durum tablosu** — sağ üst panel: zaman dilimi başına son uyumsuzluk yönü.
- **"Reg"** — regular (dönüş), **"Hid"** — hidden (devam).

## ATR Helper
- **Giriş çizgisi** (mavi) — planlanan giriş. **Stop çizgisi** (kırmızı) — ATR stop.
- **Risk bölgesi** (kırmızı bant) — giriş → stop. **Hedef çizgileri** (yeşil, "TP1/2/3 (xR)") — R-katlı hedefler.
- **Ödül bölgesi** (yeşil bant) — giriş → en uzak hedef.
- **Özet tablo** (sağ alt) — ATR, giriş, stop, R:R, risk tutarı, pozisyon büyüklüğü.

## Konfluans okuma
Paketin amacı örtüşmedir. Örneğin yüksek-olasılıklı bir long: yukarı yönlü üst-zaman-dilimi **CHoCH/BoS** (yapı) + **mitige olmamış bullish OB / dolmamış FVG**'ye geri çekilme (konum) + bu bölgenin **VAL** veya alttan bir **POC** ile hizalanması (değer) + orada **regular bullish uyumsuzluk** veya **satış-tarafı likidite sweep'i** (tetikleyici) + bölgenin ötesinde, sonraki likidite havuzuna iyi R-katlı **ATR stop** (risk). Bunlar aynı fiyatta hizalandığında [Pro Confluence Engine](../pro/README.md) bunu tek bir yüksek skor olarak gösterir.
