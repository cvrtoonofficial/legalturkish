---
name: gizlilik-sozlesmesi-triyaj
description: Gelen bir gizlilik sözleşmesini (NDA) hızlıca tarar ve YEŞİL (standart onayla imzala), SARI (gözden geçir), KIRMIZI (esaslı sorun, müzakere veya karşı teklif) olarak sınıflandırır. Tek taraflı veya karşılıklı NDA, ticari sır içeren açıklamalar, rakip taraf, kontrol değişikliği gizliliği gibi senaryolarda kullanılır. Türk hukuku eksenli: TBK genel hükümler, TTK m.55/1-b haksız rekabet, TBK m.27 kesin hükümsüzlük denetimi.
---

# /turk-hukuk-legal:gizlilik-sozlesmesi-triyaj — NDA Triyajı

NDA: @$1

## Davet

```
/turk-hukuk-legal:gizlilik-sozlesmesi-triyaj [dosya | metin]
```

## İş Akışı

### Adım 1 — Belgeyi Al ve Tipi Belirle

Aşağıdaki ayrımları netleştir:

- **Tek taraflı (açıklayan tarafın korunması)** — sadece bir taraf bilgi açıklıyor
- **Tek taraflı (alan tarafın korunması)** — sadece bir taraf bilgi alıyor
- **Karşılıklı (mutual)** — iki taraf da bilgi açıklayıp alıyor
- **Bağımsız NDA mı, sözleşme içine gömülü gizlilik klozu mu?**

NDA'nın aslında bir NDA mı yoksa ticari yükümlülük taşıyan başka bir sözleşme mi olduğunu kontrol et — bazı sözleşmeler "NDA" başlığıyla gönderilse de aslında ön sözleşme, ortaklık taahhüdü vb. taşır.

### Adım 2 — Büro NDA Kılavuzunu Yükle

`buro.local.md` dosyasında tanımlı standartlar:

- Karşılıklı yapı tercihi (büro her ihtimalde karşılıklı mı istiyor?)
- Süre üst sınırı (genelde 2-3 yıl; ticari sır için 5+)
- Zorunlu istisnalar
- Kabul edilmeyen klozlar (örn. rekabet etmeme, çalışan ayartmama)
- Yetki ve uygulanacak hukuk tercihi

Kılavuz yoksa Türk piyasasında yaygın varsayımlarla devam et ve bunu belirt.

### Adım 3 — Sistematik Tarama

#### 3.1 Yapı

| Kontrol | Standart pozisyon |
|---|---|
| Tip | Karşılıklı tercih edilir (özellikle keşif görüşmelerinde) |
| Bağımsızlık | Standalone NDA olmalı |
| Tarafların yetkili temsili | İmza yetkisi belirgin olmalı |

#### 3.2 Gizli bilgi tanımı

| Kontrol | Standart pozisyon |
|---|---|
| Kapsam dar mı geniş mi | "Tüm bilgiler" tipi tanım fazla geniş; nesnel kriter gerek |
| İşaretleme şartı | Sözlü açıklama 30 gün içinde yazılı teyit kabul edilebilir |
| Standart istisnalar | Hepsi olmalı: kamuya açık, önceden bilinen, bağımsız geliştirilen, üçüncü kişiden alınan, kanunen açıklama zorunluluğu |

**Türk hukuku notu:** Tanım, **ticari sır kavramına** yakın çizilmelidir (TTK m.55/1-b ticari sırrın korunması). Çok geniş tanım, sözleşme tasfiyesinde uygulanması güç olur.

#### 3.3 Alan tarafın yükümlülükleri

| Kontrol | Standart pozisyon |
|---|---|
| Özen derecesi | Makul özen / kendi bilgisinin gördüğü özen |
| Kullanım amacı | Sözleşmede belirtilen amaçla sınırlı |
| Paylaşım sınırı | "Bilmesi gereken" çalışan/danışman + onlar da gizlilik altında |

#### 3.4 Standart istisnalar (Türk hukuku karşılıkları)

- ✅ Halka açık bilgi (alan tarafın kusuru olmadan)
- ✅ Açıklama öncesi sahip olunan bilgi
- ✅ Bağımsız geliştirilen bilgi (referans olmadan)
- ✅ Üçüncü kişiden hukuka uygun edinilen bilgi
- ✅ Kanunen açıklama zorunluluğu (mahkeme, idare; mümkünse açıklayan tarafa ön bildirim)

