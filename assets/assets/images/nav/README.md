# Bottom nav görselleri

| Dosya | Kullanım |
|---|---|
| `mac-topu.webp` | MAÇ sekmesinin vurgulu topu (192×192, şeffaf) |
| `ikon-ana-sayfa.webp` | Ana Sayfa sekmesi (256×256 alfa, ~11 KB) |
| `ikon-takim.webp` | Takım sekmesi |
| `ikon-transfer.webp` | Transfer sekmesi |
| `ikon-yonetim.webp` | Yönetim sekmesi |

**Dört sekme ikonu (2026-10-21, İskender):** Gemini'nin tek stilli 3B seti;
eski lucide çizgi / çift tonlu SVG ikonların yerine geçti. 2026-10-22'den beri
ÇERÇEVESİZ (`AnaSayfaIkon`, 36 dp kutu, ≈ 28 dp çizim; rozet kalktı). 3B görsel
tek durumlu → pasif sekme %80 opaklık + %80 doygunluk (rozetle %55/%60'tı), aktif
tam renk. ⚠️ `ikon-ana-sayfa`, `ikon-takim`, `ikon-yonetim` lacivert ağırlıklı
(piksellerin %51–62'si koyu): `chromeBottom` üstünde siluet kenarı kontrastı
pasifte 2,5–3,0:1 — açık tonlu / konturu GÖMÜLÜ yeni varlık beklenir (kontur kodla
çizilmez). Kod:
`lib/core/ui/cosmos_bottom_nav.dart` (`_tabAssets`); bekçi:
`test/alt_nav_ana_sayfa_ikonu_test.dart`.

**Top nereden geliyor:** İskender'in Midjourney karesi (modern panelli top,
turkuaz dikişler) + `assets/brand/sezono_mark.png` bindirmesi. İmza kompoziti
kod dışında üretildi (küresel sarma + multiply); kaynak zincir:
Midjourney karesi → canlandırma (panel parlatma + dikişleri #4FE3E0'e çekme)
→ SEZONO işareti/yazısı küresel eğrilikle orta panele → daire kırpım → 192px.

Marka kararları (İskender, 2026-08-22):
- **Yalnız kupa altın** (#E8C452) — "sadece kupa sarı kalsın, o'lardaki
  sarıyı kaldır". SEZONO yazısı ve figür koyu lacivert (#0B1B3F).
- Yazı/logo topa Midjourney'de DEĞİL kompozitle basılır: MJ metni bozuk
  yazar, marka işareti de gerçek dosyadan gelmeli.

Boyut kararı: 4 varyant (52/58/66/74dp) gerçek Flutter render'ıyla
karşılaştırıldı, **C = 66dp / 28dp taşma** onaylandı. Şerit 64dp SABİT —
taşan kısım `Clip.none` ile şeridin dışına çizilir, nav'ın yüksekliğini
BÜYÜTMEZ (2026-07-23 kavisli nav bug'ı geri gelmesin).

Bekçi: `test/mac_sekmesi_test.dart`.
