---
name: uyum-kontrol
description: Önerilen bir aksiyon, ürün özelliği, kampanya veya iş girişimi için uyum kontrolü yapar. Türk hukuku eksenli — KVKK 6698, TKHK 6502, Reklam Yönetmeliği, sektörel mevzuat (BDDK, EPDK, SPK, Rekabet Kurumu, TİTCK, Sağlık Bakanlığı). Uygulanan mevzuatı, gerekli onayları, riskli alanları ve eskalasyon noktalarını çıkartır.
---

# /turk-hukuk-legal:uyum-kontrol — Uyum Kontrolü

## Davet

```
/turk-hukuk-legal:uyum-kontrol [aksiyon veya girişim]
```

## Ne İhtiyacım Var

Yapmak istediğini açıkla. Örnekler:
- "Sadık müşterilere nakit hediye kampanyası başlatacağız"
- "Mobil uygulamaya biyometrik giriş ekleyeceğiz"
- "AB müşteri verilerini Türkiye'deki sunucuda işleyeceğiz"
- "Yapay zekâ destekli sohbet özelliğini lanse edeceğiz"
- "Müşteri yorumlarını reklamda kullanmak istiyoruz"

## Çıktı

```markdown
## Uyum Kontrolü: [Girişim]

### Özet
[Hızlı değerlendirme: Devam et / Koşullarla devam et / Daha derin inceleme gerekli]

### Uygulanan Mevzuat ve Politikalar
| Mevzuat | İlgi | Temel gereklilikler |
|---|---|---|
| KVKK 6698 | ... | ... |
| TKHK 6502 | ... | ... |
| Reklam Yönetmeliği | ... | ... |

### Gereklilikler
| # | Gereklilik | Durum | Aksiyon |
|---|---|---|---|

### Risk alanları
| Risk | Önem | Hafifletme |
|---|---|---|

### Önerilen aksiyonlar
1. ...
2. ...

### Onaylar
| Onaycı | Neden | Durum |
|---|---|---|

### Derin inceleme önerisi
[Kıdemli görüş veya dış uzman önerilen alanlar]
```

## Türk Hukuku Uyum Çerçevesi

### KVKK (6698) — Kişisel Verilerin Korunması Kanunu

**Kapsam:** Türkiye'de bulunan veya hizmet alan kişilerin kişisel verisini işleyen her veri sorumlusu. Yurt dışına aktarımda da Türk veri sorumlusu sorumluluğu devam eder.

**Hukuk müşaviri için temel yükümlülükler:**

- **Hukuki sebep belirleme (KVKK m.5-6):** Her işleme faaliyeti için açık rıza dışında bir sebep aranır — sözleşme zorunluluğu, hukuki yükümlülük, meşru menfaat, hayati menfaat, kamuoyuna açık veri, fiilî imkânsızlık. Özel nitelikli veri için ek koşullar (m.6).
- **İlgili kişi başvurusu yanıtı (KVKK m.13):** 30 gün içinde yanıt; gerekçesiz reddedilemez.
- **Veri ihlali bildirimi (KVKK m.12 + Kurul kararları):** İhlalden öğrenildikten itibaren **72 saat** içinde Kurul'a bildirim eğilimi.
- **VERBİS kaydı:** Belirli kapsam altındaki veri sorumluları için zorunlu.
- **Yurt dışı aktarım (KVKK m.9):** Açık rıza, yeterli korumalı ülke listesi (henüz dar), taahhütname (Kurul izniyle), Kurul izinli belirli istisnalar.
- **Aydınlatma yükümlülüğü (KVKK m.10):** Veri toplama anında belirli bilgileri aktarma.
- **DPIA / VKED:** Yüksek risk işlemelerde yazılı etki değerlendirmesi yapılması.

**Hukuk müşavirinin sık temasları:**

- Tedarikçi sözleşmelerinde KVKK ek protokolünün kontrolü
- Ürün geliştirme ekibine privacy-by-design tavsiyesi
- Kurul soruşturma ve cevap yazısı
- Yurt dışı veri aktarımı çözümleri (taahhütname başvurusu vb.)
- Açık rıza ve aydınlatma metinlerinin incelenmesi

### TKHK (6502) — Tüketicinin Korunması Hakkında Kanun

**Kapsam:** Tüketici (mesleki olmayan amaçla mal/hizmet alan) ile yapılan her sözleşme.

**Temel başlıklar:**
- Ayıplı mal/hizmet (m.8 vd., m.13 vd.) — 2 yıl ayıp hakları
- Mesafeli sözleşmeler ve cayma hakkı (m.48 — genelde 14 gün)
- Taksitli satışlar (m.17 vd.)
- Konut kredisi (m.32 vd.)
- Haksız şartlar denetimi (m.5)
- Genel İşlem Koşulları (TBK m.20-25 ile birlikte)
- Reklam (Reklam Kurulu, Ticari Reklam ve Haksız Ticari Uygulamalar Yönetmeliği)

### Sektörel mevzuat — Hızlı Yönlendirici