Eksikse SARI bayrak.

#### 3.5 Süre

| Süre | Değerlendirme |
|---|---|
| 1-3 yıl | Standart |
| 5 yıla kadar | Ticari sır iddiası varsa kabul edilebilir |
| Süresiz | Yalnızca ticari sırlar için; **genel bilgide süresiz gizlilik klozu TBK m.27 dengesizlik denetimi açısından sorunlu** |

#### 3.6 İade ve imha

| Kontrol | Pozisyon |
|---|---|
| Tetik | Sözleşmenin sona ermesi veya talep |
| Kapsam | Bilgi ve kopyaları |
| İstisna | Kanunen veya iç uyum amaçlı saklama (yedekleme, denetim) — açıkça yazılmalı |
| Tasdik | İmha tasdiki makul; noter onaylı yeminli beyan ağır |

#### 3.7 Çare ve yaptırımlar

- İhtarsız mahkemeden ihtiyati tedbir hakkı (HMK m.389+; FSEK/SMK özel hükümleri)
- Önceden belirlenmiş cezai şart (TBK m.179) **dikkatle değerlendir** — Türk hukukunda cezai şart hâkim takdiriyle indirilebilir (m.182) ama yine de bağlayıcıdır

#### 3.8 Sorunlu klozlar (KIRMIZI tetikleyiciler)

- 🔴 **Rekabet etmeme** klozu NDA'ya gömülü (rekabet etmeme ayrı bir hukuki çerçevedir — TBK m.444 vd. işçi rekabet yasağı, TTK m.55 ticari rekabet)
- 🔴 **Çalışan ayartmama** klozu (non-solicit) — NDA dışına çıkarılmalı
- 🔴 **Münhasırlık veya beklemede tutma (standstill)** klozu — sadece M&A bağlamında uygun
- 🔴 **"Artık bilgi (residuals)" klozu** geniş kapsamlı — fiilen lisans yaratır
- 🔴 **Fikri hak devri veya lisansı** — NDA'da olmamalı, ayrı sözleşmede ele alınmalı
- 🔴 **Süresiz veya 10+ yıl gizlilik** ticari sır gerekçesi olmadan

#### 3.9 Uygulanacak hukuk & uyuşmazlık

- Türk hukuku tercih edilir
- Mahkeme: HMK m.17-18 yetki kuralları + iki tarafın merkezleri
- Tahkim: ISTAC veya ICC kabul edilebilir; aşırı zor erişim noktası SARI
- Zorunlu arabuluculuk: 6325 SK m.18/A — ticari uyuşmazlıklarda dava şartı

#### 3.10 Klozlar arası etkileşim

- Geniş gizli bilgi tanımı + uzun süre + zayıf istisnalar = Pratik olarak kullanım yasağı yaratır → 🔴
- Karşılıklı NDA ama bir taraf lehine paylaşım hakları daha geniş = 🟡 asimetri

### Adım 4 — Sınıflandırma

#### 🟢 YEŞİL — Standart onayla imzala

Tüm aşağıdakiler doğruysa:
- Doğru tip (karşılıklı veya pozisyona uygun tek taraflı)
- Tüm standart istisnalar var
- Süre standart aralıkta (1-3 yıl, ticari sır için 5)
- Rekabet etmeme / çalışan ayartmama / münhasırlık YOK
- Residuals klozu yok veya dar
- Makul yetkili mahkeme
- Cezai şart yok veya makul (örn. tedbir + tazminat hakları saklı şartıyla)
- Çalışan ve danışmana paylaşım hakkı var
- İade / imha klozunda saklama istisnası var

**Aksiyon:** Yetki matrisi içindeki onaycıya iletilebilir; gözden geçirme gereksiz.

#### 🟡 SARI — Gözden geçirme gerekli

Aşağıdakilerden biri/birkaçı var, ama temelde çözülebilir:

- Gizli bilgi tanımı tercih edilenden geniş ama makul
- Süre standardın üstünde ama piyasa aralığında (örn. 5 yıl, ticari sırda 7)
- Bir standart istisna eksik ama kolayca eklenebilir
- Dar residuals klozu (yalnız "yardım almadan bellekte kalan genel bilgi")
- Kabul edilebilir ama tercih edilmeyen mahkeme
- Karşılıklı NDA'da küçük asimetri
- İşaretleme şartı var ama pratikte uygulanabilir
- Açık iç saklama istisnası eksik (zımni var ama eklenmeli)

