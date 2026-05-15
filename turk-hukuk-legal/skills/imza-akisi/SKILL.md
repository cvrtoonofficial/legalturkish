---
name: imza-akisi
description: İmzaya hazır bir sözleşme veya yazılı belge için kontrol listesi yürütür; KEP, e-imza (5070), ıslak imza, noter onayı arasından doğru yöntemi önerir; imza sırasını ve süreçten önce kontrol edilmesi gereken son maddeleri belirler.
---

# /turk-hukuk-legal:imza-akisi — KEP & E-İmza Akışı

## Davet

```
/turk-hukuk-legal:imza-akisi [belge]
```

## İş Akışı

### Adım 1 — Belgenin Tipini Belirle

| Belge tipi | Genel imza yöntemi tercihleri |
|---|---|
| Bireyler arası sözleşme | Islak imza yeterli; özel hallerde noter (taşınmaz, miras, kefalet) |
| Tacirler arası sözleşme | KEP / e-imza yeterli; geleneksel ıslak imza da geçerli |
| Tüketici sözleşmesi | Mesafeli ise dijital yeterli; klasik şekil şartı olanlar (taşınmaz vb.) ayrı |
| Taşınmaz satışı | **Tapu sicil müdürlüğünde resmî senet zorunlu** (TMK m.706, 2644 sayılı TSK) |
| Mortgage / ipotek | Tapu sicil müdürlüğünde resmî senet |
| Kefalet | **Yazılı + miktarın kefilce el yazısıyla yazımı + tarih + kefilin imzası** (TBK m.583) |
| Vekâletname | Genelde noter onaylı; özel yetkiler için (taşınmaz satış, dava vekâleti) zorunlu |
| Miras / vasiyetname | El yazılı veya noter (TMK m.538 vd.) |
| Ön ödemeli konut satışı | Noter onaylı veya tapu sicilinde (TKHK m.40 vd. — verify) |
| Tüzel kişi yetkilendirmesi | İmza sirküleri + yetkili imza |
| Resmi tebligat (ihtarname, fesih bildirimi) | **KEP zorunlu** sermaye şirketleri arasında (TTK m.18/3) |

### Adım 2 — Şekil Şartını Kontrol Et

Aşağıdaki durumlarda **şekil şartı emredici** ve aksi davranış sözleşmeyi hükümsüz kılar:

| Sözleşme | Şekil | Mevzuat |
|---|---|---|
| Taşınmaz mülkiyeti devri | Tapu sicilinde resmî senet | TMK m.706 + 2644 SK |
| Taşınmaz satış vaadi | Noter onaylı | TBK m.237 (verify) |
| Kefalet | Yazılı + el yazısıyla kefil miktarı | TBK m.583 |
| Tüketici kredisi | Yazılı şekil | TKHK m.4/1 (verify) |
| FSEK mali hak devri ve lisansı | Yazılı + ayrı ayrı sayma | FSEK m.52 |
| SMK marka/patent/tasarım devri | Yazılı (TPMK siciline tescil 3. kişi etkililiği için) | SMK m.148 (verify) |
| Adi ortaklık (taşınmaz katkısı varsa) | Resmî şekil | TBK m.620, m.706 |
| Vasiyetname | El yazılı / resmi (noter) / sözlü (özel hal) | TMK m.531 vd. |

### Adım 3 — Doğru İmza Yöntemini Seç

#### Islak imza
- Geleneksel; her durumda geçerli
- Taraflar fiziksel olarak imzalar
- Dijital ortamda saklama: PDF tarama + orjinal saklama

#### E-imza (5070 sayılı Elektronik İmza Kanunu)
- **Güvenli elektronik imza (e-İmza):** Islak imzaya eşdeğer hukuki sonuç doğurur (5070 SK m.5)
- Bağımsız bir e-imza sertifika sağlayıcısından alınır (E-Tuğra, TürkTrust, Kamu SM, vb.)
- KEP'le birlikte resmi tebligat süreçlerinde kullanılır

#### KEP (Kayıtlı Elektronik Posta)
- 6102 TTK m.18/3 — sermaye şirketleri arasında ihtar, ihbar ve tebligat için **zorunlu**
- BTK düzenlemesi altında çalışır
- Gönderim ve teslim zaman damgalıdır
- Tebligat Kanunu m.7/a ile resmi tebligat geçerli

#### Noter
- Kanunla şekil şartı olan işlemlerde zorunlu
- Karşı tarafın iradesini sözlü teyit ettirmek için tercih edilir
- Bazı vekâletname tipleri (taşınmaz satış vekâleti) noterde düzenlenmeli

#### Onay yöntemi seçim matrisi

```
Belge:           Sözleşme imzası
Taraflar:        İki ticari şirket
KEP zorunlu mu?  Hayır (sözleşme imzası, ihtarname/fesih bildirimi değil)
E-imza var mı?   Her iki tarafta da var
Sonuç:           E-imza önerilir (hızlı, ispatı güvenli)
```

```
Belge:           İhtarname (sözleşme feshi öncesi)
Taraflar:        İki anonim şirket
KEP zorunlu mu?  Evet (TTK m.18/3)
Sonuç:           KEP zorunlu; ıslak ihtarname + noter de ek tedbir olarak gönderilebilir
```

### Adım 4 — İmza Öncesi Son Kontrol Listesi

