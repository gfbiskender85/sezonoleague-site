# Ana sayfa — Yaklaşan Maçlar ev/deplasman görselleri

| Dosya | Ne | Ölçü |
|---|---|---|
| `mac_ev.webp` | Ev sahibi — altın çerçeveli stadyum, yeşil saha | 256×256 |
| `mac_deplasman.webp` | Deplasman — beyaz/turkuaz uçak | 256×256 |
| `gosterge_deger.webp` | Piyasa değeri — altın jeton yığını + yeşil yükseliş oku | 256×256 |
| `gosterge_taraftar.webp` | Taraftar — turkuaz/beyaz atkı açan eller | 256×256 |
| `gosterge_prestij.webp` | Prestij — altın taç, turkuaz taş | 256×256 |

⭐ **Tek stilli Tasarım-2 seti (Gemini, İskender seçimi 2026-10-21).** Yumuşak
3B oyuncak dili, altın + turkuaz palet, yazı/logo/mor YOK. 2026-10-22'den beri
görseller ÇERÇEVESİZ, doğrudan panelin camında çizilir (`AnaSayfaIkon`,
`lib/core/theme/ana_sayfa_program.dart`): gösterge 32 dp, ev/deplasman telefonda
yoğun sırada 32, masaüstünde 48. Tuvalde her yanda ~%11 şeffaf pay var → görünen
çizim kutunun ≈ %78'i (ölçüldü). Kaynak PNG ve üretim kaydı bu depoda YOK (yalnız
işlenmiş 256² alfa WebP).

## Kurallar

1. **Şeffaf zemin ŞART** — görsel panelin camında duruyor (2026-10-21–22 arası rozette, ondan önce
   doğrudan ekran zemininde).
   ⚠️ Üretim aracı "transparent background" istendiğinde dama desenini
   görselin İÇİNE boyuyor (alfa üretmiyor). Doğru yol: **düz magenta**
   (`#FF00FF`) zeminde ürettirip zemini key'lemek. İlk turda bu atlandığı için
   dama deseni asset'in içine gömülmüştü.
2. **Renk gömülü** — `ColorFilter` ile boyanmaz (altın + turkuaz palet); palet
   değişirse asset yeniden üretilir.
3. **38 dp'de okunmalı.** Kalabalık/ışık direği/pencere gibi detay
   İSTENMEZ — ilk denemede stadyum silüeti UFO gibi okunmuştu.
4. Tüketici: `lib/features/ofis/widgets/ofis_v2_body.dart` (gösterge şeridi ve
   Yaklaşan Maçlar) → `AnaSayfaIkon` (çerçevesiz, 2026-10-22).
   `cacheWidth` cihazdan türetilir, dosya boyutundan DEĞİL.

## Geçmiş Kararlar

- 2026-10-22: Ortak ikon rozeti KALKTI (İskender: *«ikonların dış çevresindeki outline gibi
  duran çerçeve kötü duruyor»*); görseller çerçevesiz. Asset'lerin kendi zemini/parıltısı yok
  (kenar alfası 0) — çerçevesiz hâlde ek işlem gerekmedi.

- 2026-10-21: Gemini'nin ilk Tasarım-2 seti (taç ayrıntılı, taraftar cam figür,
  uçak siyah diskte — tek stil değildi) İskender'in seçtiği tek stilli setle
  değişti; beşi de ortak ikon rozetine girdi.

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
