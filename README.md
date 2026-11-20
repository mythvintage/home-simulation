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
| Kapı aç / kapat | kapıya, kasasına ya da üstündeki lentoya tıklama | dokunma | — |

Paneldeki **Kapıları aç**, **Üstten bak**, **Sıfırla** düğmeleri ve **Etiketler** / **Mobilya** anahtarları da kullanılabilir.
Oda tablosunda bir oda adına tıklamak kamerayı o odaya odaklar; **Sıfırla** pivotu evin ortasına geri getirir.

## Yerleşim (plan, üstten; ölçekli taslak, 1 karakter ≈ 12 cm)

```
                          CADDE CEPHESİ
                         ┌──── sürgülü boydan cam ─┐
                         │                         │
                         │                         │
                         │      YATAK ODASI        │
                         │      280 × 258          │
                         │                         │
                         ├ kapı    ─┬──────────────┤
            çelik kapı   ┃ KORİDOR  │              │
             bina holü   ┃          ┊    BANYO     │
                ┌────────┘          ┊  152 × 250   │
                │ koridor 218×87    │              │
┌───────────────┴─ kapısız─┬ kapı   ┴──────────────┤
│  AÇIK MUTFAK             │                       │
│  306 × 160               │     ÇALIŞMA ODASI     │
│   ── ada tezgah ──       │     260 × 410         │
│  SALON                   │                       │
│  306 × 393               │                       │
│                          ├─── sürgülü cam ───────┤
│              balkon      ┊      BALKON           │
│               kapısı →   ┊    260 × 143          │
└───── boydan cam ─────────┴────── korkuluk ───────┘
                       AĞAÇLIK ALAN CEPHESİ
```

Bağlantılar: Salon → Koridor (kapısız boşluk) · Salon → Balkon (cam kapı) · Çalışma odası → Koridor (kapı) ·
Çalışma odası → Balkon (sürgülü cam) · Banyo → Koridor (kapı) · Yatak odası → Koridor (kapı) · Koridor → Dış kapı (çelik kapı).

## Hesaplar

Tüm ölçüler cm ve iç yüzden iç yüze. Sahnede 1 birim = 1 cm.

- **Duvarlar:** iç bölme 10 cm, cephe ve komşu duvarlar 20 cm.
- **Açık mutfak:** 553 − 393 = 160 cm derinlik.
- **Balkon:** 553 − 410 = 143 cm derinlik, çalışma odasıyla aynı 260 cm genişlik.
- **Çalışma odası kapısı:** 260 − 162 = 98 cm boşluk, salon tarafındaki köşede.
- **Koridor kısa kolu (X):** salon kapısı 100 + ortak duvar 10 + çalışma kapısı 98 + 10 pay = **218 cm** iç ölçü,
  duvarlarla ≈ 238 cm (verdiğiniz 220–240 aralığında). Z = 87 cm.
- **Banyo genişliği:** çalışma odası üst duvarı 162 − koridor duvarı 10 = **152 cm**.
  Sağlama: yatak odası 280 − koridor uzun kolu 118 − duvar 10 = 152 cm.
- **Koridor uzun kolu:** 118 cm genişlik. Sağ dış duvar düz kabul edildiğinde yatak odası kapısının sol kenarı
  koridorun sol duvarıyla aynı hizaya gelir.
- **Banyo derinliği ve koridor uzunluğu:** ölçü yok; **250 cm** tahmin edildi. Bu, uzun kolda çelik kapının
  (banyo kapısının karşı duvarında, banyo kapısı ile yatak odası arasında) sığması için gereken uzunluğu sağlıyor.
- **Kapılar:** boşluk 100 cm, yükseklik 215 cm. Kasa payı düşülünce kanat ≈ 90 cm, açıkken net geçiş ≈ 85 cm.
  Yatak odası ve çalışma odası kapıları açılınca yan duvara (Z eksenine) paralel durur.
- **Yükseklik:** odalar 260 cm, koridor asma tavanı 235 cm.

### Dikkat: yatak odası derinliği

Mesajda yatak odası için Z = **173** cm yazıyor, çizimde ise **258** yazıyor (görselin adı da `IMG_0173`).
Modelde çizimdeki **258** kullanıldı. Değiştirmek için `index.html` içinde `M.bedroom.d` değerini düzenleyin;
plan, etiketler ve alan tablosu otomatik olarak yeniden hesaplanır.

## Ölçüleri değiştirme

`index.html` içindeki `M` nesnesi tek kaynak:

```js
const M = {
  wallIn: 10, wallEx: 20, height: 260, corridorCeiling: 235,
  doorGap: 100, doorHeight: 215,
  salon:    { w: 306, dTotal: 553, dLiving: 393 },
  study:    { w: 260, d: 410, topWall: 162 },
  corridor: { shortD: 87 },
  bedroom:  { w: 280, d: 258, straight: 120, niche: 60, nicheDepth: 5 },
  bathroom: { d: 250 },   // tahmini
};
```

Banyo ve koridor uzunluğu ölçülünce `bathroom.d` güncellenmesi yeterli.
