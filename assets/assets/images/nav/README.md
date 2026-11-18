# Bottom nav görselleri

| Dosya | Kullanım |
|---|---|
| `mac-topu.webp` | MAÇ sekmesinin vurgulu topu (512×512, şeffaf; ekranda 66 dp, decode `cacheWidth` ile ≈66×DPR) |
| `ikon-ana-sayfa.webp` | Ana Sayfa sekmesi (256×256 alfa, ~9 KB) |
| `ikon-takim.webp` | Takım sekmesi |
| `ikon-transfer.webp` | Transfer sekmesi |
| `ikon-yonetim.webp` | Yönetim sekmesi |

**Dört sekme ikonu — v2 (2026-11-18, İskender/Gemini):** açık tonlu, yere
basan 3B set (krem gövde, lacivert ayrıntı, tek altın vurgu): kulüp evi · standda
forma · sözleşme+kalem+mühür · evrak çantası. Dördü aynı açıda; 256×256 alfa
WebP (kalite 90, 7–13 KB). Üretim: 1024 kaynak → alfa kenarında magenta saçağı
bastırıldı → içeriğe kırpıldı → TEK ortak ölçekle kare tuvale, ortak taban
çizgisi (alt kenar 15 px, ≈ %6 boşluk). Eski 3B set (2026-10-21) çerçevesizdi
(`AnaSayfaIkon`, 36 dp kutu, ≈ 28 dp çizim; rozet 10-22'de kalktı); çerçevesiz
kullanım aynen sürer. Tek durumlu görsel → pasif sekme %80 opaklık + %80
doygunluk, aktif tam renk — kural yeni sette de uygun (kare alındı, pasif/aktif
ayrımı okunuyor). KONTRAST (`chromeBottom` zemini, pasif süzgeçle, ölçüm
2026-11-18): gövde medyan kontrastı eski set 1,1–1,3:1 (üç ikon lacivert
ağırlıklıydı, piksellerin %53–62'si koyu; yalnız transfer 5,0:1) → yeni set
3,4–6,9:1 (ana-sayfa 3,4 · takım 6,9 · transfer 6,8 · yönetim 4,2); açık gövde
koyu zeminde silueti taşır. Lacivert ayrıntılar zeminle yakın kalır (düşük
persentil ≈ 1,1:1) — ayrıntı, siluet değil. Kod:
`lib/core/ui/cosmos_bottom_nav.dart` (`_tabAssets`); bekçi:
`test/alt_nav_ana_sayfa_ikonu_test.dart`.

**Top nereden geliyor (2026-11-18, İskender «Tasarım A»):** Gemini üretimi gerçekçi
deri top; beşgen mavi panelde logo + kavisli SEZONO yazısı, turkuaz kenar ışığı; kraliyet mavisi orta panelde RESMİ logo (beyaz figür, altın kupa, ayakta
siyah-beyaz top) uygulama ikonundan (`assets/brand/android_legacy_icon.png`)
referansla alındı. Kaynak 1024 PNG → magenta arka plan temizlendi → daire kırpım →
512 px WebP (~65 KB). Eski Midjourney kompoziti (turkuaz dikişli panelli top +
sezono_mark bindirmesi, 192 px) yerine geçti; logo artık kodla basılmaz.

Boyut kararı: 4 varyant (52/58/66/74dp) gerçek Flutter render'ıyla
karşılaştırıldı, **C = 66dp / 28dp taşma** onaylandı. Şerit 64dp SABİT —
taşan kısım `Clip.none` ile şeridin dışına çizilir, nav'ın yüksekliğini
BÜYÜTMEZ (2026-07-23 kavisli nav bug'ı geri gelmesin).

Bekçi: `test/mac_sekmesi_test.dart`.
