# MTF Divergence Scanner — Multi-Timeframe RSI/MACD Divergence

## 🇬🇧 English

Detect regular and hidden divergences on RSI or MACD across up to three timeframes at once, in one Pine Script v6 indicator:

**Features:**
- 📈 **RSI or MACD** — switch oscillators with one input; identical pivot logic for both
- 🔄 **Regular divergence** — reversal signals (price LL / osc HL, and the bearish mirror)
- ➡️ **Hidden divergence** — continuation signals (trend-pullback)
- 🕒 **Up to 3 timeframes** — each with its own on/off and timeframe (blank = chart)
- 🏷️ **On-chart labels + status table** — tagged Reg/Hid and timeframe; table shows the last signal per TF
- 🔔 **3 alerts** — bullish, bearish, or any divergence (any timeframe)

**Built for traders who:**
- Use divergence as a confluence/context tool rather than a standalone trigger
- Want higher-timeframe momentum context without flipping charts
- Need a low-repaint scanner (signals print only on confirmed pivots)

**Pine Script v6 features used:**
- A tuple-returning divergence engine evaluated inside each `request.security` call
- Confirmed pivots (right offset) to suppress repaint
- `var` state inside the engine for swing-to-swing comparison
- A `table` status panel updated on `barstate.islast`

**How to use:**
1. Add to chart
2. Pick RSI or MACD; set your three timeframes
3. Favour low-TF regular divergence aligned with the higher-TF trend
4. Use hidden divergence to add on pullbacks in a trend
5. Combine with the SMC Toolkit — divergence into an OB or after a sweep is a strong entry

**Notes:**
- Signals print once per divergence, on confirmed pivots and closed HTF bars only — labels don't flicker or disappear on refresh
- HTF data uses the confirmed-bar idiom (last closed HTF bar) — no future data is used
- Part of [SMC Pine Suite](https://github.com/btankutt/smc-pine-suite) on GitHub — full source and more indicators there
- Open source under MPL 2.0

**Disclaimer:**
This is an educational tool, not financial advice. A divergence can persist for many bars before price reacts — wait for confirmation and use stops. Trading involves risk.

---

## 🇹🇷 Türkçe

RSI veya MACD üzerinde regular ve hidden uyumsuzlukları, aynı anda üç zaman diliminde tespit eden tek bir Pine Script v6 göstergesi:

**Özellikler:**
- 📈 **RSI veya MACD** — tek input ile osilatör değiştir; ikisi için de aynı pivot mantığı
- 🔄 **Regular uyumsuzluk** — dönüş sinyalleri (fiyat LL / osi HL ve bearish aynası)
- ➡️ **Hidden uyumsuzluk** — devam sinyalleri (trend geri çekilmesi)
- 🕒 **3 zaman dilimine kadar** — her biri kendi aç/kapa ve zaman dilimiyle (boş = grafik)
- 🏷️ **Grafik üstü etiketler + durum tablosu** — Reg/Hid ve zaman dilimi etiketli; tablo TF başına son sinyali gösterir
- 🔔 **3 alarm** — bullish, bearish veya herhangi bir uyumsuzluk (herhangi bir zaman dilimi)

**Şu tradeler için tasarlandı:**
- Uyumsuzluğu tek başına tetikleyici değil, konfluans/bağlam aracı olarak kullananlar
- Grafik değiştirmeden daha yüksek zaman dilimi momentum bağlamı isteyenler
- Düşük-repaint bir tarayıcıya ihtiyaç duyanlar (sinyaller yalnızca onaylı pivot'larda basılır)

**Pine Script v6 özellikleri:**
- Her `request.security` çağrısı içinde değerlendirilen, tuple döndüren uyumsuzluk motoru
- Repaint'i bastırmak için onaylı pivot'lar (sağ ofset)
- Salınımdan salınıma karşılaştırma için motor içinde `var` state
- `barstate.islast`'ta güncellenen bir `table` durum paneli

**Nasıl kullanılır:**
1. Grafiğe ekle
2. RSI veya MACD seç; üç zaman dilimini ayarla
3. Daha yüksek TF trendiyle hizalı düşük-TF regular uyumsuzluğu tercih et
4. Bir trendde geri çekilmelerde eklemek için hidden uyumsuzluğu kullan
5. SMC Toolkit ile birleştir — bir OB içine ya da sweep sonrası uyumsuzluk güçlü bir giriştir

**Notlar:**
- Sinyaller uyumsuzluk başına bir kez, yalnızca onaylı pivot'larda ve kapanmış HTF barlarında basılır — etiketler titremez, yenilemede kaybolmaz
- HTF verisi onaylı-bar desenini kullanır (son kapanmış HTF barı) — gelecek verisi kullanılmaz
- GitHub'daki [SMC Pine Suite](https://github.com/btankutt/smc-pine-suite) paketinin parçasıdır — tam kaynak ve daha fazla gösterge orada
- MPL 2.0 ile açık kaynak

**Sorumluluk reddi:**
Bu eğitim amaçlıdır, finansal tavsiye değildir. Bir uyumsuzluk, fiyat tepki vermeden önce birçok bar sürebilir — onay bekleyin ve stop kullanın. İşlem yapmak risk içerir.
