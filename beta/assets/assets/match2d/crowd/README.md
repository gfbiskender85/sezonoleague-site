# assets/match2d/crowd — yönlü seyirci karoları (test paketi v2)

256×256, 7×5 kişi, giysi nötr gri (kod takım rengine boyar), ten/saç doğal, zemin `#FF00FF`
(yüklemede şeffaf). `o_on` uzak tribün (önden), `o_arka` yakın tribün (arkadan), `o_yan`
kale arkaları (sola bakar; sol tribünde kod aynalar), `o_on_joy` gol sevinci, `o_on_atki`
atkı/flama, `o_dep_yan` deplasman bloğu, `o_on_seyrek` %35 dolu. Yoksa nokta kalabalığı.

Taraftar hareketi (Gemini detay turu 2026-10-26): `o_on_f2`, `o_on_f3`, `o_arka_f2`, `o_arka_f3`,
`o_yan_f2`, `o_yan_f3` — aynı 35 kişi, aynı ızgara, küçük poz farkı (mevcut karo kare 1). 3 kare/sn,
0,3 sn çapraz geçiş, bloka göre faz kaydırma; yoksa kod faz gruplarını sinüsle kaydırır. Gölgeli (koyu mor)
magenta zemin de alfaya çevrildi + mor sızma arındırıldı (kayıpsız).

`o_dep_yan_joy` (2026-10-27): deplasman bloğunun gol sevinci karosu — `o_dep_yan` ile aynı ızgara; 1024 kaynaktan 256'ya premultiplied küçültme, magenta alfaya çevrildi + sızma arındırıldı. Henüz koda bağlı değil.
