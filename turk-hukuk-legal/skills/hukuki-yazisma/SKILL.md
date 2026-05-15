---
name: hukuki-yazisma
description: Sık karşılaşılan hukuki sorgu/talep türlerine yapılandırılmış yanıt taslakları hazırlar — KVKK ilgili kişi başvurusu yanıtı, ihtarname yanıtı, savcılık ve mahkeme bilgi yazısı, kamu kurumu yazısı, kira ihtilafı yanıt, KEP bildirimi şablonu. Şablon yanıt uygun olmayan durumlar için eskalasyon kontrolü içerir.
argument-hint: "[yanıt tipi]"
---

# /turk-hukuk-legal:hukuki-yazisma — Hukuki Yanıt Şablonları

## Davet

```
/turk-hukuk-legal:hukuki-yazisma [yanıt-tipi]
```

Yaygın yanıt tipleri:
- `kvkk-basvuru` — KVKK ilgili kişi başvurusu yanıtı
- `ihtarname-yanit` — Karşı taraftan gelen ihtarnameye yanıt
- `savci-bilgi` — Savcılık veya mahkeme bilgi yazısı yanıtı
- `kamu-kurum` — Düzenleyici kurum sorgusu yanıtı (BDDK, KVKK, Rekabet, vb.)
- `kira-uyusmazlik` — Kira sözleşmesi uyuşmazlığı yazışması
- `tedarikci-soru` — Tedarikçi sözleşme sorgusu yanıtı
- `kep-bildirim` — Resmi tebligat amaçlı KEP gönderim taslağı
- `ozel` — Özel şablon kullan

Tip belirtilmezse mevcut tipleri göster ve sor.

## İş Akışı

### Adım 1 — Yanıt tipini ve karşı tarafı belirle

- Hangi tip yanıt?
- Kim göndermiş? (kişi / şirket / kurum / mahkeme / savcılık)
- Hangi belge geldi? (ihtarname / istem yazısı / soruşturma yazısı)
- Müvekkilin pozisyonu nedir?
- Cevap son tarihi var mı?

### Adım 2 — Şablonu yükle

`buro.local.md` veya ayrı şablon dizininden ilgili şablonu bul. Yoksa, varsayılan şablon yapısıyla devam et ve büroya saklamasını öner.

### Adım 3 — Eskalasyon tetikleyicilerini kontrol et

Şablon yanıt **uygun olmayan** durumlar:

#### Genel
- Konu cezai sorumluluk doğurabilir
- Düzenleyici kurum veya kolluk hâlihazırda soruşturma açmış
- Yanıt bağlayıcı bir taahhüt veya haktan vazgeçme yaratabilir
- Medya ilgisi var veya ihtimali yüksek
- Konu daha önce büroda işlenmemiş bir vakıa
- Çoklu yargı yeri / sınır ötesi boyut
- Yönetim kurulu veya yöneticiler kişi olarak etkileniyor

#### KVKK ilgili kişi başvurusu
- Başvuru reşit olmayan kişinin verisi hakkında
- Başvuru KVKK Kurulu adına yapılmış (kurum sorgusu)
- Veri litigation hold (delil koruma) kapsamında
- Başvurucu mevcut/eski çalışan ve aktif iş anlaşmazlığı var
- Başvuru anormal şekilde geniş (fishing expedition izlenimi)
- Özel nitelikli veri içeriyor (sağlık, biyometrik, vb.)

#### İhtarname yanıtı
- İhtarname uzlaşmaz pozisyonda; karşı tarafın dava açma sinyali güçlü
- Konu önceki bir yargı kararıyla ilişkili
- Konu basın yansıması yaratabilir
- Karşı taraf büyük resmi kurum / ünlü şirket / siyasi figür

#### Savcılık / mahkeme bilgi yazısı
- **Her zaman kıdemli denetim gerekir** (şablon başlangıç noktası)
- Müvekkille avukat-müvekkil iletişimi varsa imtiyaz iddiası değerlendirilmeli
- Üçüncü kişi verisi içerirse
- Sınırötesi belge talebi varsa
- Makul olmayan kısa süre verilmişse

