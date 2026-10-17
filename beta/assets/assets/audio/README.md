# assets/audio — SEZONO ses paketi (Faz 2, 2026-10-04 · Faz 3, 2026-10-05 · açılış v2, 2026-10-05)

Kaynak: ElevenLabs üretimi (İskender, 2026-10-04) — prompt kartları
https://claude.ai/artifact/E3Q8MPD36PHqBZkvZRPoVy. Ham WAV'lar İskender'in
masaüstünde (`~/Desktop/sezono sesler/`); bu klasördekiler işlenmiş çıktıdır.
Yeniden üretim: `python3 tool/audio/build_audio.py assets/audio` (ffmpeg 9 +
numpy/scipy; kaynak yolları betiğin başında).

Biçim: **AAC .m4a** (iOS OGG çalmaz), 44,1 kHz, Apple AAC kodlayıcı (`aac_at`).
Kural belgesi: `docs/rules/HIS_TITRESIM_SES.md`.

## İşlem

- **Arayüz (D1–D8):** mono · baş sessizliği kırpıldı (eşik −50 dBFS **ya da**
  tepeden −30 dB, hangisi yüksekse — D1'in önünde −44 dB'lik gürültü vardı,
  mutlak −50 eşiği onu "ses" sayıp tıkı 0,2 sn geciktiriyordu) · süre tavanı
  (D1 0,25 · D2–D5a 0,5 · D6/D7 0,9 sn; D8 tek tık 0,15 sn) · sonda 30 ms fade
  (kesimde enerji varsa 80 ms) · **RMS hizalı** −20 dBFS (D8 −26), tepe tavanı
  −3 dBTP. Kısa seslerde LUFS anlamsız (0,4 sn'lik ölçüm penceresinden kısa).
- **Anlar (E):** −16 LUFS, 4× aşırı örnekli limiter ile gerçek tepe ≤ −3 dBTP
  (kaynakta E3a/E4a/E5/E6a tepe 0 dBFS'yi aşıyordu). L/R korelasyonu > 0,95
  olanlar mono'ya indirildi (fark yok, yarı boyut). E2'nin 1,9 sn baş sessizliği
  kırpıldı; E3c 14 sn → 3,8 sn (ilk uzun düdük + 0,8 sn fade). E2 limiter
  tavanında −20 LUFS'ta kaldı (alçak frekanslı darbe; K-ağırlığı alçağı kısar).
- **Motif:** Golden Bright Horizons 36,0–40,0 sn (bir cümle = iki ölçü, ~120 BPM),
  sıfır geçişte kesim, sonda 0,6 sn sönüm.
- **Bildirim:** motifin ilk iki notası (36,00–36,47 sn) + üstel yankı kuyruğu
  (doğal sönüm; müzik sürekli olduğu için kesim noktasında kendi sönümü yok).
  0,84 sn.
- **Açılış kısa v2 (1,5 sn):** tek projektör vuruşu (D2 ham dosyası 0,40–1,20
  sn, motiften 4 dB alçak) 0,08 sn'de (`kTekProjektor.yanma`) + motifin ilk iki
  notası + yankı 0,30 sn'de (kilidin patlama anı); sonda 0,3 sn sönüş.
- **Tören:** Golden Bright 36,0–43,0 sn (iki cümle), sonda 1 sn fade. Üretilen
  2 sn'lik E7 KULLANILMADI.
- **Açılış uzun v2 (5,3 sn) — GEÇİCİ KURGU:** açılış v2 panosunun A deneme
  kurgusu (`scratchpad/acilis/v2/ses.py` üretimi `acilis_v2_A.wav`, 5,6 sn):
  stüdyo çınlaması 0,20 (D5a) · C3 uğultu 1,00 · dört projektör vuruşu
  1,42 / 1,77 / 2,12 / 2,47 (D2 «gong») · Lights parıltı 1,30 · şut 3,60
  (football striking + Decisive Strike vurgusu) · tribün patlaması 4,18 ·
  Glory coşku 4,25 · motif 4,20. Sahneyle hizalı: ses kancası 0'da (öteleme
  YOK), kilit 5,0'da oturur, uçuş 5,3'te biter → 5,3 sn'ye kesildi, son 0,4 sn
  sönüş, −16 LUFS, limiter. **B3/B4/B5/B6 yeni üretim gelince kurgu
  yenilenecek** (projektör «gong»u · şut · tribün patlaması · stüdyo çınlaması
  için ayrı ElevenLabs kartları; şimdiki vuruşlar arayüz/maç kaynaklarından
  ödünç). Eski 3,5 sn'lik C3 + B1 kurgusu emekli (B1 ışık vuruşları artık
  kullanılmıyor).
