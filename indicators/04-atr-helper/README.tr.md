# ATR Helper

> TradingView için ATR tabanlı işlem planlama aracı — dinamik stop-loss, R-katlı hedefler, risk/ödül bölgeleri ve pozisyon büyüklüğü, tek bir Pine Script v6 dosyasında.

🇬🇧 [English README](README.md)

---

## Genel Bakış

Bağımsız bir işlem-planlama katmanı (overlay). Bir yön ve giriş belirlersin; script bir ATR çarpanından volatiliteye uyarlı bir **stop-loss** türetir, risk mesafesinin katları (R katları) olarak üç **take-profit** hedefi projekte eder, **risk ve ödül bölgelerini** gölgelendirir ve stop tetiklenirse zararı hesabın sabit bir yüzdesinde tutacak **pozisyon büyüklüğünü** hesaplar.

Bu, her işlemin en zor üç parçasını — stop nereye, hedefler nereye, pozisyon ne kadar büyük olmalı — tek ve tutarlı, ATR-tabanlı bir hesaplamaya dönüştürür.

Bu gösterge [SMC Pine Suite](../../README.tr.md)'in parçasıdır. Pine Script v6 ile inşa edildi: ATR yumuşatma seçimi için `switch`, temiz yeniden çizimler için tutamaç array'leri ve işlem özeti için bir `table`.

---

## Özellikler

### 1. Dinamik ATR Stop

Stop mesafesi `ATR × çarpan`'dır; volatil koşullarda genişler, sakin koşullarda daralır. ATR yumuşatma seçilebilir (RMA, SMA, EMA, WMA).

### 2. R-Katlı Hedefler

Her take-profit, sabit bir fiyat değil, risk mesafesinin bir katı olarak tanımlanır. 2R hedefi, enstrüman veya volatiliteden bağımsız olarak stop'tan her zaman girişin iki katı uzaktadır — yani R:R tasarımca sabittir (varsayılan TP1 = 1R, TP2 = 2R, TP3 = 3R, hepsi ayarlanabilir).

### 3. Risk / Ödül Görselleştirmesi

Giriş-stop bandı kırmızı, giriş-en uzak hedef bandı yeşil gölgelendirilir; giriş, stop ve etkin her hedef için yatay çizgiler ve fiyat etiketleri çizilir.

### 4. Pozisyon Büyüklüğü

`hesap büyüklüğü`, `işlem başına risk (%)` ve stop mesafesinden, stop'ta seçilen yüzdeyi tam riske eden pozisyon büyüklüğünü hesaplar:

```
risk tutarı     = hesap × risk%
birim başına risk = stop mesafesi × birim-başına-değer
pozisyon büyüklüğü = risk tutarı ÷ birim başına risk
```

`Value per 1.0 price move` input'u, bir fiyat biriminin bir hesap-para-birimi olmadığı enstrümanları (vadeli, FX) yönetir. Kripto ve çoğu hisse için 1'de bırak.

### 5. Özet Tablo + Alarmlar

Sağ alttaki tablo ATR, giriş, stop, risk mesafesi, R:R, risk tutarı ve pozisyon büyüklüğünü listeler. Fiyat planlanan stop'u veya ilk hedefi kestiğinde alarmlar tetiklenir.

---

## Kurulum

1. TradingView'de herhangi bir grafiği aç
2. **Pine Editor**'ü aç (alt panel)
3. [`atr-helper.pine`](atr-helper.pine) içeriğini kopyala
4. Pine Editor'e yapıştır, **"Kaydet"**, ardından **"Grafiğe ekle"**

---

## Yapılandırma

### ATR
- `ATR length` (varsayılan: 14)
- `ATR smoothing` (varsayılan: RMA) — RMA / SMA / EMA / WMA
- `Stop-loss ATR multiple` (varsayılan: 1.5)

### İşlem Kurulumu
- `Direction` (varsayılan: Long) — Long veya Short
- `Entry price` (varsayılan: Current close) — Current close veya Manual
- `Manual entry price` — Entry price = Manual olduğunda kullanılır

### Take Profit (R katları)
- `TP1 / TP2 / TP3` — her biri aç/kapa ve bir R katı ile (varsayılan 1 / 2 / 3)

### Pozisyon Büyüklüğü
- `Show position sizing` (varsayılan: true)
- `Account size` (varsayılan: 10000)
- `Risk per trade (%)` (varsayılan: 1.0)
- `Value per 1.0 price move (per unit)` (varsayılan: 1.0)

### Görüntü
- `Extend lines (bars)` (varsayılan: 40)
- `Show summary table`, renkler ve `Zone transparency`

---

## Pine Script v6 Notları

- **Yumuşatma için `switch`** — ATR yumuşatma yöntemi `ta.tr(true)` üzerinde bir `switch` ile seçilir
- **R-katı matematiği** — hedefler stop mesafesinden türetilir, böylece gösterilen R:R yapısı gereği tamdır
- **Tutamaç array'leri + `clear_plan()`** — çizgiler, kutular ve etiketler takip edilir ve `barstate.islast`'ta her yeniden çizimden önce silinir
- **Bölme koruması** — pozisyon büyüklüğü, sıfır stop mesafesine karşı `na` ile korunur, sıfıra bölme önlenir

---

## Nasıl Kullanılır

1. **Yönünü** seç ve ya mevcut kapanışı giriş kabul et ya da işlem yapmayı düşündüğün seviyeye **manuel giriş** yaz.
2. **ATR çarpanını**, stop gürültünün ötesine — yakın bir swing'in ya da Order Block'un dışına, içine değil — gelecek şekilde ayarla.
3. Tablodaki **pozisyon büyüklüğünü** oku ve emir miktarın olarak kullan; her zararı hesabın aynı oranında tutan budur.
4. [SMC Toolkit](../01-smc-toolkit) ile eşle: girişi bir Order Block / FVG'ye koy, ATR stop'u bölgenin ötesine ayarla ve R hedefleriyle bir sonraki likidite havuzunu hedefle.

> ⚠️ Pozisyon büyüklüğü, stop'un planlanan fiyatta uygulandığını varsayar. Kayma (slippage), boşluklar ve ücretler gerçekleşen riskin planlanandan fazla olabileceği anlamına gelir. Temkinli boyutlandır.

---

## Lisans

Bu gösterge **Mozilla Public License 2.0** (MPL 2.0) altında açık kaynaktır. Tam metin için [LICENSE-FREE](../../LICENSE-FREE).

---

## Sorumluluk Reddi

Bu gösterge **olduğu gibi** sağlanır, kârlılık veya doğruluk garantisi yoktur. Buradaki hiçbir şey finansal tavsiye değildir. Her zaman geçmiş veride backtest yap, demo hesapta ileri test yap ve hesabına uygun pozisyon büyüklüğü ile stop-loss kullan. İşlem yapmak risk içerir. Geçmiş performans gelecekteki sonuçları garanti etmez.

---

## Yazar

**Barış Tankut** ([@btankutt](https://github.com/btankutt))
Algoritmik Ticaret Sistemleri & IoT Gömülü Mühendis

[SMC Pine Suite](../../README.tr.md)'in parçası — üretim sınıfı Pine Script v6 göstergeleri.
