# Takım hero görselleri — bırakma noktası

Takım hub'ının sekiz kartının 150dp hero bandı bu klasörden beslenir.

| Dosya | Kart | Aile | Aksan |
|---|---|---|---|
| `hero-kadro-taktik.webp` | Kadro & Taktik | obje render | kehribar `#EFC987` |
| `hero-kadro.webp` | Kadro Listesi | izometrik | mavi `#9FC2FF` |
| `hero-forma-numaralari.webp` | Forma Numaraları | obje render | çelik grisi `#C8CDD8` |
| `hero-antrenman.webp` | Antrenman Merkezi | obje render | yeşil `#7BE6A0` |
| `hero-maca-hazirlik.webp` | Maça Hazırlık | obje render | mor `#C9AEFF` |
| `hero-analizler.webp` | Analizler | izometrik | camgöbeği `#7DF3F0` |
| `hero-kondisyoner.webp` | Kondisyoner Raporu | izometrik | magenta `#FF5C8A` |
| `hero-duzen.webp` | Takım Düzeni | izometrik | buz mavisi `#B9C8EE` |

**Dosyayı bu adla buraya koymak yeterli — tek satır kod değişmez.**
`TeamHeroBand` asset manifest'ini sorgular: dosya varsa fotoğraf çizer, yoksa
bugünkü prosedürel çizime (`team_module_visuals.dart`) düşer. Klasör
`pubspec.yaml`'da zaten kayıtlı; kod hiçbir yerde görselin piksel boyutuna
bakmaz (`BoxFit.cover` + cihazdan türetilen `cacheWidth`).

⚠️ **Yukarıdaki "Aile" sütunu BAYAT — 2026-08-20'de izometrik aile TERK EDİLDİ.**
Gerekçe: izometrik dil doğası gereği ikonik; ne kadar iyi üretilirse üretilsin
hero bandında ikon gibi duruyor. **Sekiz kartın sekizi de fotografik sahne**
(`--ar 4:5`). Aksan renkleri geçerli, aile sütunu değil.

Güncel aile kuralı — **fotografik sahne, nesne portresi değil**. Sabit olan
karanlık DEĞİL, **soğuk renk grade'i + sinematik alan derinliği**:
- İç mekân kartları **AYDINLIK** (`high key lighting`, mekânı açıkça aydınlık
  tarif et; negatife `dark, moody, dim, shadowy, low key lighting, silhouette,
  night`). Gece geçenler (tünel, tribün, seremoni) doğal olarak koyu.
- **Yüz gizleme için sahneyi KARARTMA** — özneyi arkadan aydınlat
  (`rim lit from behind` + `features not visible`), karanlığı yalnız figüre bağla.
- Ölçülmüş kelime tuzakları: `collar` → klasik gömlek · `silhouette` → tüm sahne
  kararıyor · `heat press/workbench` → imalat sahnesi.
- Sayılar **tek tek sayılmalı** ("left shirt 9, middle 10"); "her birinde farklı"
  işlemiyor.

Hedef: WebP q88, sekiz dosya ≤ 320 KB. ⚠️ Kaynak kare 600px'ten küçükse
**ŞİŞİRME** — kod piksel boyutuna bakmıyor, büyütmek yalnız yumuşaklık üretir
(`hero-kesif.webp` ve `hero-duzen.webp` 384×480 doğal çözünürlükte duruyor).

Bekçi: `test/takim_kart_izgarasi_test.dart` → "hero fallback" grubu.
