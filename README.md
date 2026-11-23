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
| Kapı / dolap / portmanto kapağı aç-kapat | kapıya, kasasına ya da üstündeki lentoya tıklama | dokunma | — |
| Tekli koltuğu / çalışma sandalyesini (V2) 45° döndür | koltuğa tıklama | dokunma | — |
| Kedileri göster / gizle | paneldeki **Kediler** anahtarı | dokunma | — |

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
             bina holü   ┃ 128×223  │  142 × 340   │
                ┌────────┘          ┊              │
                │ koridor 228×117   ┊              │
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
- **Koridor kısa kolu:** **228 × 117 cm**. Z = 117 (ölçülen 87 + 30). X, salon kapısının sol kenarından
  uzun kolun sağ duvarına kadar: duvarlarla ≈ 248 cm.
- **Koridor uzun kolu:** **128 × 223 cm**, kısa kolun üstünden yatak odası duvarına kadar. Sağ dış duvar düz kabul
  edildiğinde yatak odası kapısının sol kenarı koridorun sol duvarıyla aynı hizaya gelir.
- **Banyo (kalan alan):** genişlik 280 − 128 − 10 = **142 cm**, derinlik 117 + 223 = **340 cm**.
- **Kapı sırası:** koridorda yatak odasından salona doğru önce çelik kapı (sol duvar), sonra banyo kapısı
  (sağ duvar) gelir. Kapılar karşılıklı değil.
- **Banyo yerleşimi** (kapıdan girerken): sağdaki duvarda (çalışma odası tarafı) lavabo ve köşede üst üste
  çamaşır + kurutma makinesi; karşıdaki duvarda klozet, duvarın geri kalanı boş; soldaki duvarda (yatak odası
  tarafı) kapıya yakın köşede 90 × 90 duşakabin ve yanında örülmüş duvar (apartman boşluğu / şaft, 52 × 90).
  Banyo kapısı içe, duşakabin tarafına açılır; klozet kanadın süpürdüğü alanın dışında.
- **Yatak odası:** 280 × 256 cm (teyit edildi).
- **Kapılar:** boşluk 100 cm, yükseklik 215 cm. Kasa payı düşülünce kanat ≈ 90 cm, açıkken net geçiş ≈ 85 cm.
  Yatak odası ve çalışma odası kapıları açılınca yan duvara (Z eksenine) paralel durur.
- **Yükseklik:** odalar 260 cm, koridor asma tavanı 235 cm.

## Yerleşim versiyonları

Paneldeki **Versiyon 1 / Versiyon 2** seçicisiyle iki yerleşim arasında geçilir. Seçim tarayıcıda hatırlanır;
doğrudan bağlantı için adresin sonuna `#v1` ya da `#v2` eklenebilir. Mimari, salon, mutfak, koridor, banyo ve
balkon iki versiyonda aynıdır; yalnızca balkon tarafındaki oda (260 × 410) ile cadde tarafındaki oda (280 × 256)
eşyaları ve adları yer değiştirir.

### Ortak

- **Salon:** cam tarafındaki sol duvarda 120 × 35 × 200 kitaplık; kitaplığın 40 cm daha önünde tıklandıkça
  45° dönen tekli koltuk (salona, cama ya da kitaplığa çevrilebilir).
- **Açık mutfak:** ada tezgah, sol duvar tezgahı ve arka duvar tezgahı birleşik; sağa (salon kapısına) açılan
  U. Sol kolda evye ve üst dolaplar; arka kolda ankastre set (4 gözlü cam seramik ocak, altında 60 cm
  ankastre fırın, ocaktan 65 cm yukarıda bacalı paslanmaz davlumbaz), üst dolap ve buzdolabı.
- **Koridor:** kısa kolda salon kapısının tam karşısında 96 × 38 × 230 cm boydan portmanto (iki kapaklı,
  içinde şapkalık rafı ve askı borusu); çelik kapının yanındaki duvarda 64 × 176 cm boy aynası; çelik kapının
  karşısında ayakkabılık.

- **Balkon:** kedi kum kabı (50 × 38 × 14), korkuluğun üstünden kirişe kadar 10 cm aralıklı kedi koruma teli.
  Balkona açılan odanın sürgülü camında 22 × 26 cm kedi kapısı (geçiş 14 × 19), kedi geçerken sallanır.