#### Kamu kurum / düzenleyici
- Yanıt müvekkilin mevzuata aykırılık iddiasına yol açabilir
- İdari para cezası riskine yol açabilir
- Sektörel kurumun yetki sınırı tartışmalı
- Tekzip veya genel duyuru sonucu doğurabilir

**Tetikleyici bulunursa:**
1. Şablon yanıtı **üretme**
2. Hangi tetikleyici tespit edildi, açıkla
3. Önerilen eskalasyon yolunu söyle (kıdemli görüş / dış uzman / yönetim toplantısı)
4. "TASLAK — KIDEMLİ İNCELEMEDEN GEÇMEMİŞ" ibaresiyle başlangıç çerçevesi ver

### Adım 4 — Detayları topla

#### KVKK başvurusu için
- Başvurucu adı ve iletişimi
- Talep tipi
- İlgili veri kapsamı
- Yanıt son tarihi (KVKK m.13 — 30 gün)

#### İhtarname yanıtı için
- Karşı taraf ve vekili
- İhtarnamenin tarihi ve tebliği
- Müvekkilin durumu (talebi kabul / reddet / kısmi kabul / müzakere)
- İlgili sözleşme veya hukuki ilişki

#### Savcılık bilgi yazısı için
- Soruşturma numarası
- İlgili kişiler
- Talep edilen bilgi/belge
- Yanıt son tarihi

#### Kurum yazısı için
- Kurum, yazı tarihi, sayı
- Talep edilen belge/açıklama
- Müvekkilin pozisyonu

### Adım 5 — Yanıtı oluştur

Şablonu detaylarla doldur. Yanıt:

- **Profesyonel tonda** — bürokratik dil, gereksiz tantanasız
- Türk hukuku gereken tüm unsurları içermeli
- Spesifik tarih, süre ve yükümlülüklere atıf yapmalı
- Karşı taraf için net sonraki adımları belirtmeli
- Uygun çekincesi ve hak saklı tutmaları içermeli

Taslağı kullanıcıya sun ve onayını al.

#### Tonalite ayarı
- **Hedef:** İç vs. dış, ticari vs. hukuk, bireysel vs. kurum
- **İlişki:** Yeni karşı taraf vs. mevcut iş ortağı vs. çekişmeli taraf
- **Hassasiyet:** Rutin vs. çekişmeli vs. soruşturma
- **Aciliyet:** Standart süre vs. hızlandırılmış

### Adım 6 — Şablon oluşturma (şablon yoksa)

Kullanıcı yeni şablon yapmak isterse:

1. **Kullanım senaryosunu tanımla** — hangi sıklıkla, kim için, ne tür acillik
2. **Zorunlu unsurlar** — her yanıtta olması gereken bilgi
3. **Değişkenler** — `{{degisken}}` notasyonu
4. **Eskalasyon tetikleyicileri** — şablonun KULLANILMAMASI gereken durumlar
5. **Metadata** — sürüm, yazar, son inceleme tarihi
6. **Yanıt sonrası eylemler** — kayıt, takvim, takip

## Yanıt Kategorileri

### 1. KVKK İlgili Kişi Başvurusu Yanıtı

**Alt kategoriler:**
- Başvurunun alındığının teyidi
- Kimlik doğrulama talebi
- Talebin yerine getirilmesi (erişim, düzeltme, silme, anonimleştirme)
- Kısmi yerine getirme + gerekçe
- Tam ret + gerekçe
- Süre uzatma bildirimi (mevzuatın izin verdiği ölçüde)

