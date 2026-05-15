# SMC Pine Suite

> Akıllı Para Konseptleri (SMC) trader'ları için üretim sınıfı Pine Script v6 göstergeleri.
> 12+ yıl profesyonel deneyime sahip bir algoritmik ticaret sistemleri geliştiricisi tarafından inşa edildi.

[![Lisans: MPL 2.0](https://img.shields.io/badge/Lisans-MPL_2.0-brightgreen.svg)](https://opensource.org/licenses/MPL-2.0)
[![Pine Script](https://img.shields.io/badge/Pine_Script-v6-2962FF.svg)](https://www.tradingview.com/pine-script-docs/welcome/)
[![TradingView](https://img.shields.io/badge/TradingView-Community-26a69a.svg)](https://www.tradingview.com)

🇬🇧 [English README](README.md)

---

## Genel Bakış

Akıllı Para Konseptleri (SMC) ve modern fiyat hareketi analizine odaklanmış, özenle seçilmiş profesyonel Pine Script v6 göstergeleri koleksiyonu. Her gösterge net görsel çıktı, yapılandırılabilir parametreler ve alarm-hazır mantık ile bağımsız bir araç olarak tasarlanmıştır.

Bu paket, kripto para, forex ve metal piyasaları için üretim trading sistemleri işleterek edinilen gerçek dünya içgörülerini yansıtır. Kod MPL 2.0 altında açık kaynak — fork'la, çalış, stratejine uyarla.

Dört ücretsiz göstergeyi entegre eden daha kapsamlı bir konfluans sistemi için, bkz. [Pro Confluence Engine](pro/README.md) (davetiyeli erişim).

---

## Göstergeler

### 🆓 Ücretsiz (Açık Kaynak)

| Gösterge | Amaç | Durum |
|----------|------|-------|
| [SMC Toolkit](indicators/01-smc-toolkit/) | Order Blocks, Fair Value Gaps (FVG), Likidite Sweep'leri, BoS/CHoCH | 🚧 Yakında |
| [Volume Profile Plus](indicators/02-volume-profile-plus/) | Seans bazlı VP, POC, VAH/VAL, Hacim Düğümleri | 🚧 Yakında |
| [MTF Divergence Scanner](indicators/03-mtf-divergence/) | Çoklu zaman dilimi RSI/MACD ıraksaklık tespiti | 🚧 Yakında |
| [ATR Helper](indicators/04-atr-helper/) | Dinamik SL/TP, R:R görselleştirmesi, pozisyon büyüklüğü | 🚧 Yakında |

### 💎 Pro (Davetiyeli Erişim)

| Gösterge | Amaç | Durum |
|----------|------|-------|
| [Pro Confluence Engine](pro/) | 4 ücretsiz göstergeyi adaptif skorlama ile birleştiren tek elden sinyal sistemi | 🚧 Yakında |

---

## Hızlı Başlangıç

Her gösterge bağımsız bir `.pine` dosyasıdır. Kullanmak için:

1. Bu repodaki herhangi bir `.pine` dosyasının içeriğini kopyala
2. TradingView Pine Editor'ü aç (Grafikler → Pine Editor)
3. Kodu yapıştır, **"Grafiğe ekle"** butonuna tıkla
4. Gösterge ayarlarından parametreleri yapılandır

Her gösterge için detaylı dokümantasyon, ilgili klasör içindeki README'de.

---

## Pine Script v6

Tüm göstergeler Pine Script v6 kullanır — TradingView'in mevcut ana sürümü, Kasım 2024'te yayınlandı. Bu pakette kullanılan temel v6 özellikleri:

- **Dinamik `request.*()`** çoklu sembol/zaman dilimi taraması için
- **Kısa-devre boolean değerlendirme** verimli koşul zincirleri için
- **Kullanıcı tanımlı tipler** temiz state yönetimi için
- **Metodlar (dot notation)** okunabilir array/matrix işlemleri için
- **Yerleşik `log.*()`** grafikleri kirletmeden hata ayıklama için

Hâlâ v5'teyseniz, TradingView'in [resmi v6 geçiş kılavuzu](https://www.tradingview.com/pine-script-docs/migration-guides/to-pine-version-6/)na bakın.

---

## Ticaret Felsefesi

Bu paket birkaç tartışılmaz prensip etrafında inşa edildi:

1. **Geciken göstergeler yerine fiyat hareketi** — önce SMC ve hacim bağlamı
2. **Tek sinyal yerine konfluans** — hiçbir tek gösterge karar vermez; yakınsama verir
3. **Risk yönetimi stratejinin yarısıdır** — her işlemin önceden tanımlı SL/TP'si vardır
4. **Geri test (backtest) zorunludur** — istatistiksel kanıt olmadan canlı işlem yok
5. **Piyasalar evrilir, kod da öyle olmalı** — bu göstergeler versiyonlanır ve güncellenir

Tam doktrin için [docs/trading-philosophy.md](docs/trading-philosophy.md) — bkz.

---

## Yol Haritası

Bu paket için planlananlar:

- [x] Repo yapısı ve dokümantasyon iskeleti
- [ ] SMC Toolkit (Order Blocks + FVG + Likidite Sweep'leri + Yapı)
- [ ] Volume Profile Plus (POC/VAH/VAL ile seans bazlı)
- [ ] MTF Divergence Scanner (Zaman dilimleri arasında RSI/MACD)
- [ ] ATR Helper (Dinamik SL/TP ve R:R görselleştirmesi)
- [ ] Pro Confluence Engine (dördünü birleştirir; davetiyeli erişim)
- [ ] Kapsamlı geri test (backtest) sonuçları ve istatistiksel kanıt
- [ ] Ticaret stratejisi eşlik kılavuzları (gösterge başına)

---

## İlgili Projeler

- [rpi-rfid-access-control](https://github.com/btankutt/rpi-rfid-access-control) — Üretim sınıfı IoT erişim kontrol sistemi (Python + FastAPI + Raspberry Pi)

---

## Lisans

Bu repo **iki lisans** kullanır:

- **MPL 2.0** — `indicators/` içindeki tüm ücretsiz göstergeler (dosya bazlı copyleft)
- **Tescilli (Proprietary)** — `pro/` içindeki Pro Confluence Engine (davetiyeli erişim)

Tam metin için [LICENSE-FREE](LICENSE-FREE) ve [LICENSE-PRO](LICENSE-PRO) — bkz.

---

## Yazar

**Barış Tankut** — Algoritmik Ticaret Sistemleri & IoT Gömülü Mühendis
12+ yıl profesyonel yazılım/donanım geliştirme deneyimi.

- GitHub: [@btankutt](https://github.com/btankutt)
- Aktif olduğu alanlar: Kripto Para · Forex · Metaller · Algoritmik Strateji Geliştirme
- Ticaret sistemleri, Pine Script geliştirme ve IoT entegrasyonu alanlarında danışmanlık & freelance işlere açık

---

## Sorumluluk Reddi

Bu göstergeler **eğitim araçlarıdır**, finansal tavsiye değildir. Geçmiş performans gelecekteki sonuçları garanti etmez. Her zaman:

- Geçmiş veriler üzerinde kapsamlı geri test (backtest) yapın
- Canlı işlem öncesi demo hesaplarda ileri test yapın
- Doğru risk yönetimi kullanın (pozisyon büyüklüğü, stop loss'lar)
- Hiçbir göstergenin trader muhakemesinin yerini tutmayacağını anlayın