| Sektör | Düzenleyici | Ana mevzuat |
|---|---|---|
| Bankacılık & finansal hizmetler | BDDK | 5411 Bankacılık K., 6361 Finansal Kiralama K. |
| Sermaye piyasası | SPK | 6362 SerPK + tebliğler |
| Sigortacılık | T.C. Sigortacılık ve Özel Emeklilik Düzenleme ve Denetleme Kurumu (SEDDK) | 5684 Sigortacılık K. |
| Telekom & elektronik haberleşme | BTK | 5809 Elektronik Haberleşme K. |
| Enerji (elektrik, doğal gaz, petrol) | EPDK | 6446 Elektrik Piyasası K., 4646 Doğal Gaz, 5015 Petrol |
| Rekabet | Rekabet Kurumu | 4054 Rekabetin Korunması K. |
| Sağlık | Sağlık Bakanlığı, TİTCK | 3359 SSHK, 1262 İspençiyari ve Tıbbi Müstahzarlar K. |
| Bilişim & internet | BTK + DGTM | 5651 SK, 6493 Ödeme Hizmetleri K. |
| Çalışma & sosyal güvenlik | Çalışma Bakanlığı, SGK | 4857 İş K., 5510 SGK |
| Çevre | Çevre Bakanlığı | 2872 Çevre K. |

### Reklam ve pazarlama uyum kontrol listesi

- ✅ Reklam Kurulu Yönetmeliği gerekliliklerine uygunluk
- ✅ Karşılaştırmalı reklamda haksız rekabet sınırı (TTK m.55)
- ✅ İndirim/kampanya bilgilendirmesi (TKHK + Ticari Reklam Yön.)
- ✅ Influencer ve içerik üreticisi etiketlemesi (Reklam Kurulu 2020/4 sayılı Kılavuz)
- ✅ "Doğal" "organik" "vegan" gibi iddiaların belgelenmesi
- ✅ Sağlık iddiası varsa TİTCK denetimi
- ✅ Veri kullanımı KVKK uyumlu

### Yapay zekâ / makine öğrenmesi girişimleri

Şu an Türkiye'de spesifik bir YZ Kanunu yok; ama:
- KVKK m.11 — otomatik karar verme sonuçlarına itiraz hakkı
- AB AI Act dolaylı etkisi (AB pazarına satış / işleme)
- Sektör mevzuatı (örn. bankacılıkta BDDK kararları YZ destekli kredi puanlama hakkında)
- FSEK YZ çıktısı eserlik tartışması — netleşmemiş içtihat

## İlgili Kişi Başvurularını Yanıtlama (KVKK m.11, m.13)

### Başvuru alma

İlgili kişi başvurusu alındığında:

1. **Başvuru tipini tanımla:**
   - Veriye erişim talebi
   - Veriyi düzeltme talebi
   - Silme veya anonimleştirme talebi
   - İşlemenin sona erdirilmesi
   - Otomatik karara itiraz
   - Aktarımın engellenmesi
   - Zarara yol açan sonucun ortadan kaldırılması

2. **Hangi mevzuat geçerli?**
   - Sadece KVKK mi?
   - Yurt dışı kişi ise GDPR ile çakışma mı?
   - Sektörel mevzuat ek hak/yükümlülük tanıyor mu?

3. **Kimliği doğrula:**
   - Makul ölçüde belge talep et
   - Aşırı belge isteme; ilgili kişiyi caydırma şüphesi
   - Vekâletname varsa avukat aracılığıyla başvuru

4. **Kayıt et:**
   - Tarih, başvuru tipi, ilgili kişi kimliği, mevzuat, son tarih

### Yanıt süreleri

| Mevzuat | Yanıt süresi |
|---|---|
| KVKK m.13 | 30 gün |
| GDPR (çakışan kişi için) | 30 gün, +60 gün uzatma mümkün |

### İstisnalar

- Mahkeme kararıyla saklama zorunluluğu (litigation hold benzeri)
- Mevzuat gereği saklama (örn. e-fatura 10 yıl, SGK 30 yıl, vb.)
- Üçüncü kişi haklarının ihlali olmaması
- Anonimleştirilmiş veri üzerinde geri dönüş imkânsızlığı

### Yanıt süreci

1. Tüm sistemlerden ilgili kişinin verisini topla
2. İstisnayı uygula ve gerekçele
3. Yanıtı hazırla: talebi yerine getir veya neden yerine getirilemediğini açıkla
4. Reddedilen talep için açık hukuki gerekçe
5. KVKK Kurulu'na şikâyet hakkını hatırlat (KVKK m.14)
6. Yanıtı ve başvurunun kayıt tut

## Mevzuat İzleme

### Neyin izlenmesi gerekir

- Resmî Gazete yayınları
- Sektörel kurum/kurul kararları (BDDK, EPDK, KVKK, Rekabet, vb.)
- Yargıtay, Danıştay, AYM içtihatları (`yargi_mcp.search`)
- AYM bireysel başvuru kararları
- AİHM ilgili kararları
- AB düzenlemeleri (sınırötesi etki)

### İzleme yaklaşımı

1. RG bültenine abone ol
2. İlgili kurumların duyuru sayfalarını izle
3. Sektör derneklerinin uyarılarına dikkat
4. Uyum takvimi tut (yürürlük tarihleri, son tarihler)
5. Hukuk ekibine maddi gelişme brifingi

### Eskalasyon kriterleri

- Yeni mevzuat müvekkilin temel iş faaliyetini etkiliyor
- Sektörde bir cezai uygulama gözetim sinyali veriyor
- Yaklaşan bir uyum tarihi organizasyonel değişiklik gerektiriyor
- Müvekkilin dayandığı veri aktarım mekanizması iptal ediliyor
- Kurum müvekkil hakkında soruşturma açıyor

## İpuçları

1. **Spesifik ol** — "Müşterilere e-posta göndereceğiz" yerine "tüm müşteri listesine ticari elektronik ileti (İYS) kapsamında promosyon e-postası göndereceğiz"
2. **Coğrafyayı belirt** — uyum gereklilikleri yargı yerine göre değişir
3. **Hangi veriyle çalışılıyor?** — bu uyum gerekliliklerinin çoğunu belirler
