# MTF Divergence Scanner

> TradingView için çoklu zaman dilimi RSI / MACD uyumsuzluk dedektörü — üç zaman diliminde regular ve hidden uyumsuzluklar, tek bir Pine Script v6 dosyasında.

🇬🇧 [English README](README.md)

---

## Genel Bakış

Fiyat salınımlarını bir osilatöre (RSI veya MACD histogramı) karşı karşılaştırıp hem **regular** (dönüş) hem **hidden** (devam) uyumsuzluklarını işaretleyen bağımsız bir uyumsuzluk tarayıcısı. `request.security` ile aynı anda üç zaman dilimini değerlendirir; böylece grafik zaman dilimini izlerken daha yüksek zaman dilimleri arka planda taranır.

Sinyaller **onaylanmış osilatör pivot'larından** türetilir — bir uyumsuzluk yalnızca pivot'u kilitlendiğinde (oluşumundan `piv_right` bar sonra) çizilir. Üst zaman dilimi bayrakları ayrıca yalnızca son **kapanmış** HTF barından okunur ve tüm çıktı onaylı barlarla kapılanır — basılan bir sinyal bar içinde titremez ve grafik yenilemesinden sağ çıkar.

Bu gösterge [SMC Pine Suite](../../README.tr.md)'in parçasıdır. Pine Script v6 ile inşa edildi: tuple döndüren fonksiyonlar, MTF değerlendirmesi için `request.security` ve durum paneli için bir `table`.

---

## Özellikler

### 1. İki Osilatör

- **RSI** — momentum osilatörü; uyumsuzluklar bir hareketin tükenişini işaretler
- **MACD histogramı** — `macd çizgisi − sinyal çizgisi`; histogram üzerindeki uyumsuzluklar genellikle çizginin kendisinden daha erkendir

Tek bir input ile aralarında geçiş yap; pivot mantığı ikisi için de aynıdır.

### 2. Regular vs Hidden Uyumsuzluk

- **Regular bullish** — fiyat daha düşük dip, osilatör daha yüksek dip → olası yukarı dönüş
- **Regular bearish** — fiyat daha yüksek tepe, osilatör daha düşük tepe → olası aşağı dönüş
- **Hidden bullish** — fiyat daha yüksek dip, osilatör daha düşük dip → yükseliş trendinde geri çekilme (devam)
- **Hidden bearish** — fiyat daha düşük tepe, osilatör daha yüksek tepe → düşüş trendinde geri çekilme (devam)

Regular ve hidden bağımsız olarak açılıp kapatılabilir.

### 3. Üç Zaman Dilimine Kadar

Üç zaman dilimi yuvasının her birinde aç/kapa ve bir zaman dilimi seçici vardır. Bir yuvayı boş bırakırsan grafiğin kendi zaman dilimi kullanılır. Varsayılanlar: grafik, 60dk, 240dk.

### 4. Grafik Üstü Etiketler + Durum Tablosu

Tespit edilen uyumsuzluklar barda etiket basar (bullish için altta, bearish için üstte), tür (`Reg`/`Hid`) ve zaman dilimi ile işaretlenir. Sağ üstteki kompakt tablo, zaman dilimi başına en son uyumsuzluk yönünü gösterir.

### 5. Üç Alarm Koşulu

- Bullish uyumsuzluk (herhangi bir zaman dilimi)
- Bearish uyumsuzluk (herhangi bir zaman dilimi)
- Herhangi bir uyumsuzluk (her iki yön, herhangi bir zaman dilimi)

---

## Kurulum

1. TradingView'de herhangi bir grafiği aç
2. **Pine Editor**'ü aç (alt panel)
3. [`mtf-divergence.pine`](mtf-divergence.pine) içeriğini kopyala
4. Pine Editor'e yapıştır, **"Kaydet"**, ardından **"Grafiğe ekle"**

---

## Yapılandırma

### Osilatör
- `Oscillator` (varsayılan: RSI) — RSI veya MACD
- `RSI length` (varsayılan: 14)
- `MACD fast / slow / signal length` (varsayılan: 12 / 26 / 9)

### Pivot'lar
- `Pivot left` (varsayılan: 5) — pivotun solunda gereken bar sayısı
- `Pivot right` (varsayılan: 5) — sağında gereken bar; bu onay gecikmesidir

