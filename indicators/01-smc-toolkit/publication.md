# SMC Toolkit — Smart Money Concepts All-in-One

## 🇬🇧 English

A clean, modern Pine Script v6 implementation of standard Smart Money Concepts in a single indicator:

**Features:**
- 📊 **Market structure** — BoS (Break of Structure) and CHoCH (Change of Character) labels at structural breaks
- 🟩 **Order Blocks** — last opposite-color candle before BoS, with mitigation tracking and optional volume filter
- 🔷 **Fair Value Gaps** — 3-candle gap detection with ATR-scaled size filter; filled gaps auto-marked
- 〰️ **Liquidity levels** — equal highs/lows within ATR tolerance form BSL/SSL pools, with sweep alerts
- 🔔 **6 alert conditions** — BoS, CHoCH, and liquidity sweeps (both directions)

**Built for traders who:**
- Use SMC frameworks (Inner Circle Trader, ICT, etc.) and want everything in one indicator
- Need clean visuals (mitigated zones turn gray, capped display counts)
- Trade across timeframes (works on any timeframe from 1M to 1W)
- Want a non-repainting tool (uses confirmed pivots + time-based coordinates)

**Pine Script v6 features used:**
- User-defined types for clean state management
- Time-based xloc for zoom-stable drawings
- Dot-notation methods for readability
- Strict typing throughout

**How to use:**
1. Add to chart
2. Configure inputs (5 groups: Structure, Order Blocks, FVG, Liquidity, Display)
3. Wait for structural breaks (BoS/CHoCH labels appear)
4. Look for confluence: OB + FVG + Liquidity at the same level
5. Set alerts on the events that matter to you

**Configuration tips:**
- For 1H+ timeframes, default `swing_length = 5` works well
- For 15M and below, reduce to 3
- `FVG min size` controls how many FVGs you see — lower it if FVGs are missing
- All features can be toggled independently

**Notes:**
- Pivots have a `swing_length` bar confirmation delay (required to avoid lookahead bias)
- This is part of [SMC Pine Suite](https://github.com/btankutt/smc-pine-suite) on GitHub — full source, screenshots, and additional indicators available there
- Open source under MPL 2.0

**Disclaimer:**
This is an educational tool, not financial advice. Smart Money Concepts are interpretive — backtest your strategy and use proper risk management. Trading involves risk.

---

## 🇹🇷 Türkçe

Standart Akıllı Para Konseptleri (SMC)'nin tek bir göstergede modern Pine Script v6 implementasyonu:

**Özellikler:**
- 📊 **Piyasa yapısı** — BoS (Yapı Kırılımı) ve CHoCH (Karakter Değişimi) etiketleri
- 🟩 **Order Blocks** — BoS öncesi son ters renkli mum, mitigasyon takibi ve isteğe bağlı hacim filtresi
- 🔷 **Fair Value Gaps** — 3-mumlu gap tespiti, ATR-ölçekli boyut filtresi; dolan FVG'ler otomatik işaretlenir
- 〰️ **Likidite seviyeleri** — ATR toleransı içinde eşit highs/lows BSL/SSL havuzları oluşturur, sweep alarmları
- 🔔 **6 alarm koşulu** — BoS, CHoCH ve likidite sweep'leri (her iki yön)

**Şu tradeler için tasarlandı:**
- SMC çerçevelerini kullananlar (Inner Circle Trader, ICT, vb.) ve tek göstergede her şeyi isteyenler
- Temiz görsele ihtiyaç duyanlar (mitige edilen bölgeler gri olur, gösterim sayısı sınırlı)
- Çoklu zaman dilimlerinde işlem yapanlar (1D'den 1W'a kadar)
- Repaint etmeyen bir araç isteyenler (onaylı pivot'lar + zaman-tabanlı koordinatlar kullanır)

**Pine Script v6 özellikleri:**
- Temiz state yönetimi için user-defined types
- Zoom-stable çizimler için time-based xloc
- Okunabilirlik için dot-notation methodları
- Strict typing

**Nasıl kullanılır:**
1. Grafiğe ekle
2. Inputs'u yapılandır (5 grup: Yapı, Order Blocks, FVG, Likidite, Görüntü)
3. Yapısal kırılımları bekle (BoS/CHoCH etiketleri belirir)
4. Konfluans ara: aynı seviyede OB + FVG + Likidite
5. Önemli olduğunu düşündüğün eventlere alarm kur

**Konfigürasyon ipuçları:**
- 1H ve üzeri için varsayılan `swing_length = 5` iyi çalışır
- 15M ve altı için 3'e düşür
- `FVG min size` kaç FVG göreceğini kontrol eder — eksikse düşür
- Tüm özellikler bağımsız kapatılıp açılabilir

**Notlar:**
- Pivot'lar `swing_length` bar onay gecikmesine sahiptir (lookahead bias'ı önlemek için gerekli)
- Bu, GitHub'daki [SMC Pine Suite](https://github.com/btankutt/smc-pine-suite) paketinin parçasıdır — tam kaynak kod, ekran görüntüleri ve ek göstergeler orada
- MPL 2.0 ile açık kaynak

**Sorumluluk reddi:**
Bu eğitim amaçlıdır, finansal tavsiye değildir. Akıllı Para Konseptleri yorumlamaya açıktır — stratejinizi backtest edin ve uygun risk yönetimi kullanın. İşlem yapmak risk içerir.