- **Fon:** 60 sn → 56 sn kesintisiz döngü (son 4 sn ile ilk 4 sn eşit güçlü
  çapraz geçiş — döngü noktasında örnek düzeyinde süreklilik). Ofis −30 LUFS,
  maç günü −28 LUFS; uygulamada ayrıca kanal sesi 0,35. Stereo **64 kbps**
  (96 kbps'te paket 1,82 MB'a çıkıyordu; −30 LUFS'luk pad'de fark duyulmaz).
- **Faz 3 — ofis fonu iki katman:** C1a pad −30 LUFS + C1c atmosfer
  (`Dusk_in_the_Empty_Office`, uzak saha sesleri) −34 LUFS — önce karışım, sonra
  tek döngü geçişi (iki katman aynı noktada çapraz geçer); tek dosya `fon_ofis`.
- **Faz 3 — tribün döngüleri (maç odası):** C3a sakin · C3b baskı · C3c coşku,
  30 sn → 27 sn kesintisiz döngü. Ölçülen ham dikiş farkı 13–16 dB → son 3 sn ↔
  ilk 3 sn eşit güçlü çapraz geçiş; kodlanmış dosyada dikiş 0–1,4 dB. Üçü de
  −26 LUFS (şiddet farkı karakterden — seviye sıçraması geçişte pompalardı),
  stereo 64 kbps. C3d (`Stadium_Breath_and_Roar`) pakete GİRMEDİ.
- **Faz 3 — anlar:** E4a gol 4 sn −16 LUFS stereo (L/R korelasyonu 0,11);
  E4b rakip gol kaynak −31 → −20 LUFS (gol sesinden 4 dB alçak); E6b
  antrenman bitti: tepe +0,1 dBFS, baş 0,26 sn sessizlik kırpıldı, 2 sn'ye
  kesildi, 0,6 sn sönüş, limiter (L/R 0,94 → stereo).
- **Faz 3 — açılış ışıkları:** B1 (`Lights_of_the_Arena`) ~90 ms arayla ~20
  vuruşluk bir «tunk» dizisi; bütünü dört projektörle örtüşmüyordu. Dört
  belirgin vuruş (B1 0,53 · 0,645 · 0,74 · 0,965 sn, giderek güçlenen) −5 ms ..
  +85 ms kesildi, 0,35 sn yankı kuyruğuyla projektörlerin yanma anlarına
  (0,30 · 0,58 · 0,86 · 1,14 sn — `kDortProjektor.yanma`; ses kancası tam hâlde
  0,8 sn ötelendiği için ses saati = sahne saati) konuldu. Düzey motif başının
  6 dB altı (uğultuyla aynı tavan), bindirme ilk 1,6 sn içinde.

## Ölçümler (kodlanmış .m4a üzerinde, ffmpeg `ebur128`)

