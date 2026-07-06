# Volume Profile Plus — Session POC, Value Area & Volume Nodes

## 🇬🇧 English

A clean Pine Script v6 Volume Profile with the classic market-profile reference levels in one indicator:

**Features:**
- 📊 **Volume histogram** — horizontal volume distribution across price bins, recomputed on the latest bar
- 🎯 **Point of Control (POC)** — the single highest-volume price level, drawn and labelled
- 🟦 **Value Area (VAH/VAL)** — the configurable % of volume (default 70%) expanded outward from the POC
- 🟩 **HVN / 🟥 LVN** — high and low volume nodes highlighted, so you can see where price stalls vs travels fast
- 🔔 **Alert** — fires when price crosses the current profile's POC (live only; suppressed on session rollover, where the POC relocates)

**Built for traders who:**
- Trade auction/market-profile concepts and want value-area context on any chart
- Use crypto/forex (Fixed lookback) or futures/indices (Session anchor)
- Want a fair-value reference to pair with SMC zones

**Two calculation modes:**
- **Session** — anchored to a higher timeframe (daily, weekly, …); a fresh profile each period
- **Fixed lookback** — a constant N-bar window for continuous markets

**Pine Script v6 features used:**
- Array-backed volume bins with simple scans for POC and value area
- Volume distributed across every row a bar's range spans
- `barstate.islast` recompute to keep nested loops cheap
- Handle arrays cleared before each redraw (no stacked profiles)

**How to use:**
1. Add to chart
2. Pick Session or Fixed lookback, set rows and Value Area %
3. Read the POC as fair value; VAH/VAL as the edges of acceptance
4. Expect price to stall at HVNs and move quickly through LVNs
5. Combine with the SMC Toolkit — an OB/FVG at a POC is higher confluence

**Notes:**
- The live session's profile updates as new volume arrives (expected for any session profile)
- Part of [SMC Pine Suite](https://github.com/btankutt/smc-pine-suite) on GitHub — full source and more indicators there
- Open source under MPL 2.0

**Disclaimer:**
This is an educational tool, not financial advice. Backtest your strategy and use proper risk management. Trading involves risk.

---

## 🇹🇷 Türkçe

Klasik market-profile referans seviyelerini tek bir göstergede toplayan, temiz bir Pine Script v6 Hacim Profili:

**Özellikler:**
- 📊 **Hacim histogramı** — fiyat kovalarına yatay hacim dağılımı, en son barda yeniden hesaplanır
- 🎯 **Kontrol Noktası (POC)** — en yüksek hacimli tek fiyat seviyesi, çizilir ve etiketlenir
- 🟦 **Değer Alanı (VAH/VAL)** — POC'tan dışa genişleyen, yapılandırılabilir hacim oranı (varsayılan %70)
- 🟩 **HVN / 🟥 LVN** — yüksek ve düşük hacim düğümleri vurgulanır; fiyatın nerede duraksayıp nerede hızlı geçtiğini görürsün
- 🔔 **Alarm** — fiyat mevcut profilin POC'unu kesince tetiklenir (yalnızca canlı; POC'un yer değiştirdiği seans devrinde bastırılır)

**Şu tradeler için tasarlandı:**
- Auction/market-profile konseptleriyle işlem yapan ve her grafikte değer-alanı bağlamı isteyenler
- Kripto/forex (Sabit geriye-bakış) veya vadeli/endeks (Seans sabiti) kullananlar
- SMC bölgeleriyle eşleştirilecek bir adil-değer referansı isteyenler

**İki hesaplama modu:**
- **Seans** — daha yüksek bir zaman dilimine sabitlenir (günlük, haftalık, …); her periyotta yeni profil
- **Sabit geriye-bakış** — sürekli piyasalar için sabit N-bar penceresi

**Pine Script v6 özellikleri:**
- POC ve değer alanı için basit taramalı, array-tabanlı hacim kovaları
- Her barın hacmi, aralığının kapsadığı tüm satırlara dağıtılır
- İç içe döngüleri ucuz tutmak için `barstate.islast` yeniden hesaplama
- Her yeniden çizimden önce temizlenen tutamaç array'leri (üst üste profil yok)

**Nasıl kullanılır:**
1. Grafiğe ekle
2. Seans veya Sabit geriye-bakış seç, satır sayısı ve Değer Alanı %'sini ayarla
3. POC'u adil değer, VAH/VAL'ı kabul kenarları olarak oku
4. Fiyatın HVN'lerde duraksamasını, LVN'lerden hızlı geçmesini bekle
5. SMC Toolkit ile birleştir — POC üzerindeki bir OB/FVG daha yüksek konfluans

**Notlar:**
- Canlı seansın profili yeni hacim geldikçe güncellenir (her seans profili için beklenen)
- GitHub'daki [SMC Pine Suite](https://github.com/btankutt/smc-pine-suite) paketinin parçasıdır — tam kaynak ve daha fazla gösterge orada
- MPL 2.0 ile açık kaynak

**Sorumluluk reddi:**
Bu eğitim amaçlıdır, finansal tavsiye değildir. Stratejinizi backtest edin ve uygun risk yönetimi kullanın. İşlem yapmak risk içerir.
