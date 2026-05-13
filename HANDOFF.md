# Nil Pansiyon v2 — Handoff

**Tarih:** 2026-05-13 · **Branch:** main · **Local URL:** http://localhost:8765
**Live (eski):** https://nilpansiyon.info (Lovable Vite SPA — değiştirilecek)

## Kullanıcı (Kaan)

- Pansiyon Uzungöl/Çaykara'da, **kuzeninin işletmesi**. Site kuzene "yaraşacak", "daha önce görülmemiş eşsizlikte" olacak.
- Eski site (`golden-uzungol-palace` repo, React/Lovable) **1.5/10** olarak puanlandı, gerekçe: jenerik.
- **Trabzonlu/Arap zenginler dolu sever, minimal sevmez** — luxe + natural + custom hedef.
- Son durum (Kaan'ın değerlendirmesi): **"6/10 oldu sonunda"**. Hedef: **"best looking website"** + **"mobile cinematic experience"**.

## Şu anki dosya yapısı

```
/Users/ozai/projects/nilpansiyon-v2/
├── index.html                      ← tek dosya, ~3360 satır (tüm CSS+JS inline)
├── manifest.webmanifest             ← PWA manifest
├── assets/
│   ├── img/  (18 jpg + logo.png — eski v1'den çekildi)
│   └── video/ (3 oda tour mp4)
└── _reference/
    ├── old-bundle.js                ← eski sitenin minified JS bundle'ı
    ├── old-v1/                      ← `golden-uzungol-palace` clone — eski site
    └── orijinal asset kopyaları
```

## Site mimarisi (sıralı)

1. **Hero** — cross-fade 4 foto (Uzungöl kuş bakışı vs), custom cursor, falling spruce needles, "EST · 1987 · UZUNGÖL" eyebrow, devasa italic "nil pansiyon" tek satır, tagline, sub strip
2. **Manifesto** — 3 stanza şiir (sabah çayın buğusu / öğle ladin / akşam bulut), mandala SVG ornament, çay buharı SVG (sağda animated)
3. **Stats ribbon** — ince şerit: 12 oda · 30 m göl · 1090 m rakım · 3 dil
4. **Odalar** — 6 oda asimetrik editorial grid, **r1/r2/r3 üzerinde hover'da video preview** (Deluxe / 2+1 / 1+1)
5. **Sofra** — paper bg, 7 yemek menüsü (mıhlama, kuymak, karalâhana, hamsi, köy ekmeği, fındık tatlısı, çay)
6. **Hikâye** — pansiyon dış cephe fotosu + 2 col anlatı + signature "Nil Ailesi"
7. **Mevsim** — 4 kart (ilkbahar/yaz/sonbahar/kış) gradient bg + ornament SVG + sıcaklık
8. **Konum** — adres + 7 mesafe + custom SVG harita (göl dalgaları + pin pulse + kontur draw + road dash flow) + Google Maps deeplink
9. **Misafir defteri** — 4 testimonial (Booking 10/10, Tripadvisor, Google 5/5, Instagram)
10. **Rezervasyon** — custom date picker + guest counter + oda tercihi → WhatsApp deeplink (+90 545 384 28 29)
11. **Awards marquee** — Booking · Tripadvisor · NatGeo · Hürriyet · Atlas · Conde Nast (kayan italic Fraunces)
12. **Footer** — mark + iletişim + adres + sayfa linkleri + "nil" watermark

## Yatay özellikler (her bölümde aktif)

- **Custom cursor** (brass dot + ring, mix-blend difference, hover'da büyür)
- **Cursor halo** (600px radial gold light, lag-follow, mix-blend screen)
- **Boot screen** (1.4s "nil · pansiyon" hoşgeldin)
- **Grain overlay** (SVG fractal noise + jitter)
- **Mist layers** (radial gradients, drift animation)
- **Section nav dots** (sağ kenar 11 brass nokta, IO ile aktif olan büyür)
- **Sticky booking bar** (hero geçince çıkar, footer/rez yakınında gizlenir)
- **WhatsApp FAB** (sağ alt, sticky bar varken gizlenir)
- **Custom gold scrollbar**
- **Falling spruce needles** (hero'da subtle)
- **Reveal-on-scroll** (IntersectionObserver, 72+ element)

## Renk paleti (kararlı)

```
--ink:        #07080A     ← gece, hero/odalar/rez/footer
--paper:      #F5EEDC     ← cream, manifesto/sofra/hikaye/mevsim/konum/defter
--paper-2:    #EBE2CA     ← cream-2
--gold:       #C8A45C     ← brass accent ana
--gold-hi:    #E8C988     ← brass parlak
--gold-deep:  #8E6B30     ← brass koyu
--moss:       #16201A     ← derin yeşil — accent only
--bordo:      #5C1F22     ← bordo — accent only (kaldırıldı çoğunlukla)
```

## Tipografi

- **Display**: Fraunces (italic, variable axes — opsz 60-144, SOFT 0-100, WONK 0-1, wght 200-360)
- **Body**: Lora
- **Mono**: IBM Plex Mono (label/eyebrow/mesafe için)

## Sonraki session için NET HEDEFLER

Kaan'ın açık talepleri:

1. **"Best looking website"** — hâlâ 6/10. 9/10+'a çıkması için:
   - Hero'yu daha sinematik yap (video bg seçeneği? veya layered photo with depth?)
   - Manifesto'yu daha vurucu hale getir (typography reveal animations, gold detay)
   - Mevsim kartlarına gerçek mevsim fotoğrafları (bg'lere — şu an gradient only)
   - Hikâye section'ında photo'ya parallax + caption frame
   - Award marquee'ye gerçek logo SVG'leri (şu an text only)
   - Defter testimonials carousel (4 → 8-10) + foto avatarlar

2. **"Mobile cinematic experience"** — şu an mobile responsive ama "cinematic" değil:
   - Hero mobilde portrait optimize (title boyutu, photo focal point)
   - Asimetrik odalar grid mobilde tek-sütun ama her oda full-bleed cinema gibi
   - Mevsim 4-kart mobilde horizontal-scroll snap-points (paginated)
   - Sticky bar mobile özel davranış
   - Custom cursor mobil'de yok (zaten kapalı), bunun yerine swipe affordance göstergeler

3. **Maps açılsın** — Konum section'da "Google Maps'te aç" CTA çalışıyor (`target="_blank"`). Eğer **embed** isteniyorsa, SVG map altına Google Maps iframe ekle. Şu an Kaan onayladı bence ama belki iframe istiyor.

## İlgili kişi / İletişim

- **Pansiyon WhatsApp**: +90 545 384 28 29
- **Email**: info@nilpansiyon.com
- **Adres**: İnönü Cd. No 92/A, Uzungöl, 61940 Çaykara / Trabzon
- **GitHub repo**: `ozzaii/nilpansiyon-v2` (boş, henüz push edilmedi)

## Komutlar

```bash
# local dev (no build step — tek HTML)
cd ~/projects/nilpansiyon-v2
python3 -m http.server 8765
# → http://localhost:8765

# git
git log --oneline
# bdabb14 ... ← initial commit

# eski v1 referansı için
ls _reference/old-v1/
```

## Önemli notlar / tuzaklar

- **`html { scroll-behavior: smooth }`** — JS'ten `window.scrollTo(0, x)` çağrıları yumuşak scroll yapıyor. Hızlı test için JS'te `document.documentElement.style.scrollBehavior='auto'` set et.
- **Boot screen 1.45s** delay — testlerde ilk 2s'i bekle.
- **Reveal observer rootMargin '0px 0px 120px 0px'** — instant scroll'da bazen tetiklenmiyor; ihtiyaç olursa init'te tüm in-viewport reveals'a `.in` zorla.
- **Hero photos cross-fade her 7.2s** — `.bg-photo.active` class değişir.
- **`<button>` ve `<a>` elements use `cursor: none` desktop'ta** — touch'ta `auto`'ya geri döner via media query.
- **WhatsApp FAB ve sticky-bar overlap riski** — MutationObserver ile WA FAB sticky-bar.shown varken gizleniyor.
- **Background agent çalışırken dosya konflict** — index.html'i aynı anda hem ana session hem bg agent edit ederse merge çakışır. Sırayla.

## Hızlı checklist — bir sonraki session

- [ ] Hero'da video arka plan seçeneği test et (3 oda tour video'sundan birini muted+loop hero bg yap)
- [ ] Mevsim kartlarına gerçek bg foto bul/ekle (Unsplash veya Pixabay Uzungöl/Karadeniz mevsim)
- [ ] Defter'i 8+ testimonial carousel'a çevir (auto-rotate, swipe)
- [ ] Mobil cinematic — hero portrait crop, mevsim horizontal-scroll
- [ ] Awards marquee'ye SVG logoları ekle (Booking, Tripadvisor, NatGeo brand marks)
- [ ] Manifesto sağ stanza'ya per-stanza reveal stagger
- [ ] Konum SVG map'e zoom-on-hover veya Google Maps iframe ek
- [ ] Performans test — Lighthouse, 90+ hedef
- [ ] Deploy planı — Netlify/Vercel/Cloudflare Pages + `nilpansiyon.info` domain swap

## Last actions before handoff

- Maps butonu doğrulandı: `target="_blank"` ile yeni sekme açar ✓
- HANDOFF.md yazıldı ✓
- Initial commit yapıldı: `bdabb14` ✓
- Next commit (hero rebuild + manifesto/mevsim polish + handoff) — bu mesajdan sonra atılacak

---

## 🔥 PROMPT — Bir sonraki Claude'a görev

> Kaan'ın **kuzeninin** Uzungöl'deki Nil Pansiyon'u için ÇOK ÖZEL bir site yapıyoruz. Site dünyanın en güzel görünen, en custom, en pahalı hisseden boutique pansiyon sitesi olacak. Kuzen Trabzonlu — minimal sevmez, dolu/lüks sever (Arap/Trabzon zenginleri estetiği).
>
> **Şu ana kadar 6/10.** Senin görevin **10/10'a çıkarmak.**
>
> ### Tek dosya, tek HTML
> `~/projects/nilpansiyon-v2/index.html` — CSS+JS inline. **Build step yok.** `python3 -m http.server 8765` → `localhost:8765`.
>
> ### MUTLAK kurallar
> - **NO**: cliche purple gradients, Playfair/Inter/Cormorant fontları, generic AI aesthetics, başka library/build sistemi getirme.
> - **YES**: Fraunces variable axes (italic, opsz 144, SOFT 100, WONK 1, wght 280-360), Lora body, IBM Plex Mono labels. Palette: --ink #07080A, --paper #F5EEDC, --gold #C8A45C, --gold-deep #8E6B30. Bordo/moss accent only.
> - **CUSTOM ANIMATIONS** her yerde — software kurallarını aşan kostüm motion. Slow easings (1-2s). transform+opacity tercih. mix-blend-mode kullan. SVG draw-on-scroll.
> - **EXPENSIVE LOOKING DETAILS** — ince hairlines, gold textur, paper grain, refined typography pairs, custom cursor/halo, lived-in lush feeling.
> - **MOBILE CINEMATIC** — sadece responsive değil, mobilde de cinematic. Hero portrait crop, oda kartları full-bleed swipe, mevsim horizontal scroll-snap, sticky bar uyumlu.
>
> ### Spesifik üst-seviye işler (sırayla)
> 1. **Hero**'yu sinematize et: belki bir oda tour video'sunu muted+loop+heavily-blurred hero bg yap, üstünde tek satır italic title. Veya layered photo with parallax depth (foreground, midground, background layers).
> 2. **Manifesto**'yu vurucu hale getir: her stanza ayrı reveal, gold detay, sağdaki çay buharı SVG'sini daha belirgin yap.
> 3. **Odalar**'da hover'da Roman numeral I-VI floating + caption frame; oda kartları hover'da subtle scale + lift + brass border.
> 4. **Sofra**'da yemek isimleri hover'da italic glow, tag pulse.
> 5. **Hikâye** photo'ya parallax + frame caption.
> 6. **Mevsim** kartlarına GERÇEK mevsim fotoğrafları bul/ekle (Karadeniz mevsim photography). Hover'da kart genişler ve çoklu detay açılır.
> 7. **Konum** map'i daha derin SVG illustration veya Google Maps embed alternatifi olarak iframe.
> 8. **Defter**'i 8-10 testimonial carousel + auto-rotate + foto avatar (gerçek avatar yok, gradient initials kullan).
> 9. **Awards**'a SVG logoları (Booking/Tripadvisor/NatGeo).
> 10. **Footer**'a custom signature (yaprak/ladin pattern).
>
> ### Test akışı
> 1. Local server aç (`python3 -m http.server 8765`)
> 2. Tarayıcıda browse, hover/click test, mobile emulator
> 3. Kaan'a screenshot/canlı göster, geri bildirim al, iterate
> 4. Lighthouse 90+ hedef
>
> ### İletişim
> Kaan "knk" der, Türkçe/İngilizce mix, küfür OK, övgü yok, direkt konu. Kuzenin gönlünün hoş olması — emotional stake yüksek. Detaylar matters; her bir milimetre matters.
>
> **`assets/img/` ve `assets/video/` tam dolu — yeni asset eklersen oraya.** Eski v1 referansı `_reference/old-v1/`.
