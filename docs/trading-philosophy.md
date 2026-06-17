# Trading Philosophy

> The doctrine behind SMC Pine Suite. Every indicator in this repository is built to serve these principles — not the other way around.

🇹🇷 Türkçe çeviri bu dosyanın [ikinci yarısındadır](#ticaret-felsefesi-türkçe).

---

## Why a philosophy at all?

Indicators are tools, and tools encode assumptions. A moving-average crossover assumes trends persist; an oscillator assumes mean reversion. When you stack tools without a coherent worldview, they contradict each other and you end up curve-fitting to noise.

This suite starts from a single premise: **price moves to find liquidity, and the footprints of that search are readable.** Smart Money Concepts (SMC), volume profile, and momentum divergence are three lenses on the same process. The indicators here are deliberately narrow so that each lens stays clean, and the [Pro Confluence Engine](../pro/README.md) is the layer that combines them.

---

## The five principles

### 1. Price action over lagging indicators

Structure, order flow, and volume come first. A 50-period moving average tells you where price *was*; a break of structure tells you what price is *doing now*. Lagging indicators are used only as context (e.g. a higher-timeframe trend filter), never as a primary trigger.

**In the code:** the SMC Toolkit detects structure from confirmed pivots, the Volume Profile reads actual traded volume per price, and the MTF scanner reads momentum *relative to price* rather than in isolation.

### 2. Confluence over single signals

No single indicator decides a trade. A break of structure is interesting; a break of structure *into an unmitigated order block that also sits at a volume Point of Control* is a setup. Convergence of independent signals is what shifts probability.

**In the code:** every free indicator is standalone and toggle-able so you can layer them deliberately. The Pro Confluence Engine formalises this — it scores six independent modules and only signals when enough of them agree, scaled by higher-timeframe alignment.

### 3. Risk management is half the strategy

Entries get the attention; exits and sizing decide the equity curve. Every trade must have a pre-defined invalidation level and position size *before* it is taken. A great entry with no plan is a gamble.

**In the code:** the ATR Helper exists for exactly this — it derives a volatility-adjusted stop, projects targets as fixed R-multiples, and computes the position size that keeps every loss the same fraction of the account. Risk is treated as a first-class input, not an afterthought.

### 4. Backtesting is mandatory

No live capital without statistical evidence. A setup that "looks good" on a chart is a hypothesis, not an edge. Edges are measured across hundreds of occurrences, in and out of sample, with realistic costs.

**In practice:** treat these indicators as the *inputs* to a tested strategy, not as the strategy itself. Forward-test in a demo account before risking real money. The roadmap includes publishing backtest methodology and results so claims can be checked, not just asserted.

### 5. Markets evolve, code should too

Regimes change. A tool tuned for 2021 crypto volatility behaves differently in a quiet range. Indicators here are versioned, documented, and updated — and their parameters are exposed precisely so you can adapt them to the instrument and timeframe you actually trade.

**In the code:** every indicator carries a version header, every parameter is an input with sensible defaults and tooltips, and changes are tracked so you can reason about what shifted between versions.

---

## How the pieces fit together

A representative workflow that respects all five principles:

1. **Bias** — read higher-timeframe market structure (SMC Toolkit) and the trend filter. Decide long-only, short-only, or stand aside.
2. **Location** — wait for price to reach a high-value zone: an unmitigated order block or fair value gap, ideally aligned with a volume Point of Control or value-area edge (Volume Profile Plus).
3. **Trigger** — look for a confirmation: a liquidity sweep, a change of character, or a momentum divergence (MTF Divergence Scanner).
4. **Risk** — define the stop beyond the zone and size the position to a fixed account risk (ATR Helper). If the R-multiple to the next liquidity target is poor, skip the trade.
5. **Review** — log the outcome against the plan, not the result. A losing trade taken correctly is a good trade; a winning trade taken on a whim is not.

The [Pro Confluence Engine](../pro/README.md) automates steps 1–3 into a single score, but the discipline of steps 4–5 is always the trader's.

---

## What this philosophy is *not*

- It is **not** a promise of profit. Confluence improves probability; it does not remove risk.
- It is **not** a black box. Every concept the Pro engine scores is implemented openly in the free indicators so you can audit the logic.
- It is **not** financial advice. These are educational tools for traders who do their own analysis and manage their own risk.

---

<a name="ticaret-felsefesi-türkçe"></a>

# Ticaret Felsefesi (Türkçe)

> SMC Pine Suite'in arkasındaki doktrin. Bu repodaki her gösterge bu ilkelere hizmet etmek için inşa edildi — tersi değil.

## Neden bir felsefe?

Göstergeler araçtır ve araçlar varsayımları kodlar. Ortalama kesişimi trendlerin süreceğini varsayar; osilatör ortalamaya dönüşü varsayar. Tutarlı bir bakış açısı olmadan araçları üst üste yığarsanız, birbirleriyle çelişir ve gürültüye aşırı uyum (curve-fitting) yaparsınız.

Bu paket tek bir önermeden başlar: **fiyat likidite aramak için hareket eder ve bu aramanın ayak izleri okunabilir.** Akıllı Para Konseptleri (SMC), hacim profili ve momentum uyumsuzluğu aynı sürecin üç merceğidir. Buradaki göstergeler bilerek dardır ki her mercek temiz kalsın; [Pro Confluence Engine](../pro/README.md) ise bunları birleştiren katmandır.

## Beş ilke

### 1. Geciken göstergeler yerine fiyat hareketi
Yapı, emir akışı ve hacim önce gelir. 50-periyot ortalama fiyatın *nerede olduğunu* söyler; yapı kırılımı fiyatın *şu an ne yaptığını* söyler. Geciken göstergeler yalnızca bağlam olarak kullanılır, asıl tetikleyici olarak değil.

### 2. Tek sinyal yerine konfluans
Hiçbir tek gösterge işleme karar vermez. Bir yapı kırılımı ilginçtir; *mitige olmamış bir order block'a girip aynı zamanda hacim Kontrol Noktası'nda (POC) duran* bir yapı kırılımı ise bir kurulumdur. Bağımsız sinyallerin yakınsaması olasılığı kaydırır.

### 3. Risk yönetimi stratejinin yarısıdır
Girişler ilgi görür; çıkışlar ve boyutlandırma sermaye eğrisini belirler. Her işlemin, alınmadan *önce* tanımlı bir geçersizlik (invalidation) seviyesi ve pozisyon büyüklüğü olmalıdır. Planı olmayan harika bir giriş kumardır. ATR Helper tam da bunun için vardır.

### 4. Geri test (backtest) zorunludur
İstatistiksel kanıt olmadan canlı sermaye yok. "İyi görünen" bir kurulum bir hipotezdir, bir edge değil. Edge'ler yüzlerce örnek üzerinde, örneklem içi ve dışı, gerçekçi maliyetlerle ölçülür. Bu göstergeleri test edilmiş bir stratejinin *girdileri* olarak görün, stratejinin kendisi olarak değil.

### 5. Piyasalar evrilir, kod da öyle olmalı
Rejimler değişir. Göstergeler versiyonlanır, dokümante edilir ve güncellenir; parametreleri tam da işlem yaptığınız enstrüman ve zaman dilimine uyarlayabilmeniz için açıktır.

## Parçalar nasıl birleşir

1. **Önyargı (Bias)** — üst zaman dilimi yapısını oku (SMC Toolkit) ve trend filtresini uygula.
2. **Konum** — fiyatın yüksek-değerli bir bölgeye gelmesini bekle: mitige olmamış bir OB veya FVG, ideal olarak bir POC / değer-alanı kenarıyla hizalı (Volume Profile Plus).
3. **Tetikleyici** — bir onay ara: likidite sweep'i, karakter değişimi (CHoCH) veya momentum uyumsuzluğu (MTF Divergence Scanner).
4. **Risk** — stop'u bölgenin ötesine koy ve pozisyonu sabit hesap riskine boyutlandır (ATR Helper). Sonraki likidite hedefine R-katı kötüyse işlemi atla.
5. **Gözden geçirme** — sonucu değil, planı esas alarak kaydet. Doğru alınmış zararlı bir işlem iyi bir işlemdir; keyfi alınmış kârlı bir işlem değildir.

## Bu felsefe *ne değildir*

- Kâr **vaadi değildir**. Konfluans olasılığı iyileştirir; riski ortadan kaldırmaz.
- Bir kara kutu **değildir**. Pro motorunun skorladığı her konsept ücretsiz göstergelerde açıkça uygulanmıştır.
- Finansal tavsiye **değildir**. Bunlar, kendi analizini yapan ve kendi riskini yöneten trader'lar için eğitim araçlarıdır.
