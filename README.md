# Daire 3D Modeli

El çizimi ölçülerden üretilmiş, tarayıcıda çalışan tek sayfalık 3B daire modeli (Three.js).

## Çalıştırma

`index.html` dosyasını bir tarayıcıda açın. Three.js ve yazı tipleri CDN'den yüklendiği için internet bağlantısı gerekir.
Yerel sunucu isterseniz: `python3 -m http.server` → `http://localhost:8000`.

## Kontroller

| Eylem | Fare | Dokunmatik | Klavye |
|---|---|---|---|
| Evin ortasındaki pivot etrafında sağa-sola döndürme | sol tuşla yatay sürükleme | tek parmakla kaydırma | ← → |
| Bakış açısını eğme | dikey sürükleme | tek parmakla dikey kaydırma | ↑ ↓ |
| Yakınlaştırma | tekerlek | iki parmak | + − |
| Odaya odaklan | odaya tıklama | dokunma | — |
| Tüm daireye dön | boş alana ya da başka odaya tıklama | dokunma | Esc |
| Kapı aç / kapat | kapıya, kasasına ya da üstündeki lentoya tıklama | dokunma | — |

Paneldeki **Kapıları aç**, **Üstten bak**, **Sıfırla** düğmeleri ve **Etiketler** / **Mobilya** anahtarları da kullanılabilir.
Bir odaya tıklandığında kamera pivotunu o odanın merkezine alır, odayı kadraja sığdırır ve diğer odalar soluklaşır;
döndürme artık odanın merkezi etrafında olur. Boş alana ya da başka bir odaya tıklamak kamerayı dairenin merkezine
ve tüm daireyi gören uzaklığa geri getirir. Oda tablosundaki adlar da aynı odağı açıp kapatır.

## Yerleşim (plan, üstten; ölçekli taslak, 1 karakter ≈ 12 cm)

```
                          CADDE CEPHESİ
                         ┌──── sürgülü boydan cam ─┐
                         │                         │
                         │                         │
                         │      YATAK ODASI        │
                         │      280 × 256          │
                         │                         │
                         ├ kapı    ─┬──────────────┤
            çelik kapı   ┃ KORİDOR  │    BANYO     │
             bina holü   ┃ 128×223  │  142 × 320   │
                ┌────────┘          ┊              │
                │ koridor 228×97    ┊              │
┌───────────────┴─ kapısız─┬ kapı   ┴──────────────┤
│  AÇIK MUTFAK             │                       │
│  306 × 160               │     ÇALIŞMA ODASI     │
│   ── ada tezgah 50 ──    │     260 × 410         │
│  SALON                   │                       │
│  306 × 393               │                       │
│                          ├─── sürgülü cam ───────┤
│              balkon      ┊      BALKON           │
│               kapısı →   ┊    260 × 193          │
└───── boydan cam ─────────┴────── korkuluk ───────┘
                       AĞAÇLIK ALAN CEPHESİ
```

Bağlantılar: Salon → Koridor (kapısız boşluk) · Salon → Balkon (cam kapı) · Çalışma odası → Koridor (kapı) ·
Çalışma odası → Balkon (sürgülü cam) · Banyo → Koridor (kapı) · Yatak odası → Koridor (kapı) · Koridor → Dış kapı (çelik kapı).

## Hesaplar

Tüm ölçüler cm ve iç yüzden iç yüze. Sahnede 1 birim = 1 cm.

- **Duvarlar:** iç bölme 10 cm, cephe ve komşu duvarlar 20 cm.
- **Salon bloğu (Z):** salon 393 + ada tezgah 50 + açık mutfak 160 = **603 cm**. İlk ölçülerde ada tezgahın
  yeri sayılmamıştı; 50 cm'lik pay tahmini (50–60).
- **Balkon:** 603 − 410 = **193 cm** derinlik, çalışma odasıyla aynı 260 cm genişlik.
- **Çalışma odası kapısı:** 260 − 162 = 98 cm boşluk, salon tarafındaki köşede.
- **Koridor kısa kolu:** **228 × 97 cm**. Z = 97 (ölçülen 87 + 10). X, salon kapısının sol kenarından
  uzun kolun sağ duvarına kadar: duvarlarla ≈ 248 cm.
- **Koridor uzun kolu:** **128 × 223 cm**, kısa kolun üstünden yatak odası duvarına kadar. Sağ dış duvar düz kabul
  edildiğinde yatak odası kapısının sol kenarı koridorun sol duvarıyla aynı hizaya gelir.
- **Banyo (kalan alan):** genişlik 280 − 128 − 10 = **142 cm**, derinlik 97 + 223 = **320 cm**.
- **Kapı sırası:** koridorda yatak odasından salona doğru önce çelik kapı (sol duvar), sonra banyo kapısı
  (sağ duvar) gelir. Kapılar karşılıklı değil.
- **Banyo yerleşimi** (kapıdan girerken): sağdaki duvarda (çalışma odası tarafı) lavabo ve köşede üst üste
  çamaşır + kurutma makinesi; karşıdaki duvarda klozet, duvarın geri kalanı boş; soldaki duvarda (yatak odası
  tarafı) kapıya yakın köşede duşakabin.
- **Yatak odası:** 280 × 256 cm (teyit edildi).
- **Kapılar:** boşluk 100 cm, yükseklik 215 cm. Kasa payı düşülünce kanat ≈ 90 cm, açıkken net geçiş ≈ 85 cm.
  Yatak odası ve çalışma odası kapıları açılınca yan duvara (Z eksenine) paralel durur.
- **Yükseklik:** odalar 260 cm, koridor asma tavanı 235 cm.

## Ölçüleri değiştirme

`index.html` içindeki `M` nesnesi tek kaynak:

```js
const M = {
  wallIn: 10, wallEx: 20, height: 260, corridorCeiling: 235,
  doorGap: 100, doorHeight: 215,
  salon:    { w: 306, dLiving: 393, island: 50, dKitchen: 160 },
  study:    { w: 260, d: 410, topWall: 162 },
  corridor: { shortD: 97, longW: 128, longD: 223 },
  bedroom:  { w: 280, d: 256, straight: 120, niche: 60, nicheDepth: 5 },
};
```

Banyo ölçüsü girilmez: koridor ve yatak odası ölçülerinden kalan alan olarak hesaplanır.
Koridor ölçüldüğünde `corridor` değerlerini güncellemek yeterli.
