# Yönetim hero görselleri — bırakma noktası

Yönetim hub'ının on kartının 150dp hero bandı bu klasörden beslenir.

| Dosya | Kart | Sahne | Aksan | Durum |
|---|---|---|---|---|
| `hero-personel.webp` | Teknik Kadro | üç antrenör sahayı izliyor, sırtları dönük | mavi `#9FC2FF` | ✅ |
| `hero-kunye.webp` | Kulüp Binası | koyu modern tesis cephesi (İskender MJ karesi, 3. sürüm) — arma montaj halkasına rozet, ad cephedeki pano bandına TABELA olarak CANLI bindirilir (`kunye_hero_overlay.dart`) | çelik grisi `#C8CDD8` | ✅ |
| `hero-akademi.webp` | Akademi | 12-13 yaşında çocuklar sahada koşuyor, yakın çekim | yeşil `#7BE6A0` | ✅ |
| `hero-saglik.webp` | Sağlık Merkezi | kulüp binasının sağlık KAPISI (İskender MJ karesi, 2. sürüm): koyu cephe + yeşil eczane artısı + cam kapıda BOŞ disk — arma CANLI bindirilir (`saglik_hero_overlay.dart`, ad yok) | magenta `#FF5C8A` | ✅ |
| `hero-antrenman-tesisi.webp` | Antrenman Tesisi | A takımı sahada düz koşu, seviye-nötr | camgöbeği `#7DF3F0` | ✅ |
| `hero-gozlem-agi.webp` | Gözlem Ağı (2026-10-04) | gözlemci tribünde sırtı dönük maç izliyor — `transfer/hero-kesif.webp`'nin kopyası (o dosya transferde kullanılmıyordu) | mercan `#FF9F5A` | ✅ |
| `hero-stadyum.webp` | Stadyum | tribünden taraftar perspektifi, siluetler önde | mor `#C9AEFF` | ✅ |
| `hero-finans.webp` | Mali Durum | yönetici silüeti + laptopta hesap hareketleri | kehribar `#EFC987` | ✅ |
| `hero-sponsorluk.webp` | Sponsorluklar | imza töreni silüeti, arkada blur uydurma logo panosu | buz mavisi `#B9C8EE` | ✅ |
| `hero-yetki.webp` | Yetki & Ayarlar | el silüeti + telefon ayarlar menüsü, arka plan blur | derin turkuaz `#4FE3E0` | ✅ |

**Dosyayı bu adla buraya koymak yeterli — tek satır kod değişmez.**
`YonetimHeroBand` asset manifest'ini sorgular: dosya varsa fotoğraf çizer,
yoksa bugünkü prosedürel çizime (`yonetim_module_visuals.dart`) düşer. Klasör
`pubspec.yaml`'da zaten kayıtlı; kod hiçbir yerde görselin piksel boyutuna
bakmaz (`BoxFit.cover` + cihazdan türetilen `cacheWidth`).

⚠️ **Eski "obje render / izometrik" aile ayrımı TERK EDİLDİ** (2026-08-20).
Gerekçe: izometrik dil doğası gereği ikonik; hero bandında ikon gibi duruyor.
**Dokuz kartın dokuzu da fotografik sahne** (`--ar 4:5`, kadraj `center 44%`).
Ekran hero'sunda (`Yv4Hero`, bant 176 dp) bu kadrajın kod karşılığı TEK
sabit: `kYonetimHeroAlignment = Alignment(0, −0.12)` (`yonetim_v4_kit.dart`,
2026-09-08 — eski −0.3 özneyi başından kesiyordu). Ekranda kopya sabit yok.

Ölçülmüş kurallar (İskender turlarından):
- **Seviye-nötr kal:** bina, projektör, çatı, skorboard bir yükseltme kademesi
  ima eder — oyuncuda o kademe olmayabilir. Antrenman Tesisi bu yüzden sahada
  düz koşu; tesisin kendisi kadrajda YOK.
- **Yüz gösterme:** silüet / sırtı dönük / arkadan aydınlatma. Ama sahneyi
  KARARTMA — `silhouette` kelimesi tüm kareyi koyulaştırıyor, özneyi arkadan
  aydınlatıp karanlığı yalnız figüre bağla.
- **Gerçek marka YOK:** sponsor panosu uydurma işaret + blur (logo okunursa
  IP riski, okunmazsa "renkli tuğla" çıkıyor).
- Çocuk sahnesinde **yakın çekim** şart — uzaktan yaş belli olmuyor.

Hedef: WebP q88. Kaynak kare 384×480 doğal çözünürlükte bırakılır —
**ŞİŞİRME**, kod piksel boyutuna bakmaz, büyütmek yalnız yumuşaklık üretir.
Yedi dosya bugün toplam ~144 KB.

**Künye İSTİSNASI (2026-08-22):** dokuz kareden yalnız Künye'nin görseli
"yarım" — kapının üstündeki lacivert pano BİLEREK BOŞ. Arma ve kulüp adı
görselde değil, kodda basılır (`kunye_hero_overlay.dart` → gerçek `ClubCrest`
+ kulüp adı, veri `ClubProvider`). Gerekçe: armayı Midjourney'de tutturmak
imkânsız + her kulüpte farklı olmalı. Hiza SABİT DEĞİL: halka/pano
konumları görselden ölçülüp (`kunye_hero_overlay.dart` sabitleri, 384×480
karede) hero ölçeğinden TÜRETİLİR — 375'lik SE'de de 430'luk Pro Max'te de
oturur. Görseli değiştirirken o sabitler yeni kareden yeniden ölçülmeli.

**Künye karesinin ÖLÇÜLEN hatları (2026-08-25, 384×480 kaynak kare):**

| Ne | y | Kullanan |
|---|---|---|
| Çatı hattı (cephenin üst kenarı) | 225 | armanın üst sınırı — TAŞAMAZ |
| Arma montaj halkası (merkez) | 251 | `_crestCy`, çap `_crestSize` = 50 |
| Pano bandı (düz yüzey) | 277 – 304 | `_bandTop`/`_bandBottom` — tabela |

Tabela bandı ekranda **kenardan kenara** çizilir (uçları görünen "asılı plaka"
hissi İskender tarafından reddedildi, 2026-08-25). Ad puntosu SABİT 20: kulüp
adı 7-15 karakter (`CLUB_NAME_MIN_LEN`/`MAX_LEN`), en kötü durumda bile
300 px'e sığar; kural öncesi uzun adlar o eşikte ufalır, KESİLMEZ.
Son iki kare (Künye + Sağlık) Midjourney değil Gemini üretimi — aynı dil
korunarak; kaynak istemler bu dosyanın git geçmişinde.

Bekçi: `test/yonetim_kart_izgarasi_test.dart` → "hero fallback" +
"künye hero bindirmesi" grupları; geometri (bant/arma/çatı hattı)
`test/kulup_binasi_tabela_test.dart`.
