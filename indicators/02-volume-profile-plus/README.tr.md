# Volume Profile Plus

> TradingView için seans bazlı Hacim Profili — POC, Değer Alanı (VAH/VAL) ve HVN/LVN düğümleri, tek bir Pine Script v6 dosyasında.

🇬🇧 [English README](README.md)

---

## Genel Bakış

Yatay hacim histogramı ve klasik market-profile referans seviyelerini çizen bağımsız bir Hacim Profili göstergesi:

- **Kontrol Noktası (POC)** — en çok hacmin işlem gördüğü tek fiyat seviyesi
- **Değer Alanı Üst / Alt (VAH / VAL)** — toplam hacmin yapılandırılabilir bir oranını (varsayılan %70) kapsayan, POC'tan dışa doğru genişleyen fiyat bandı
- **Yüksek / Düşük Hacim Düğümleri (HVN / LVN)** — alışılmadık derecede yoğun veya seyrek katılım gören, renkle vurgulanan fiyat seviyeleri

Profil, daha yüksek bir zaman dilimine sabitlenen bir **seansa** (örn. günlük, haftalık) veya **sabit bir geriye-bakış** penceresine göre hesaplanabilir. Her bara ait hacim, barın high–low aralığının kapsadığı tüm fiyat satırlarına eşit dağıtılır; bu, standart OHLCV verisinden gerçek bir tick-hacim profiline yaklaşır.

Bu gösterge [SMC Pine Suite](../../README.tr.md)'in parçasıdır. Pine Script v6 ile inşa edildi: hacim kovaları için array'ler, çizim tutamaçları için metodlar (dot notation) ve sınırlı döngü maliyeti için `barstate.islast` yeniden hesaplaması.

---

## Özellikler

### 1. Seans veya Sabit-Geriye-Bakış Aralığı

- **Seans** modu, profili `input.timeframe` ile daha yüksek bir zaman dilimine sabitler. Sabitlenen periyot her değiştiğinde (yeni gün, yeni hafta vb.) yeni bir profil başlar.
- **Sabit geriye-bakış** modu, seanstan bağımsız olarak sabit sayıda barı profiller; kripto gibi sürekli piyasalar için kullanışlıdır.

### 2. Kontrol Noktası (POC)

En yüksek birikimli hacme sahip satır. Düz yatay çizgi olarak çizilir ve fiyatıyla etiketlenir. POC, piyasanın "en adil değer" referansıdır ve tekrar ziyaret edildiğinde sıkça destek/direnç görevi görür.

### 3. Değer Alanı (VAH / VAL)

Algoritma POC'tan başlayarak, yapılandırılan hacim yüzdesi yakalanana kadar iki komşu satırdan ağır olanı tekrar tekrar yutar. O bandın üst ve altı VAH ve VAL olur; isteğe bağlı gölgelendirilir.

### 4. Hacim Düğümleri (HVN / LVN)

- **HVN** — HVN eşiğinin (varsayılan POC hacminin %80'i) üstündeki satırlar. Fiyat bunların çevresinde sıkışmaya eğilimlidir.
- **LVN** — LVN eşiğinin (varsayılan %20'si) altındaki satırlar. Fiyat bu "boşluklardan" hızlıca geçme eğilimindedir.

### 5. Alarm

Fiyat en son POC'u kestiğinde tek bir alarm koşulu tetiklenir.

---

## Kurulum

1. TradingView'de herhangi bir grafiği aç
2. **Pine Editor**'ü aç (alt panel)
3. [`volume-profile-plus.pine`](volume-profile-plus.pine) içeriğini kopyala
4. Pine Editor'e yapıştır, **"Kaydet"**, ardından **"Grafiğe ekle"**

---

## Yapılandırma

### Hesaplama
- `Profile range` (varsayılan: Session) — Seans vs Sabit geriye-bakış
- `Session anchor timeframe` (varsayılan: D) — Bir seansı tanımlayan üst zaman dilimi
- `Fixed lookback (bars)` (varsayılan: 200) — Sabit geriye-bakış pencere boyutu
- `Number of rows` (varsayılan: 50) — Fiyat çözünürlüğü; yüksek = daha ince ama daha yavaş
- `Value Area (%)` (varsayılan: 70) — Değer alanının kapsadığı hacim oranı

### Hacim Düğümleri
- `Highlight HVN / LVN` (varsayılan: true)
- `HVN threshold (% of POC volume)` (varsayılan: 80)
- `LVN threshold (% of POC volume)` (varsayılan: 20)

### Görüntü
- `Profile width (bars)` (varsayılan: 80) — Maksimum histogram bar uzunluğu
- `Show POC line`, `Show Value Area`, `Shade Value Area`, `Show price labels`
- Profil gövdesi, değer alanı, HVN, LVN ve POC renkleri

---

## Pine Script v6 Notları

- **Array-tabanlı kovalar** — `array<float>` satır başına hacmi tutar; değer-alanı yürüyüşü ve POC araması basit array taramalarıdır
- **Hacim dağıtımı** — her barın hacmi, sadece kapanışına atanmak yerine low–high arasındaki satırlara eşit bölünür
- **`barstate.islast` yeniden hesaplama** — profil her tarihsel barda değil, her gerçek-zaman güncellemesinde bir kez yeniden inşa edilir
- **Tutamaç array'leri + `clear_drawings()`** — kutular, çizgiler ve etiketler takip edilir ve her yeniden çizimden önce silinir, profiller üst üste yığılmaz

---

## Nasıl Kullanılır

1. **POC**'u seansın adil değeri olarak belirle. Ortalamaya dönüş kurulumları POC'u hedefler; trend kurulumları ondan ret bekler.
2. **VAH/VAL**'ı kabul bölgesinin kenarları olarak gör. Dışarı taştıktan sonra değer alanına geri kapanış klasik bir fade sinyalidir; dışarıda kabul ise devam sinyali.
3. Fiyatın **HVN'lerde duraksamasını**, **LVN'lerden hızlı geçmesini** bekle — hedef koymak ve boşlukları öngörmek için faydalı.
4. [SMC Toolkit](../01-smc-toolkit) ile birleştir — bir POC veya değer-alanı kenarıyla hizalanan Order Block ya da FVG, daha yüksek konfluanslı bir bölgedir.

> ⚠️ Bu bir eğitim aracıdır. Her zaman stratejini backtest et ve uygun pozisyon büyüklüğü kullan.

---

## Performans

- **Derleme süresi:** çoğu grafikte ~1-2 saniye
- **Bellek:** `max_boxes_count=500`, `max_lines_count=500`, `max_labels_count=500` ile sınırlı
- **Repaint:** Canlı seansın profili yeni hacim geldikçe güncellenir (her seans profili için beklenen davranış). Kapanmış seanslar ve sabit-geriye-bakış aralıkları oluştuktan sonra sabittir.

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
