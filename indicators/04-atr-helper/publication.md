# ATR Helper — Dynamic SL/TP, R:R & Position Sizing

## 🇬🇧 English

An ATR-based trade-planning overlay that turns stop placement, targets, and position size into one consistent calculation, in one Pine Script v6 indicator:

**Features:**
- 🛑 **Dynamic ATR stop** — `ATR × multiple`, selectable smoothing (RMA/SMA/EMA/WMA)
- 🎯 **R-multiple targets** — up to 3 TPs defined as multiples of the risk distance (R:R is exact by design)
- 🟥🟩 **Risk / reward zones** — shaded entry→stop and entry→target bands with price labels
- 🧮 **Position sizing** — from account size, risk %, and stop distance (with a value-per-point input for futures/FX)
- 🔔 **Alerts** — when price crosses the planned stop or first target (set a Manual entry price; with "Current close" the levels trail the close and never cross)

**Built for traders who:**
- Want volatility-adjusted stops instead of fixed-pip stops
- Size every position to a fixed % account risk
- Plan entries/targets visually before committing

**Pine Script v6 features used:**
- `switch` for ATR smoothing selection over `ta.tr(true)`
- R-multiple math so the displayed R:R is exact
- Handle arrays cleared before each redraw on `barstate.islast`
- `na`-guarded sizing against a zero stop distance

**How to use:**
1. Add to chart
2. Pick direction; accept the current close or type a manual entry
3. Tune the ATR multiple so the stop sits beyond the noise
4. Read the position size from the table and use it as your order quantity
5. Pair with the SMC Toolkit — entry at an OB/FVG, ATR stop beyond the zone, target the next liquidity pool

**Configuration tips:**
- `Value per 1.0 price move` = 1 for crypto/most stocks; adjust for futures/FX contract value
- Default ATR multiple 1.5 is a starting point — widen on noisy instruments
- TP R-multiples default to 1 / 2 / 3 and are independently toggle-able

**Notes:**
- Sizing assumes the stop is honoured at the planned price; slippage and gaps can increase realized risk
- Part of [SMC Pine Suite](https://github.com/btankutt/smc-pine-suite) on GitHub — full source and more indicators there
- Open source under MPL 2.0

**Disclaimer:**
This is an educational tool, not financial advice. Size conservatively and use proper risk management. Trading involves risk.

---

## 🇹🇷 Türkçe

Stop yerleşimi, hedefler ve pozisyon büyüklüğünü tek ve tutarlı bir hesaplamaya dönüştüren, ATR tabanlı bir işlem-planlama katmanı (tek bir Pine Script v6 göstergesi):

**Özellikler:**
- 🛑 **Dinamik ATR stop** — `ATR × çarpan`, seçilebilir yumuşatma (RMA/SMA/EMA/WMA)
- 🎯 **R-katlı hedefler** — risk mesafesinin katları olarak 3 TP'ye kadar (R:R tasarımca tam)
- 🟥🟩 **Risk / ödül bölgeleri** — gölgeli giriş→stop ve giriş→hedef bantları, fiyat etiketleriyle
- 🧮 **Pozisyon büyüklüğü** — hesap büyüklüğü, risk % ve stop mesafesinden (vadeli/FX için birim-başına-değer input'u ile)
- 🔔 **Alarmlar** — fiyat planlanan stop'u ya da ilk hedefi kesince (Manual giriş fiyatı ayarlayın; "Current close" modunda seviyeler kapanışla birlikte kayar ve asla kesişmez)

**Şu tradeler için tasarlandı:**
- Sabit-pip stop yerine volatiliteye uyarlı stop isteyenler
- Her pozisyonu sabit % hesap riskine boyutlandıranlar
- Girmeden önce giriş/hedefleri görsel planlayanlar

**Pine Script v6 özellikleri:**
- `ta.tr(true)` üzerinde ATR yumuşatma seçimi için `switch`
- Gösterilen R:R'ın tam olması için R-katı matematiği
- `barstate.islast`'ta her yeniden çizimden önce temizlenen tutamaç array'leri
- Sıfır stop mesafesine karşı `na` korumalı boyutlandırma

**Nasıl kullanılır:**
1. Grafiğe ekle
2. Yönü seç; mevcut kapanışı kabul et ya da manuel giriş yaz
3. ATR çarpanını, stop gürültünün ötesine gelecek şekilde ayarla
4. Tablodan pozisyon büyüklüğünü oku ve emir miktarın olarak kullan
5. SMC Toolkit ile eşle — OB/FVG'de giriş, bölgenin ötesinde ATR stop, sonraki likidite havuzunu hedefle

**Konfigürasyon ipuçları:**
- `Value per 1.0 price move` = kripto/çoğu hisse için 1; vadeli/FX kontrat değeri için ayarla
- Varsayılan ATR çarpanı 1.5 bir başlangıç noktasıdır — gürültülü enstrümanlarda genişlet
- TP R-katları varsayılan 1 / 2 / 3'tür ve bağımsız açılıp kapatılır

**Notlar:**
- Boyutlandırma, stop'un planlanan fiyatta uygulandığını varsayar; kayma ve boşluklar gerçekleşen riski artırabilir
- GitHub'daki [SMC Pine Suite](https://github.com/btankutt/smc-pine-suite) paketinin parçasıdır — tam kaynak ve daha fazla gösterge orada
- MPL 2.0 ile açık kaynak

**Sorumluluk reddi:**
Bu eğitim amaçlıdır, finansal tavsiye değildir. Temkinli boyutlandırın ve uygun risk yönetimi kullanın. İşlem yapmak risk içerir.
