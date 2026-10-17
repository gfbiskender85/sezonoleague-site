# Ana sayfa — Yaklaşan Maçlar ev/deplasman görselleri

| Dosya | Ne | Ölçü |
|---|---|---|
| `mac_ev.webp` | Ev sahibi — TEPEDEN görünen stadyum halkası + çim | 106×114 (38 dp @3x) |
| `mac_deplasman.webp` | Deplasman — mavi cam uçak | 114×114 (38 dp @3x) |
| `gosterge_deger.webp` | Piyasa değeri — yeşil jeton yığını + yükseliş oku | 86×102 (34 dp @3x) |
| `gosterge_taraftar.webp` | Taraftar — mavi üç figür | 139×102 (34 dp @3x) |
| `gosterge_prestij.webp` | Prestij — altın taç | 115×102 (34 dp @3x) |

2026-08-29, İskender: *"rakip logosu hiç koymayalım, ana asset home ya da uçak
görseli olsun, altında da rakip adı yazsın"* + *"ev yerine stadyum ikonu
üretelim"*.

## Kurallar

1. **Şeffaf zemin ŞART** — kart yok, görsel doğrudan ekran zemininde duruyor.
   ⚠️ Üretim aracı "transparent background" istendiğinde dama desenini
   görselin İÇİNE boyuyor (alfa üretmiyor). Doğru yol: **düz magenta**
   (`#FF00FF`) zeminde ürettirip zemini key'lemek. İlk turda bu atlandığı için
   dama deseni asset'in içine gömülmüştü.
2. **Renk gömülü** — `ColorFilter` ile boyanmaz. Ev camgöbeği (#7DF3F0→#2FBFC4),
   deplasman mavi (#BBD2FF→#5C79D6); palet değişirse asset yeniden üretilir.
3. **38 dp'de okunmalı.** Kalabalık/ışık direği/pencere gibi detay
   İSTENMEZ — ilk denemede stadyum silüeti UFO gibi okunmuştu.
4. Tüketici: `lib/features/ofis/widgets/ofis_v2_body.dart` → `_UpcomingCell`.
   `cacheWidth` cihazdan türetilir, dosya boyutundan DEĞİL.

## Geçmiş Kararlar

- 2026-08-29 (ilk tur): 3/4 açıdan **oval kâse** üretildi. İskender: *"daha iyi
  bir stadyum asseti üretebilirdin"* — 38 dp'de küvet gibi okunuyordu.
- 2026-08-29 (ikinci tur): beş aday 38 dp'de yan yana çizilip karşılaştırıldı —
  oval kâse · ön cephe · ışık direkli · rozet · **tepeden (SEÇİLDİ)**.
  ⭐ Karar 120 px'te değil **38 dp'de** verildi: diğer dördü o boyutta
  "yeşilimsi bir leke"ye dönüşüyordu. Tepeden görünümde halka kalın olduğu için
  silüet ayakta kalıyor, ortadaki çim "burası saha" bilgisini taşıyor ve uçakla
  optik ağırlığı denk.
  ⛔ Elenenleri tekrar önerme: ışık direkleri 38 dp'de KAYBOLUYOR; ön cephenin
  katmanları birbirine giriyor; rozet sepet/çanta gibi de okunabiliyor.
- 2026-08-29 (üçüncü tur): **Kulüp Göstergeleri şeridi**. İki kullanım
  çizilip gösterildi — cam pul KORUNUR (görsel 20 dp) / cam pul KALKAR
  (görsel 34 dp). İskender **seçenek 2**'yi seçti.
  ⭐ Gerekçe ölçüldü: eski Material glyph 17 dp'ydi; üretilmiş 3B görselin
  detayı o boyutta kayboluyor, cam pul onu bir kat daha küçültüyordu.
  Yaklaşan Maçlar da "kapsız" olduğu için ikisi artık aynı dili konuşuyor.
  ⚠️ Üretim notu: jeton ilk turda gülen YÜZLE, ikinci turda beyaz yuvarlak
  köşeli ÇERÇEVEYLE geldi. Prompt'ta "no face/no smiley" ve "background
  filling the ENTIRE frame edge to edge, no rounded corners, no white border"
  ikisi de açıkça yazılmalı.
  ⛔ Cam pul (`_GlassPill`) ve `_indGreen/_indBlue/_indAmber` sabitleri
  SİLİNDİ — tüketicisi kalmamıştı.