**Temel unsurlar:**
- KVKK m.11 hakkına atıf
- Yanıt son tarihi
- Kimlik doğrulama yöntemi
- İlgili kişinin diğer hakları (Kurul'a şikâyet — m.14)
- İletişim bilgisi

**Şablon yapısı:**

```
Sayın {{ad_soyad}},

{{tarih}} tarihli, {{ref_no}} numaralı KVKK m.11 kapsamındaki [erişim/düzeltme/silme] talebiniz tarafımıza ulaşmıştır.

[Kimlik doğrulama / Yerine getirme / Reddetme gerekçesi]

KVKK m.13/2 uyarınca tarafınıza [...] tarihine kadar esaslı yanıt verilecektir.

Yanıttan memnun kalmamanız halinde KVKK m.14 uyarınca Kurul'a şikâyet hakkınız saklıdır.

Saygılarımızla,
{{veri_sorumlusu}}
Tarih: {{tarih}}
```

### 2. İhtarname Yanıtı

**Alt kategoriler:**
- Talebin reddi
- Talebin kabulü
- Kısmi kabul ve karşı talep
- Müzakere daveti
- Hak ihtirazı ile cevap

**Temel unsurlar:**
- Karşı tarafın ihtarnamesine ref
- Olgu düzeltmeleri (varsa)
- Hukuki dayanak (TBK, TTK, vb.)
- Müvekkilin pozisyonu net
- Karşı taraf için sonraki adım
- Hak saklı tutmaları

**Şablon yapısı:**

```
KONU: {{tarih}} tarihli ihtarnamenize cevabımızdır.

Sayın {{karşı_taraf}},

{{tarih}} tarihinde tarafımıza ulaşan ihtarnamenizde ileri sürdüğünüz iddiaları reddetmekteyiz.

1. OLAYLARA İLİŞKİN
[...]

2. HUKUKİ DEĞERLENDİRME
[İlgili mevzuat ve içtihat atıfları]

3. TARAFIMIZIN POZİSYONU
[Talebi kabul/red/kısmi kabul + gerekçe]

İhtarnamenizde ileri sürülen taleplere katılmadığımızı, sözleşmesel ve yasal haklarımızın saklı kaldığını bildirir; uyuşmazlığın görüşme yoluyla çözülmesini öneririz.

Saygılarımızla,
Vekili
{{avukat}}
{{tarih}}
```

### 3. Savcılık / Mahkeme Bilgi Yazısı Yanıtı

**Kritik not:** Savcılık veya mahkeme yazıları her zaman kıdemli denetim gerektirir. Şablonlar başlangıç çerçevesi olarak işlev görür.

**Temel unsurlar:**
- Soruşturma no veya esas no
- Belge teslimi onayı (varsa) veya itiraz
- Süre uzatma talebi (gerektiğinde — CMK m.41 vd. ve HMK uyarınca)
- Avukat-müvekkil imtiyazı iddiaları (varsa)

### 4. KVKK Kurulu veya Sektörel Kurum Yazısı

**Alt kategoriler:**
- Bilgi/belge talebi cevabı
- Şikâyete cevap
- Soruşturma savunması
- İdari para cezası itirazı (varsa)

### 5. KEP ile Resmi Tebligat

**Şablon yapısı:**

```
KEP Adresi: {{karşı_taraf_kep}}
Konu: {{konu}}

Sayın {{karşı_taraf}},

İşbu yazımız, 6102 sayılı Türk Ticaret Kanunu m.18/3 ve ilgili mevzuat uyarınca KEP yoluyla taraf [müvekkil] adına resmi tebligat olarak gönderilmiştir.

[İçerik]

Saygılarımızla,
{{ad}}
{{tarih}}
```

### 6. Kira Uyuşmazlığı Yazışması

**Alt kategoriler:**
- Kira artışı talebine yanıt (TBK m.344 — TÜFE üst sınırı, mevzuat doğrulanmalı)
- Kira ödeme temerrüdü ihtarı yanıtı
- Tahliye taahhüdü pozisyonu

### 7. Tedarikçi / Müşteri Hukuki Sorgu Yanıtı

**Alt kategoriler:**
- Sözleşme durum sorgusu cevabı
- Değişiklik talebi cevabı
- Uyum belgesi talebi
- Denetim talebi
- Sigorta poliçesi talebi

## Çıktı Formatı

```markdown
## Hukuki Yanıt: [Tip]

**Muhatap:** [...]
**Konu:** [...]

---

[Yanıt metni]

---

### Eskalasyon kontrolü
[Tetikleyici tespit edilmedi / Şu tetikleyiciler bulundu: ...]

### Mevzuat ve içtihat doğrulaması
- ...

### Sonraki adımlar
1. ...
2. Takvime ekle: [son tarih]
3. ...
```

## Notlar

- Yanıt sunulmadan önce her zaman kullanıcının onayını al
- E-posta MCP bağlıysa taslak e-posta yaratabilir
- Yanıt son tarihlerini takvime ekleme önerisi sun
- Mevzuata bağlı yanıtlarda (KVKK, savcılık) süre kritik
