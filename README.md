# KINETIC ATLAS

Bağımlılıksız, herkese açık kurgusal bir SVG/scroll deneyimi. Sıcak kâğıt zeminde tek canlı aksan rengiyle ilerleyen büyük bir heykel; kaydırdıkça **Çizgi → Örgü → Akış → Patlama** evrelerine dönüşür.

## Özellikler

- Tek dosya: `index.html`; GitHub Pages kökünden doğrudan çalışır.
- Gerçek SVG manipülasyonu: scroll progress her evrede `path d`, düğüm koordinatları, merkez dairesi, halo, yörünge, beam ve burst çizgilerini günceller.
- Pointer/touch sürükleme: sahne üzerinde işaretçi veya parmakla heykeli kontrollü biçimde büker.
- `↻` düğmesi yeni bir varyasyon fazı üretir.
- Mobil menü, dokunma hedefleri, klavye odak stilleri, semantik heading yapısı ve ARIA açıklamaları.
- `prefers-reduced-motion: reduce` için animasyonları kapatan, anlamlı statik başlangıç sahnesini koruyan fallback.
- Harici font, görsel veya JavaScript bağımlılığı yok; Türkçe karakterler sistem fontlarıyla güvenli.
- Yatay taşmayı önlemek için `overflow-x: hidden`, akışkan ölçüler ve mobil breakpoint kullanılır.

## Yerelde çalıştırma

```bash
cd kinetic-atlas
python3 -m http.server 4173
# tarayıcı: http://127.0.0.1:4173/
```

Dosya statik olduğu için build/install adımı yoktur.

## Hızlı doğrulama

```bash
# HTML içindeki script'i çıkarıp JavaScript syntax kontrolü
python3 - <<'PY'
from pathlib import Path
import re
html = Path('index.html').read_text(encoding='utf-8')
script = re.search(r'<script>\s*(.*?)\s*</script>', html, re.S).group(1)
Path('kinetic-atlas-inline.js').write_text(script, encoding='utf-8')
PY
node --check kinetic-atlas-inline.js
rm kinetic-atlas-inline.js

# Ayrı bir terminalde sunucuyu başlattıktan sonra:
curl --fail --silent --show-error --output /dev/null --write-out '%{http_code}\n' http://127.0.0.1:4173/
```

## Kullanım

1. Sayfayı aşağı kaydırarak dört evreyi gez.
2. Sahne üzerinde sürükleyerek SVG heykelini bük.
3. Sağ alttaki `↻` düğmesiyle aynı kurallardan farklı bir varyasyon çıkar.
4. Mobilde `Atlas` menüsünü ve 01–04 evre kısayollarını kullan.