**Aksiyon:** Tek tur redline ile çözülür; spesifik konular işaretlenmiş bir görev olarak iletilir.

#### 🔴 KIRMIZI — Esaslı sorun

- Karşılıklı olması gerekirken tek taraflı (veya yön yanlış)
- Kritik istisnalar eksik (özellikle bağımsız geliştirme veya kanunen açıklama)
- Rekabet etmeme / çalışan ayartmama / münhasırlık / standstill klozu
- Aşırı uzun veya süresiz, ticari sır gerekçesi yok
- Aşırı geniş tanım (kamuya açık veya bağımsız geliştirilen bilgiyi de kapsar)
- Geniş residuals klozu (fiilen lisans yaratır)
- Fikri hak devri/lisansı gömülü
- Belge aslında NDA değil

**Aksiyon:** İmzalamayın. Müzakere, büro standart NDA'sıyla karşı teklif, veya reddet.

### Adım 5 — Triyaj Raporu

```markdown
## NDA Triyaj Raporu

**Sınıflandırma:** [🟢 YEŞİL / 🟡 SARI / 🔴 KIRMIZI]
**Taraflar:** [...]
**Tip:** [Karşılıklı / Tek taraflı açıklayan / Tek taraflı alan]
**Süre:** [...]
**Uygulanacak hukuk:** [...]
**Değerlendirme dayanağı:** [Büro kılavuzu / Türk piyasası varsayımları]

### Tarama sonuçları
| Kriter | Durum | Notlar |
|---|---|---|
| Yapı | [✓/⚠/✗] | ... |
| Gizli bilgi tanımı | [✓/⚠/✗] | ... |
| Süre | [✓/⚠/✗] | ... |
| Standart istisnalar | [✓/⚠/✗] | ... |
| Sorunlu klozlar | [✓/⚠/✗] | ... |

### Tespit edilen sorunlar

#### Sorun 1 — [SARI/KIRMIZI]
**Ne:** [tanım]
**Risk:** [ne olabilir]
**Öneri:** [değişiklik metni veya yaklaşım]

### Tavsiye
[Spesifik sonraki adım]

### Sonraki adımlar
1. ...
2. ...
```

## Türk Hukuku İçin Pratik Notlar

**Cezai şart (TBK m.179-182):** NDA'larda cezai şart yaygın ama hâkim TBK m.182 uyarınca aşırı cezai şartı **indirir**. Karşı taraf bunu bildiği için cezai şart caydırıcılığı sınırlıdır; **ihtiyati tedbir + fiili tazminat** kombinasyonu pratikte daha etkilidir.

**Cezai şartın kümülatif veya seçimli olduğu:** TBK m.180 — cezai şart aksi belirtilmedikçe **alternatif olarak (ya cezai şart ya tazminat)** istenir. NDA tasarımında bu netleştirilmeli ("ek olarak istenir" yazılmalı).

**Haksız rekabet kümülatif koruma:** TTK m.54-63 NDA'dan bağımsız haksız rekabet hükümleri uygulanır; ticari sır ele geçirme (TTK m.55/1-b) suç ve haksız fiil teşkil eder. Bu, NDA klozu zayıf olsa da koruma sağlar.

**Çalışan rekabet yasağı:** TBK m.444 vd. (yer, konu, süre üst sınırı 2 yıl). Çalışan ile yapılan NDA'larda bu sınırların aşılmaması kritik. Müvekkil işveren ise rekabet yasağı klozu ayrı bir sözleşme veya ek protokol olarak alınmalı.

**Cumhurbaşkanlığı / kamu kurumu ile NDA:** Kamuda farklı çerçeveler işler (4734 KİK kapsamı dışındaki gizlilik anlaşmaları, Devlet Sırrı Kanunu Tasarısı'nın durumu). Kamu tarafıyla NDA varsa kıdemli kontrol şarttır.

## Notlar

- Belge gerçekten NDA değilse (örn. başlığı NDA ama içeriği ön sözleşme/işbirliği taahhüdü), bunu doğrudan KIRMIZI olarak işaretle ve tam sözleşme incelemesi öner.
- Daha büyük bir sözleşmenin parçası olan gizlilik klozları için, ana sözleşmenin bağlamı analizi etkiler — bu skill bağımsız NDA için optimizedir.
- Mevzuat doğrulama gerektiren konular `mevzuat_mcp` ile çekilir; içtihat ihtiyacı `yargi_mcp` ile karşılanır.
