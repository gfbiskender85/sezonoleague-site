# sezonoleague.com

SEZONO League tanıtım sayfası — statik site, GitHub Pages üzerinden yayında.

- `index.html` — tek sayfa; TR/EN/ES metinleri sayfanın içindeki `I18N` sözlüğünde, varsayılan dil İngilizce.
- `img/` — uygulama ekran görüntüleri (iOS simülatör, İngilizce arayüz), marka işareti, favicon, OG görseli.
- `CNAME` — özel alan adı.

Kaynak parçalar ve derleyici (part1–4 + build.py) geliştirme makinesinde `~/Desktop/SEZONO-site/` altında durur;
`python3 build.py` tek dosyalık sürümü, `dist` adımı da bu repodaki yayın hâlini üretir.