- **Salon:** kanepenin karşısında, mutfak tarafında 44 × 44 tabanlı, 78 cm kedi tırmalama direği.
- **Çalışma masası (iki versiyonda):** klavye, mouse ve izolasyon pedlerinde kullanıcıya dönük iki adet
  3,5 inç referans hoparlör.

## Kediler

Üç kedi (bembeyaz, tekir, simsiyah) daire içinde kendi başına dolaşır. 10 cm'lik bir ızgarada mobilya ve
duvarlardan kaçınarak yol bulurlar; kapalı kapılardan geçemezler, balkona yalnızca kedi kapısından (ya da açık
balkon kapısından) çıkarlar. Kediler dolaşabilsin diye iki odanın kapısı açık başlar.

Davranışlar rastgele seçilir: yürüyerek gezinme, ani koşu, birbirini kovalama (kovalanan kaçar), oturma,
yalanma, ekmek pozisyonunda yatma, kanepede / tekli koltukta / yatakta / tırmalama direğinin tepesinde
uyuma, direği tırmalama, kum kabına gitme, balkonda dışarıyı seyretme. Uyurken nefes alır, dururken etrafa
bakınır ve göz kırparlar. Odaya odaklanıldığında odanın dışındaki kediler de soluklaşır.

### Versiyon 1 — çalışma odası balkon tarafında

- **Çalışma odası (260 × 410):** kapıdan girince soldaki duvarın köşesinde, iki duvara 2 cm mesafeyle
  150 × 150 × 5 cm platform; üzerinde EFNOTE 5 elektronik davul ve taburesi. Masanın sağında, masaya dik,
  tuşları sandalyeye bakan X standında Roland JUNO-Di (61 tuş, 100,8 × 30 × 10,4 cm). Salon duvarı boyunca
  sıralı gitar standında 4 gitar (1 akustik, 3 elektro).
- **Yatak odası (280 × 256):** sağ duvara yaslı 155 cm karyola; sol duvarda 150 × 60 × 220 üç kapaklı dolap.

### Versiyon 2 — odalar yer değiştirdi

- **Yatak odası (260 × 410, balkon tarafı):** 155 cm yatak, başlığı salon duvarının karşısındaki duvarda;
  balkon camının önünde 60 cm boşluk ve halı; komodin yok. Tavana kadar (255 cm) L gardırop: sağ duvar
  boyunca yataktan sonra 190 cm, köşeden dönüp kapı tarafındaki duvar boyunca oda kapısının kasasına kadar
  160 cm, derinlik 60 cm. Köşe iki kolun ortak iç hacmi; içinde askı boruları, kapı yanındaki bölmede 4 raf,
  üstte asma bölme. Beş sütunda altta uzun, üstte asma bölme kapağı olmak üzere 10 kapak; menteşeler köşeden
  uzakta, kapaklar odaya açılır.
- **Çalışma odası (280 × 256, cadde tarafı):** cam köşesinde 150 × 150 × 5 cm platform ve EFNOTE 5 (davulcu
  cama bakar); kapı duvarında X standında JUNO-Di, tuşları odaya bakar; klavyenin üstünde duvar askılarında
  4 gitar; sol duvarda 140 × 60 çalışma masası ve monitör; masanın önünde, ortasına hizalı, tıklandıkça 45°
  dönen çalışma sandalyesi.

## Ölçüleri değiştirme

`index.html` içindeki `M` nesnesi tek kaynak:

```js
const M = {
  wallIn: 10, wallEx: 20, height: 260, corridorCeiling: 235,
  doorGap: 100, doorHeight: 215,
  salon:    { w: 306, dLiving: 393, island: 50, dKitchen: 160 },
  study:    { w: 260, d: 410, topWall: 162 },
  corridor: { shortD: 117, longW: 128, longD: 223 },
  bedroom:  { w: 280, d: 256, straight: 120, niche: 60, nicheDepth: 5 },
};
```

Banyo ölçüsü girilmez: koridor ve yatak odası ölçülerinden kalan alan olarak hesaplanır.
Koridor ölçüldüğünde `corridor` değerlerini güncellemek yeterli.
