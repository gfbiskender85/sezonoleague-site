# assets/match2d — 2D maç gösterimi («Stadyum görünümü»)

Sözleşme: `docs/design/mac2d_test_paketi/MAC_2D_TEST_URETIM_PAKETI_V2_ACILI.md` (açılı plaka,
kullanıcı kararı 2026-10-26) ve `docs/rules/MAC_2D_GOSTERIM_FE.md` kural 8.

- `templates.json` — 52 sahne şablonu. ÜRETİLMİŞ dosya: `python3 tool/match2d_templates_gen.py`.
- `anchors.json` — plaka saha dörtgeni, tribün yamukları, karo/taş/top pivotları
  (`lib/features/match/mac2d/mac2d_plak.dart` okur; bozuksa derlenmiş varsayılan).
- `plak/` `crowd/` `oyuncu/` `top/` `pano/` `prop/` — Gemini çıktıları (WebP, sRGB). Yeni nesil kase
  plakaları (2026-10-26) b1–b4 dördü de var; saha dörtgeni dördünde aynı (240,330 / 1040,330 / 1190,640 /
  90,640). Ad plakaları ve tabela kırpılmış, magenta önceden alfaya çevrilmiş. `hava/` (yağmur, sis; siyah
  zemin, screen karışım) — koda bağlı DEĞİL, pubspec'te kayıtlı değil. Dosya adı
  paket tablosuyla BİREBİR. Klasörler `pubspec.yaml`'da kayıtlı: dosya bırakılınca kod
  DEĞİŞMEDEN devralır (`mac2dAvailableAssets` manifestten çözer); bulunmayan katman kodla
  çizilen yer tutucuyla kalır. Magenta zemin yüklemede şeffaflaştırılır.
- Detay turu (2026-10-26): `top/top` (yeni beyaz + siyah beşgen), `prop/yedek_kulubesi`, `prop/tunel_agzi`,
  `tifo/pankart_yatay`, `tifo/bayrak_dikey_f1..f3`, `crowd/o_{on,arka,yan}_f2|f3` — hepsi pakette;
  `tifo/` pubspec'te kayıtlı. Kod: `mac2d_detay.dart` + `mac2d_painter_detay.dart` (kural 16–19).
- Pankart turu (2026-10-26): `tifo/pankart_yatay` UZUN pankartın kumaşı (dokuz-dilim: uçlar %12, orta gerilir);
  yazı/arma/renk KODDA (kural 18). İleride `tifo/pankart_uzun` (8:1, nötr gri boş kumaş, magenta zemin) gelirse
  koda dokunmadan onun yerine geçer (anahtar `kMac2dBannerClothLong`, manifestte yoksa yüklenmez).
  `anchors.json` `plate.tunnel` ağızları + tünel yanı `far_3*`/`far_4*` blok kenarları yeniden ölçüldü.
- Gerçek marka/logo/yazı/yüz YOK; pano/plaka/büyük ekran BOŞ üretilir (içerik kodda).