```markdown
## İmza Öncesi Kontrol Listesi

### Belge bütünlüğü
- [ ] Tüm sayfalar numaralı ve doğru sırada
- [ ] Tüm ekler mevcut ve atfedilen yerde
- [ ] Şartlar ve definitions tutarlı
- [ ] Müzakere son turu sonrası tüm değişiklikler işli
- [ ] Karşı tarafın gönderdiği versiyon ile imzaya gönderilen versiyon aynı mı (hash, sayfa sayısı, dosya boyutu)

### Tarafların kontrolü
- [ ] Tüzel kişi ünvanı tam ve doğru (MERSIS kontrolü)
- [ ] İmza sirküleri güncel
- [ ] Vekâletname varsa süresi geçerli ve özel yetki açık
- [ ] Karşı tarafın imza yetkilisi yetkili mi (imza sirkülerinden teyit)

### Şekil
- [ ] Bu sözleşme için emredici şekil şartı var mı?
- [ ] Damga vergisi durumu (488 sayılı Damga Vergisi K.) — bazı sözleşmeler damga vergisi gerektirir, hesaplanmış mı?
- [ ] Pul olmadan zayıf delil değil mi (özelde damga vergisi tarafı eksik olan kanıt için süpheli)

### Yetki
- [ ] İmza yetkisi onay matrisinde — toplam değer ve yetkiyi imzalayan
- [ ] Yönetim kurulu kararı gerekiyor mu (örn. yüksek değerli işlem, ortaklığın temel iş alanı)
- [ ] Genel kurul kararı gerekiyor mu (TTK m.408 — istisnai işlemler)

### Süre & koşullar
- [ ] Tüm koşullar gerçekleştirildi mi (closing conditions)
- [ ] Yetkili kurumdan onay gerekli mi (Rekabet Kurumu eşik, BDDK izni, vb.)
- [ ] Vergi mukimliği belgesi (yurt dışı) hazır mı

### Yan belgeler
- [ ] KVKK ek protokolü imzalanacak mı (eş zamanlı)
- [ ] İmza sirküleri kopyası
- [ ] Vekâletname (uygun ise)
- [ ] Kefil imzaları (varsa, TBK m.583 şart kontrolü)
- [ ] Sigorta poliçesi sureti
```

### Adım 5 — İmza Sırası

Çoklu imza gereken durumlarda:

| Sıra tipi | Kullanım |
|---|---|
| **Sıralı (sequential)** | Önce iç onaylar → karşı taraf imzası → müvekkilin son imzası. Müvekkilin son imzaya kadar geri çekilme hakkı korunur. |
| **Paralel** | İki taraf eş zamanlı imzalar. Yüksek güven ortamı; sözleşme tüm imzalar tamamlanınca yürürlüğe girer. |
| **Kefil için ayrı sıra** | Kefilin imzası ayrı belge veya ayrı sayfada (TBK m.583 şart) |

### Adım 6 — Çıktı

```markdown
## İmza Akışı Planı

**Belge:** [...]
**Taraflar:** [...]
**Önerilen yöntem:** [KEP / E-imza / Islak / Noter]
**Gerekçe:** [...]

### Şekil şartı durumu
[Emredici şekil şartı yok / Şu şekil şartı gerek: ...]

### Damga vergisi
[Hesaplandı: ... TL / Damga muafiyeti: ...]

### Yetki onayı
[Yönetim kararı: gerekli/değil; alınmış/alınmamış]

### İmza sırası
1. [İlk imza] — kim, ne zaman
2. [İkinci imza] — kim, ne zaman
3. [Eş zamanlı kefil imzası, varsa]

### Yan belgeler hazır mı
- [ ] İmza sirküleri
- [ ] Vekâletname
- [ ] KVKK ek protokolü
- [ ] Diğer ...

### Son kontrol notları
- ...

### İmza sonrası
1. İmzalı suretin saklanma yeri
2. Tedarikçi/müşteri kaydına işleme
3. Takvime ekleme: yenileme uyarısı, sürelerin başlangıcı
4. (Gerekirse) KEP üzerinden karşı tarafa imzalı suret gönderme
```

## Türk Pratiği için Notlar

**Damga vergisi:** Sözleşme tutarına göre damga vergisi hesaplanır. Bazı sözleşme tipleri muaf, bazıları indirimli. Damga vergisi ödenmemiş sözleşme zayıf delil sayılabilir. Damga vergisi tablosu yıllık güncellenir; her sözleşme için hesap yapılmalı.

**Türkçe nüsha şartı:** Bazı durumlarda Türkçe nüsha zorunluluğu vardır (örn. iş sözleşmesi 4857 SK m.8 + 805 SK — yabancı dil zorunluluğunun sınırı tartışmalı). Yabancı dilli sözleşmeler genelde **çift dilli** veya **resmi tercüme** ile sunulur.

**Tüzel kişi temsili:** İmza sirküleri MERSIS üzerinden teyit edilir. Karşı tarafın imza sirkülerinin alınması ve **müvekkil dosyasında saklanması** uygulamada kritik.

**Vekâletname özelleştirmesi:** Avukat olmayan vekiller için noter onaylı vekâletname yeterli; avukat için baroda kayıtlı vekâletname. Özel yetkili işlemler (taşınmaz satış, ibra, sulh) açıkça yazılmalı.

**KEP teslimi ispatı:** KEP delili **iadeli taahhütlü posta veya noter ihtarnamesi**ne göre daha güçlü; zaman damgalı ve içeriği değiştirilemez.

## Notlar

- İmzaya gönderilmek üzere son metni tarafların hepsinin onayladığından emin ol.
- E-imza kullanımında **sertifikanın geçerli olduğunu** her seferinde teyit et.
- Noter onayı planlı yapılmalı; randevu gerekebilir (özellikle taşınmaz işlemlerinde).
- İmzalanmış belgenin **bir nüshası karşı tarafa, bir nüshası bürolda, bir nüshası dijital arşivde** olacak şekilde dağıt.
