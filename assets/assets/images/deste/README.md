# Deste kart illüstrasyonları (G22)

2026-11-15 — Takım / Maç / Transfer sekmelerinin «Deste» kart görünümü (bayrak `SEKME_DESTE`,
`lib/features/hub/deste/`). Her modül kartının sağ alt köşesinde (masaüstünde ortasında) çizilir.

- Kaynak: Gemini üretimi, 1024×1024 RGBA PNG (krem + lacivert + altın 3B nesne, saydam zemin).
- Paket hâli: saydam kenar kırpılır, kareye ortalanır, **384×384 WebP** (q84, alfa q90). 22 dosya ≈ 420 KB.
- Ad = `<sekme>_<modül>.webp`; koddaki karşılığı `DesteModul.illus` (`desteIllusAsset`).
- Kıta kupalarının her kademesi kendi illüstrasyonunu kullanır: `mac_elit_kupa` · `mac_super_kupa` · `mac_yukselen_kupa`
  (`desteKitaIllus`).
- 2026-11-16 (G23): jenerik görünen dört kart futbola özgü nesneyle yeniden üretildi — transfer pazarı (askıda forma +
  fiyat etiketi), görüşmeler (mühürlü sözleşme + dolma kalem + top), geçmiş (bağcıklı eski deri top + kum saati),
  numaralar (arkadan «10» forma); kıta kupaları üç ayrı siluet (elit: uzun kulplu · süper: kalkan plaket · yükselen: alevli ince kupa).
- Kapsam bekçisi: `test/deste_sekme_test.dart` → «illüstrasyon kapsamı».
