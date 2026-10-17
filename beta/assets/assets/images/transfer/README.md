# Transfer hero görselleri — bırakma noktası

Transfer hub'ının altı kartının 150dp hero bandı bu klasörden beslenir.

| Dosya | Kart | Aile | Aksan |
|---|---|---|---|
| `hero-pazar.webp` | Transfer Pazarı | fotografik | camgöbeği `#7DF3F0` |
| `hero-kesif.webp` | Keşif | fotografik | yeşil `#7BE6A0` |
| `hero-ihtiyac.webp` | İhtiyaç Listesi | fotografik | mavi `#9FC2FF` |
| `hero-gorusme.webp` | Görüşmeler | fotografik | kehribar `#EFC987` |
| `hero-satis.webp` | Satış Merkezi | fotografik | magenta `#FF2D78` |
| `hero-gecmis.webp` | Transfer Geçmişi | fotografik | çelik grisi `#C8CDD8` |

**Dosyayı bu adla buraya koymak yeterli — tek satır kod değişmez.**
`TransferHeroBand` asset manifest'ini sorgular: dosya varsa fotoğraf çizer,
yoksa bugünkü prosedürel çizime (`transfer_module_visuals.dart`) düşer. Klasör
`pubspec.yaml`'da zaten kayıtlı; kod hiçbir yerde görselin piksel boyutuna
bakmaz (`BoxFit.cover` + cihazdan türetilen `cacheWidth`).

Üretim prompt'ları: `docs/design/transfer_kart_gorselleri_midjourney_prompts.md`
(backend deposu). Hedef: 600px genişlik, WebP q88, altı dosya ≤250 KB.

Bekçi: `test/transfer_kart_izgarasi_test.dart` → "hero fallback" grubu.
