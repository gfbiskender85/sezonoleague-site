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
- 2026-11-16 (G26): 11 Yönetim kartı illüstrasyonu (`yonetim_*`, Yönetim Deste) aynı boruyla eklendi: 384×384 WebP, 16–31 KB/dosya,
  yaklaşık 260 KB; paket toplamı 33 dosya ≈ 680 KB. Kaynak: Gemini 1024 PNG.
- 2026-11-17 (tek aile, bayrak `DESTE_TEK_AILE`): `ana_mesajlar.webp` — Ana Sayfa «Mesajlar» iş kartının görseli (mühürlü
  zarf + mektup), aynı boruyla 384×384 WebP, 17 KB; paket toplamı 34 dosya. Ana Sayfa'nın diğer iş kartları sekmelerdeki
  modül görselini kullanır (`desteAnaIllus`).
- 2026-11-17 (G25): Maça Hazırlık V2 — `takim_kulube` (yedek kulübesi) · `takim_konusma` (düdük + pazubandı + megafon) · `takim_kadro_aciklama` (kadro panosu); aynı boru, 384×384 WebP, 26–35 KB/dosya (≈88 KB); paket toplamı 36 dosya (tek aile `ana_mesajlar` ile birlikte 37). Çim: `assets/images/match/mh_cim_yatay.webp` (1440×960).
- 2026-11-22: Yönetim Deste için `yonetim_muze.webp` (müze vitrini + altın kupa/flama/madalya) üretildi ve `yonetim_taraftarlar.webp` (megafon + bayrak + davul + atkı) güncellendi; aynı boru 384×384 RGBA WebP; paket toplamı **38 dosya**.
- 2026-11-23: Yönetim Deste için `yonetim_forum.webp` (iki 3B konuşma balonu + kalkan rozet + not defteri ve altın dolma kalem) eklendi; aynı boru 384×384 RGBA WebP (24 KB); paket toplamı **39 dosya**.