| Dosya | Kaynak | Süre sn | Kanal | LUFS | RMS dBFS | Tepe dBTP | kbps | KB |
|---|---|---|---|---|---|---|---|---|
| `ui_secim.m4a` | D1_select.wav | 0,26 | mono | — | −23,9 | −4,2 | 64 | 2,9 |
| `ui_onay.m4a` | D2_confirm.wav | 0,30 | mono | — | −20,0 | −8,1 | 64 | 3,1 |
| `ui_uyari.m4a` | D3_warn.wav | 0,51 | mono | −31,2 | −20,0 | −7,5 | 64 | 4,4 |
| `ui_kart.m4a` | D4_kart.wav | 0,49 | mono | −21,2 | −20,0 | −3,0 | 64 | 5,1 |
| `ui_perde.m4a` | D5a_perde_ac.wav | 0,51 | mono | −28,8 | −20,0 | −7,6 | 64 | 4,9 |
| `ui_para.m4a` | D6_para.wav | 0,91 | mono | −24,4 | −22,6 | −3,0 | 64 | 8,5 |
| `ui_bildirim_yedek.m4a` | D7_bildirim.wav | 0,86 | mono | −25,3 | −20,0 | −8,7 | 64 | 6,0 |
| `ui_kaydirici.m4a` | D8_kaydirici.wav | 0,09 | mono | — | −26,0 | −8,0 | 64 | 1,5 |
| `an_cekic.m4a` | E2_cekic.wav | 1,04 | mono | −20,1 | −8,4 | −4,3 | 64 | 8,9 |
| `an_baslama.m4a` | E3a_baslama.wav | 2,02 | stereo | −16,1 | −22,0 | −12,3 | 96 | 23,9 |
| `an_devre.m4a` | E3b_devre.wav | 2,02 | stereo | −16,0 | −21,5 | −12,7 | 96 | 24,3 |
| `an_bitis.m4a` | E3c_bitis.wav | 3,78 | stereo | −16,1 | −21,8 | −11,0 | 96 | 48,6 |
| `an_gol.m4a` | E4a_gol.wav | 4,02 | stereo | −16,1 | −19,4 | −6,4 | 96 | 47,6 |
| `an_rakip_gol.m4a` | E4b_rakip_gol.wav | 3,02 | stereo | −20,1 | −23,1 | −7,3 | 96 | 35,9 |
| `an_kart.m4a` | E5_kart.wav | 2,02 | stereo | −16,1 | −19,1 | −9,0 | 96 | 26,8 |
| `an_antrenman_basla.m4a` | E6a_antr_basla.wav | 2,67 | mono | −16,0 | −15,4 | −7,4 | 64 | 20,7 |
| `an_antrenman_bitti.m4a` | E6b_antr_bitti.wav | 2,02 | stereo | −16,2 | −21,8 | −11,6 | 96 | 25,9 |
| `an_seviye.m4a` | E8_seviye.wav | 2,02 | mono | −16,0 | −15,5 | −3,9 | 64 | 16,0 |
| `an_kotu_haber.m4a` | E9_kotu_haber.wav | 3,00 | mono | −16,0 | −14,2 | −5,1 | 64 | 22,8 |
| `an_imza.m4a` | E1_imza.wav | 0,91 | mono | −17,1 | −17,9 | −3,3 | 64 | 8,7 |
| `motif.m4a` | Golden_Bright… 36,0–40,0 sn | 4,02 | stereo | −16,0 | −18,6 | −5,6 | 96 | 47,6 |
| `bildirim.m4a` | Golden_Bright… 36,00–36,47 sn + yankı | 0,84 | stereo | −18,0 | −19,5 | −8,9 | 96 | 10,1 |
| `acilis_kisa.m4a` | D2 vuruş 0,40–1,20 sn @0,08 + Golden_Bright… 36,00–36,47 sn + yankı @0,30 | 1,51 | stereo | −16,0 | −18,1 | −6,3 | 96 | 14,1 |
| `toren.m4a` | Golden_Bright… 36,0–43,0 sn | 7,01 | stereo | −16,1 | −18,6 | −5,6 | 96 | 82,5 |
| `acilis.m4a` | acilis_v2_A.wav (pano A kurgusu, GEÇİCİ) 0–5,3 sn, son 0,4 sn sönüş | 5,32 | stereo | −16,1 | −19,2 | −3,5 | 96 | 73,6 |
| `fon_ofis.m4a` | C1a ofis pad −30 + C1c atmosfer −34 (döngü) | 56,01 | stereo | −29,7 | −32,0 | −15,4 | 64 | 456,9 |
| `fon_macgunu.m4a` | C2a_macgunu.wav (döngü) | 56,01 | stereo | −28,2 | −30,1 | −9,0 | 64 | 459,7 |
| `fon_tribun_sakin.m4a` | C3a_tribun_sakin.wav (döngü) | 27,00 | stereo | −26,3 | −26,8 | −7,7 | 64 | 221,3 |
| `fon_tribun_baski.m4a` | C3b_tribun_baski.wav (döngü) | 27,00 | stereo | −26,2 | −29,0 | −13,1 | 64 | 218,2 |
| `fon_tribun_cosku.m4a` | C3c_tribun_coskU.wav (döngü) | 27,00 | stereo | −26,2 | −29,4 | −14,6 | 64 | 232,8 |

**Toplam: 2.215.400 bayt ≈ 2,11 MB** (Faz 2: 1,33 MB; Faz 3 tribün ×3 ≈ 672 KB
+ uzun gol/rakip gol; açılış v2 +33 KB). `test/ses_test.dart` bekçisi 2.200 KB'ı aşınca kırılır —
tribün döngüleri zaten en düşük stereo hızda (64 kbps); fazlası ayrı karar.

## Kaynak → hedef eşlemesi

