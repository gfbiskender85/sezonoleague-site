# Takım Düzeni satır görselleri — bırakma noktası

Takım Düzeni v2 ekranındaki 7 satırın sağ görsel alanı (168×112, 3:2) bu
klasörden beslenir. Asset ölçüsü **504×336** (@3x). Kaynak: export 31
`takim-duzeni-v2/README.md` tablosu.

| BE `id` | Dosya | Sahne |
|---|---|---|
| `savunmaYerlesimi` | `org_savunma_yerlesimi.png` | dört savunmacı blok, arkada kaleci |
| `presOrg` | `org_pres.png` | üç oyuncu topa koşuyor, baskı |
| `savunmaGecisi` | `org_savunma_gecisi.png` | top kaybı, geri koşu |
| `hucumOrg` | `org_hucum_organizasyonu.png` | pas üçgenleri, hat arası |
| `hucumGecisi` | `org_hucum_gecisi.png` | kontratak, ok gibi koşu |
| `dtSavunma` | `org_duran_top_savunma.png` | ceza sahasında markaj |
| `dtHucum` | `org_duran_top_hucum.png` | frikik duvarı, vuruş hazırlığı |

**Dosyayı bu adla buraya koymak yeterli — kod değişmez.** Eşleme tek yerde:
`lib/features/team/takim_duzeni/takim_duzeni_screen.dart` → `kOrgFeatureAssetFile`.
Dosya yokken ikon + dosya adı + `504×336` yazan koyu panel çizilir; kırık
görsel işareti boyanmaz (`Image.asset` + `errorBuilder`).