### Uyumsuzluk Türleri
- `Regular divergence (reversal)` (varsayılan: true)
- `Hidden divergence (continuation)` (varsayılan: false)

### Zaman Dilimleri
- `Timeframe 1 / 2 / 3` — her biri aç/kapa ve zaman dilimi ile (boş = grafik)

### Görüntü
- `Show on-chart labels`, `Show status table`
- Bullish / bearish renkleri

---

## Pine Script v6 Notları

- **Tuple döndüren motor** — `calc_div()` fonksiyonu `[regular_bull, regular_bear, hidden_bull, hidden_bear]` döndürür ve her `request.security` çağrısı içinde değerlendirilir; böylece tüm pivot matematiği hedef zaman diliminin bağlamında çalışır
- **Yalnızca onaylı pivot'lar** — sağ ofsetli `ta.pivothigh`/`ta.pivotlow`, sinyallerin oluşan barda değil onaydan sonra belirmesini sağlar, repaint'i bastırır
- **Fonksiyon içinde `var` state** — önceki pivot fiyatı ve osilatör değerleri, salınımdan salınıma karşılaştırma için güvenlik bağlamı başına saklanır
- **`table` durum paneli** — tek bir kalıcı tablo `barstate.islast`'ta güncellenir

---

## Nasıl Kullanılır

1. İşlem zaman dilimini grafik olarak ayarla, bağlam için iki daha yüksek zaman dilimi seç.
2. **Düşük zaman dilimi regular uyumsuzluğunun daha yüksek zaman dilimi trendiyle hizalandığı** sinyalleri tercih et — örn. 4H yükselişteyken grafikte regular bullish uyumsuzluk.
3. **Hidden uyumsuzluğu**, tepe/dip aramak yerine trend pozisyonlarına geri çekilmelerde ekleme yapmak için kullan.
4. [SMC Toolkit](../01-smc-toolkit) ile birleştir: bir Order Block içine ya da likidite sweep'ine giren regular uyumsuzluk, güçlü bir konfluans girişidir.

> ⚠️ Uyumsuzluk bir bağlam aracıdır, tek başına tetikleyici değil. Bir uyumsuzluk, fiyat tepki vermeden önce birçok bar sürebilir. Her zaman bir fiyat-aksiyonu onayı bekle ve stop kullan.

---

## Repaint Notları

- Sinyaller **onaylı pivot'lara** dayanır (pivottan `piv_right` kapanmış bar sonra) — uyumsuzluklar yalnızca kilitlenmiş salınımlar üzerinden ölçülür.
- Üst zaman dilimi bayrakları **onaylı-bar desenini** kullanır (`expr[1]` + `lookahead_on`): her grafik barı, son **kapanmış** HTF barının sinyalini görür — geçmiş ve canlı barlarda birebir aynı; yenilemede hiçbir şey kaymaz ya da kaybolmaz. Gelecek verisi kullanılmaz.
- Etiketler, tablo durumu ve alarm bayrakları `barstate.isconfirmed` ile kapılanır ve her sinyalin **yükselen kenarına** indirgenir — uyumsuzluk başına bir etiket, bir alarm; bar-içi hayalet sinyal yok.
- Zaman dilimi slotlarında grafiğin kendi zaman dilimini veya **daha yükseğini** kullanın; grafikten düşük zaman dilimleri `request.security` ile güvenilir taranamaz — bu slotlar nötralize edilir ve durum tablosunda `(low TF)` olarak işaretlenir.

---

## Lisans

Bu gösterge **Mozilla Public License 2.0** (MPL 2.0) altında açık kaynaktır. Tam metin için [LICENSE-FREE](../../LICENSE-FREE).

---

## Sorumluluk Reddi

Bu gösterge **olduğu gibi** sağlanır, kârlılık veya doğruluk garantisi yoktur. Her zaman geçmiş veride backtest yap, demo hesapta ileri test yap ve hesabına uygun pozisyon büyüklüğü ile stop-loss kullan. İşlem yapmak risk içerir. Geçmiş performans gelecekteki sonuçları garanti etmez.

---

## Yazar

**Barış Tankut** ([@btankutt](https://github.com/btankutt))
Algoritmik Ticaret Sistemleri & IoT Gömülü Mühendis

[SMC Pine Suite](../../README.tr.md)'in parçası — üretim sınıfı Pine Script v6 göstergeleri.
