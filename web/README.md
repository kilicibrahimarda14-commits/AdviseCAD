# AdviseCAD — Kurumsal Web Sitesi

2 boyutlu CNC lazer kesim süreçleri için geliştirilen AdviseCAD yazılımının tanıtım
sitesi. Saf **HTML + CSS** ile yazılmıştır — framework, derleme adımı ve bağımlılık yoktur.

## Çalıştırma

`index.html` dosyasına çift tıklamanız yeterli. Yerel sunucu tercih ederseniz:

```
npx serve web
```

## Dosya yapısı

```
web/
├── index.html            Ana sayfa (hero, özellikler, örnek çıktı, süreç, SSS)
├── ozellikler.html       5 özellik + manuel yöntem karşılaştırma tablosu
├── nasil-calisir.html    4 adımlı süreç + zaman karşılaştırması
├── fiyatlandirma.html    3 paket + özellik tablosu + SSS
├── hakkimizda.html       Marka hikayesi, ilkeler, misyon/vizyon
├── iletisim.html         İletişim formu + bilgiler
├── indir.html            İndirme, sistem gereksinimleri, kurulum, sürüm notları
├── 404.html              Sayfa bulunamadı
├── robots.txt, sitemap.xml
├── css/
│   ├── tokens.css        Renk, tipografi, boşluk, gölge — TEK KAYNAK
│   ├── base.css          Reset, tipografi, odak, bölüm ve grid yardımcıları
│   ├── layout.css        Üst menü (JS'siz mobil menü) ve alt bilgi
│   ├── components.css    Buton, kart, rozet, tablo, form, akordiyon
│   ├── pages.css         Sayfa başlığı, karşılaştırma, süreç, özellik satırları
│   └── blocks.css        İstatistik şeridi, fiyat kartları, iletişim, indirme, CTA
├── assets/               logo dosyaları + favicon.svg
└── downloads/            Kurulum dosyasının konacağı klasör (README.txt'e bakın)
```

## Logo

Marka kilidi (mark + "AdviseCAD" + slogan) tek görsel olarak kullanılır. Kaynak
logodan şeffaf zeminli olarak kırpılıp web çözünürlüğüne indirilmiştir.

| Dosya | Nerede kullanılır | Boyut |
|---|---|---|
| `assets/logo.png` | Üst menü — açık zeminler | 668 × 176 |
| `assets/logo-light.png` | Alt bilgi — koyu zeminler | 668 × 176 |
| `assets/logo-mark.png` | Yalnız mark gerekirse (açık zemin) | 208 × 176 |
| `assets/logo-mark-light.png` | Yalnız mark gerekirse (koyu zemin) | 208 × 176 |

Görüntülenme yüksekliği [css/layout.css](css/layout.css) içindeki `.logo__img`
kuralındadır: üst menüde 40px (tablette 34px, dar ekranda 30px), alt bilgide 52px.

## Tasarımı değiştirme

Renk, yazı tipi, boşluk ve köşe yarıçapı gibi değerlerin **hepsi**
[css/tokens.css](css/tokens.css) içindedir. Marka rengini değiştirmek için
`--green-*` skalasını düzenlemeniz yeterlidir; site genelinde her yere yansır.
HTML veya diğer CSS dosyalarında doğrudan renk kodu yazılmamıştır.

Mevcut palet **doğrudan logodan örneklenmiştir**:

| Değer | Kaynak |
|---|---|
| `--green-700: #034642` | Logo markının gövde tonu |
| `--green-600: #045e57` | Logodaki "CAD" harfleri |
| `--green-500: #06776e` | Slogan ayraç çizgisi |
| `--ink-900: #121b28` | Logodaki "Advise" yazısının laciverti |

Logo değişirse bu dört değeri yeni logodan ölçüp güncellemek, sitenin tamamını
yeni markaya taşımak için yeterlidir.

## JavaScript kullanılmayan yerler

Site bilinçli olarak JavaScript'siz yazıldı. Normalde JS gerektiren şeyler şu
şekilde çözüldü:

| İşlev | Çözüm |
|---|---|
| Mobil menü | Gizli `checkbox` + `label` (`css/layout.css`) |
| Akordiyon / SSS | Tarayıcının kendi `<details>` / `<summary>` öğeleri |
| Scroll animasyonları | CSS `animation-timeline: view()` — desteklemeyen tarayıcıda içerik normal görünür |
| Hero'daki lazer kesim animasyonu | SVG `stroke-dashoffset` + CSS keyframes |
| Form doğrulama | HTML5 `required`, `type="email"`, `minlength` |

Tüm animasyonlar işletim sistemindeki **"hareketi azalt"** ayarına saygı duyar.

## YAPILACAKLAR — yayına almadan önce

1. **Kurulum dosyası.** `downloads/` klasörüne `AdviseCAD-Setup.exe` dosyasını koyun.
   Ayrıntı için [downloads/README.txt](downloads/README.txt).
2. **Sürüm bilgileri.** `indir.html` içindeki sürüm numarası, dosya boyutu ve yayın
   tarihi alanları şu an yer tutucudur (`1.0.0`, `— MB`, `—`).
3. **İletişim bilgileri.** Telefon (`+90 (000) 000 00 00`) ve adres alanları yer
   tutucudur. `iletisim.html` ve tüm sayfaların alt bilgisinde geçer.
4. **İletişim formu.** Şu an sunucu tarafı olmadığı için `mailto:` ile kullanıcının
   e-posta programını açar. Gerçek gönderim için `iletisim.html` içindeki `<form>`
   etiketinin `action` değerini kendi uç noktanızla değiştirin (dosyada açıklama
   satırı olarak belirtilmiştir).
5. **Alan adı.** `canonical`, `og:url` ve `sitemap.xml` içinde
   `https://www.advisecad.com` varsayılmıştır; farklıysa güncelleyin.
6. **Örnek rakamlar.** Ana sayfa, Özellikler ve Nasıl Çalışır sayfalarındaki maliyet
   ve ölçüm değerleri temsilî örneklerdir; sayfalarda bu durum açıkça belirtilmiştir.

## Sonraki adım — çoklu dil

Sitedeki tüm metinler `data-i18n="anahtar"` öznitelikleriyle işaretlenmiştir.
İleride JavaScript eklendiğinde, bir çeviri sözlüğü ve küçük bir motor dosyasıyla
8 dil (TR, EN, DE, FR, ES, IT, RU, AR) devreye alınabilir; HTML'e yeniden dokunmak
gerekmez. Arapça için sağdan sola düzen gerekeceğinden CSS boyunca mantıksal
özellikler (`margin-inline-start`, `padding-inline` vb.) kullanılmıştır.
