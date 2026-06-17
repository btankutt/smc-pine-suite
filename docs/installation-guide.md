# Installation Guide

> How to add any SMC Pine Suite indicator to a TradingView chart, configure it, and set up alerts.

🇹🇷 Türkçe sürüm bu dosyanın [ikinci yarısındadır](#kurulum-kılavuzu-türkçe).

---

## Requirements

- A TradingView account (the free tier is sufficient for all four open-source indicators).
- A chart on any symbol and timeframe.
- Pine Script v6 — TradingView's current engine, used by every script in this suite. No setup needed; it's built into the Pine Editor.

---

## Step 1 — Open the Pine Editor

1. Open any chart on [TradingView](https://www.tradingview.com).
2. At the bottom of the screen, click the **Pine Editor** tab.

If you don't see it, enable it from the bottom toolbar's panel menu.

## Step 2 — Paste an indicator

1. In this repository, open the indicator you want, e.g. [`indicators/02-volume-profile-plus/volume-profile-plus.pine`](../indicators/02-volume-profile-plus/volume-profile-plus.pine).
2. Click the **Raw** button on GitHub and copy the entire file (Ctrl/Cmd-A, Ctrl/Cmd-C).
3. In the Pine Editor, select all existing text and replace it with the copied code.
4. Click **Save** and give the script a name (e.g. "Volume Profile Plus").

## Step 3 — Add it to the chart

Click **Add to chart**. The script compiles (usually 1–2 seconds) and appears on your chart. If you see a red error marker, make sure you copied the *entire* file including the `//@version=6` line at the top.

## Step 4 — Configure inputs

Hover the indicator name on the chart and click the **gear icon** (Settings). Inputs are grouped logically (e.g. Calculation, Display). Hover any input label to see its tooltip. Sensible defaults are provided; start there and adjust per instrument and timeframe.

## Step 5 — Set up alerts (optional)

Indicators that expose alert conditions can drive TradingView alerts:

1. Click the **Alarm clock (Alerts)** icon in the right toolbar, or right-click the chart → **Add alert**.
2. Under **Condition**, select the indicator, then choose one of its alert conditions (e.g. "Price crossed POC", "Bullish divergence").
3. Set the trigger (Once per bar close is recommended for non-repainting behaviour).
4. Choose how you want to be notified (popup, email, webhook) and click **Create**.

---

## Indicator-specific notes

| Indicator | First thing to set | Notes |
|-----------|--------------------|-------|
| [SMC Toolkit](../indicators/01-smc-toolkit/) | `Swing detection length` | Use 5 for 1H+, 3 for 15M and below |
| [Volume Profile Plus](../indicators/02-volume-profile-plus/) | `Profile range` (Session/Fixed) | Use Fixed lookback for 24/7 crypto |
| [MTF Divergence Scanner](../indicators/03-mtf-divergence/) | The three timeframes | Leave a slot blank to use the chart timeframe |
| [ATR Helper](../indicators/04-atr-helper/) | `Account size` & `Risk per trade (%)` | Set `Value per 1.0 price move` for futures/FX |

---

## Troubleshooting

- **"Add to chart" is greyed out** — the script hasn't compiled. Check the console at the bottom of the Pine Editor for the error and confirm you pasted the whole file.
- **Nothing draws** — many scripts draw on the latest bars only (e.g. the volume profile). Scroll to the right edge of the chart.
- **Too many / too few signals** — adjust the sensitivity inputs (pivot length, FVG min size, divergence pivots). Lower values = more sensitive.
- **A drawing limit warning** — these scripts cap drawings at 500; older drawings are removed automatically. This is expected on long histories.

---

<a name="kurulum-kılavuzu-türkçe"></a>

# Kurulum Kılavuzu (Türkçe)

> Herhangi bir SMC Pine Suite göstergesini TradingView grafiğine ekleme, yapılandırma ve alarm kurma.

## Gereksinimler
- Bir TradingView hesabı (dört açık kaynak gösterge için ücretsiz katman yeterli).
- Herhangi bir sembol ve zaman diliminde bir grafik.
- Pine Script v6 — bu paketteki her scriptin kullandığı güncel motor. Kurulum gerekmez; Pine Editor'e gömülüdür.

## Adım 1 — Pine Editor'ü aç
1. [TradingView](https://www.tradingview.com)'de herhangi bir grafiği aç.
2. Ekranın altındaki **Pine Editor** sekmesine tıkla.

## Adım 2 — Göstergeyi yapıştır
1. Bu repoda istediğin göstergeyi aç, örn. [`volume-profile-plus.pine`](../indicators/02-volume-profile-plus/volume-profile-plus.pine).
2. GitHub'da **Raw** düğmesine tıkla ve tüm dosyayı kopyala.
3. Pine Editor'de mevcut metni seç ve kopyaladığın kodla değiştir.
4. **Kaydet**'e tıkla ve scripte bir ad ver.

## Adım 3 — Grafiğe ekle
**Grafiğe ekle**'ye tıkla. Script derlenir (genelde 1–2 saniye) ve grafiğine eklenir. Kırmızı hata görürsen, en üstteki `//@version=6` satırı dâhil *tüm* dosyayı kopyaladığından emin ol.

## Adım 4 — Input'ları yapılandır
Grafikte gösterge adının üzerine gel ve **dişli (Ayarlar)** simgesine tıkla. Input'lar mantıksal gruplara ayrılmıştır. Herhangi bir input etiketinin üzerine gelerek ipucunu gör. Makul varsayılanlar verilmiştir; oradan başla ve enstrüman/zaman dilimine göre ayarla.

## Adım 5 — Alarm kur (isteğe bağlı)
1. Sağ araç çubuğundaki **Alarm** simgesine tıkla veya grafiğe sağ tıkla → **Alarm ekle**.
2. **Koşul** altında göstergeyi seç, sonra alarm koşullarından birini seç (örn. "Price crossed POC", "Bullish divergence").
3. Tetikleyiciyi ayarla (repaint etmeyen davranış için "Bar kapanışında bir kez" önerilir).
4. Bildirim şeklini seç ve **Oluştur**'a tıkla.

## Sorun giderme
- **"Grafiğe ekle" pasif** — script derlenmemiş. Pine Editor'ün altındaki konsoldan hatayı kontrol et ve tüm dosyayı yapıştırdığından emin ol.
- **Hiçbir şey çizilmiyor** — birçok script yalnızca son barlarda çizer (örn. hacim profili). Grafiğin sağ kenarına kaydır.
- **Çok fazla / çok az sinyal** — hassasiyet input'larını ayarla (pivot uzunluğu, FVG min boyut, uyumsuzluk pivot'ları). Düşük değer = daha hassas.
- **Çizim limiti uyarısı** — bu scriptler çizimleri 500 ile sınırlar; eskileri otomatik silinir. Uzun geçmişlerde beklenen bir durumdur.