| Kart | ElevenLabs dosyası | Hedef |
|---|---|---|
| D1 | `A_very_soft,_short_t_#4-…` | `ui_secim` (select kanalı) |
| D2 | `A_satisfying,_solid,_#3-…` | `ui_onay` (confirm kanalı) |
| D3 | `Two_quick,_muffled,__#1-…` | `ui_uyari` (warn kanalı) |
| D4 | `A_thick_collectible__#2-…` | `ui_kart` (keşif dosyası açılışı) |
| D5a | `Açılış_A_soft,_short_#4-…` | `ui_perde` (pakette, bağlı DEĞİL) |
| D6 | `A_short,_pleasant_ca_#1-…` | `ui_para` (transfer kapandı · sponsor) |
| D7 | `Two_soft,_rising_not_#1-…` | `ui_bildirim_yedek` (yedek; bildirim motiften) |
| D8 | `An_extremely_short,__#1-…` | `ui_kaydirici` (pakette, bağlı DEĞİL) |
| E1 | `Two_fountain_pen_sig_#4-…` | `an_imza` (kanca — yenileme masası app#1050) |
| E2 | `A_single_decisive_wo_#1-…` | `an_cekic` (müzayede «Hemen Al») |
| E3a/b/c | `A_single_sharp_refer_#1` · `Two_referee_whistle__#2` · `Three_long_referee_w_#4` | `an_baslama` · `an_devre` · `an_bitis` |
| E4a | `The_Decisive_Strike_…` (Faz 3; eski `A_football_striking__#3` emekli) | `an_gol` |
| E4b | `Missed_Opportunity_…` (Faz 3) | `an_rakip_gol` |
| E5 | `A_sharp_referee_whis_#2-…` | `an_kart` (maç kartı) |
| E6a | `A_coach's_whistle_bl_#3` | `an_antrenman_basla` |
| E6b | `End_of_Training_…` (Faz 3; eski `One_long_coach's_whi_#3` emekli) | `an_antrenman_bitti` |
| B1 | `Lights_of_the_Arena_…` (Faz 3) | `acilis` v2 kurgusunda parıltı katmanı (1,30 sn; vuruş D2'den) |
| C1c | `Dusk_in_the_Empty_Office_…` (Faz 3) | `fon_ofis` (atmosfer katmanı) |
| C3a/b/c | `Stadium_Murmur_and_Anticipation_…` · `Stadium_Pressure_Chant_…` · `Stadium_Glory_Loop_…` (Faz 3) | `fon_tribun_sakin` · `fon_tribun_baski` · `fon_tribun_cosku` |
| C3d | `Stadium_Breath_and_Roar_…` | pakete GİRMEDİ (İskender 10-05) |
| — | `Legacy_of_the_Club_…` (60 sn müzik) | **karar bekliyor** — kullanılmadı |
| E8 | `A_short_uplifting_ri_#2-…` | `an_seviye` (kanca — tesis bitti anı yok) |
| E9 | `A_low,_soft,_descend_#1-…` | `an_kotu_haber` (antrenmanda sakatlık) |
| G3/G5 | `Golden_Bright_Horizons_Logo_…` | `motif` · `bildirim` · `acilis_kisa` · `toren` · `acilis` (v2 kurgusunda 4,20 sn) |
| C3 giriş | `secilen/acilis_giris_C3.wav` | `acilis` (v2 kurgusunda uğultu, 1,00 sn) |
| D2 · D5a · E4a · `A_football_striking__#3` · `Large_football_stadi_#2` · `Stadium_Glory_Loop` | ödünç | `acilis` v2 GEÇİCİ kurgusu (gong · çınlama · şut vurgusu · top · tribün patlaması · coşku) + `acilis_kisa` (D2 vuruş) |
| C1a | `Office_at_Dusk_…184258.wav` | `fon_ofis` |
| C2a | `Echoes_of_Match_Day_…` | `fon_macgunu` |
| C1b · C2b | `Office_at_Dusk_… (1)` · `Match_Day_Echoes_…` | yedek — pakete GİRMEDİ |
| C3x/y/z | `Large_football_stadi_#1/#2/#3` | KULLANILMADI (0,5–1 sn; döngü olamaz) |
| E7 | `A_triumphant_7-secon_#3-…` | KULLANILMADI (2 sn geldi; tören Golden Bright'tan) |

## needsRegen — ElevenLabs'tan yeniden üretilecekler

Faz 3'te kapandı: C3 tribün ×3 · E4a gol · E4b rakip gol · E6b antrenman bitti ·
B1 açılış ışıkları · C1 atmosfer katmanı.

| Kart | Sorun | İstenen süre |
|---|---|---|
| E1 imza | 1 sn — kalem sesi kısa | **2,5 sn** (iki imza + kağıt) |
| D5b perde kapanış | hiç yok | **0,4 sn** (D5a'nın tersi) |
| B2 açılış top vuruşu | hiç yok (logo anı) | **0,6 sn** |
| B3 projektör «gong» | D2 arayüz onayından ödünç (açılış v2) | **0,8 sn** (tek, kuru, metalik; ×4 yanma) |
| B4 şut | `A_football_striking__#3` + Decisive Strike karışımı | **1,0 sn** (vuruş + ıslık) |
| B5 tribün patlaması | `Large_football_stadi_#2` (0,5–1 sn) | **1,5 sn** (patlama + sönen coşku) |
| B6 stüdyo çınlaması | D5a perde sesinden ödünç | **1,2 sn** (tek yumuşak çınlama) |

## Karar bekliyor

| Dosya | Durum |
|---|---|
| `Legacy_of_the_Club_2026-10-04T205508.wav` (60 sn müzik) | pakete girmedi; nerede/ne zaman çalacağı İskender'in kararı (fon müzik değil atmosferdir — kural 8) |
