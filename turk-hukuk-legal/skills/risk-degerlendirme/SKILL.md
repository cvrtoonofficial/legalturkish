---
name: risk-degerlendirme
description: Hukuki riski önem × olasılık matrisinde değerlendirir, eskalasyon kriteri uygular, kıdemli görüş veya dış hukuk uzmanı gerektirip gerektirmediğini söyler. Sözleşme riski, dava maruziyeti, KVKK ve sektörel mevzuat ihlali riski, fikri haklar tecavüzü riski için kullanılır.
---

# /turk-hukuk-legal:risk-degerlendirme — Hukuki Risk Değerlendirmesi

## Davet

```
/turk-hukuk-legal:risk-degerlendirme [risk konusu]
```

## Değerlendirme Çerçevesi

### Önem (Severity) Skalası

| Seviye | Tanım | Türk hukuku örnekleri |
|---|---|---|
| 1 — Düşük | Düşük maliyet, sınırlı operasyonel etki, kolay onarılır | Tip sözleşmede dilbilgisi hatası, küçük tüketici şikâyeti |
| 2 — Orta | Önemli para tutarı veya orta itibar etkisi | Tek bir tedarikçi sözleşmesi anlaşmazlığı, KVKK m.13 yanıt gecikmesi |
| 3 — Yüksek | Büyük finansal etki, kamu görüşü etkisi, idari para cezası riski | KVKK m.12 veri ihlali bildirimi gerektiren olay, FSEK/SMK tecavüzü iddiası, Rekabet Kurumu ön soruşturma |
| 4 — Kritik | Var olma tehdidi, ceza yargılaması, lisans iptal, büyük dava | Bilişim suçu iddiası, BDDK işlem yasağı, ana ürün için patent davası, AYM bireysel başvuru aşaması |

### Olasılık (Likelihood) Skalası

| Seviye | Tanım |
|---|---|
| 1 — Düşük | <%10 |
| 2 — Orta | %10–30 |
| 3 — Yüksek | %30–60 |
| 4 — Çok yüksek | >%60 |

### Risk matrisi

|  | Olasılık 1 | Olasılık 2 | Olasılık 3 | Olasılık 4 |
|---|---|---|---|---|
| Önem 1 | DÜŞÜK | DÜŞÜK | ORTA | ORTA |
| Önem 2 | DÜŞÜK | ORTA | ORTA | YÜKSEK |
| Önem 3 | ORTA | YÜKSEK | YÜKSEK | KRİTİK |
| Önem 4 | YÜKSEK | YÜKSEK | KRİTİK | KRİTİK |

## Değerlendirme İş Akışı

### Adım 1 — Riski Tanımla

- Hangi olay/durum?
- İlgili taraflar
- Maddi olgular ve zaman çizelgesi
- Karşı tarafın bilgi/iddia durumu
- Mevcut delil paketi

### Adım 2 — Hukuki Çerçevedeki Yeri

- Hangi maddi hukuk normu (TBK, TTK, FSEK, KVKK, vb.)?
- Hangi usul hukuku (HMK, İYUK, CMK)?
- Hangi yargı yeri (genel mahkeme, ihtisas, idari, ceza)?
- Hangi süreler (zamanaşımı, hak düşürücü)?

### Adım 3 — Sonuç Etkileri (Quantify)

| Etki kategorisi | Tahmin |
|---|---|
| Doğrudan maddi zarar | ... TL |
| Yargı masrafları (harç, vekâlet, bilirkişi, posta) | ... TL |
| Süre tahmini (ilk derece + BAM + Yargıtay) | ... yıl |
| Olası idari para cezası | KVKK üst sınırı, Rekabet K. üst sınırı, vb. |
| İtibar etkisi | Düşük/Orta/Yüksek |
| Operasyonel etki | Üretim durması, faaliyet kısıtı, lisans riski |
| Yansı hak etkisi | Üçüncü kişilerle sözleşme zincirleri |

### Adım 4 — Türk Yargılama Sisteminin Dinamiklerini Dikkate Al

- **İhtiyati tedbir riski:** Karşı taraf tedbir alabilir mi? (Patent, marka, telif davalarında yaygın)
- **Bilirkişi kaderi:** Konu bilirkişi raporuna mı kalıyor? Hangi nokta tartışmalı?
- **İstinaf + Yargıtay olasılığı:** İlk derece kararı dönüm noktası mı, yoksa BAM/Yargıtay'da değişme olasılığı yüksek mi?
- **Arabuluculuk:** 6325 SK kapsamında dava şartı arabuluculuk uygulanıyor mu? Anlaşma şansı?
- **Yargıtay 11. HD (FSEK/SMK) veya 9. HD (iş) yerleşik içtihat var mı?** (`yargi_mcp` ile doğrula)
- **AYM bireysel başvuru:** Anayasal hak ihlali boyutu var mı?

### Adım 5 — Eskalasyon Kararı

| Risk seviyesi | Tavsiye |
|---|---|
| DÜŞÜK | İç kararla devam, log kaydı yeter |
| ORTA | Hukuk müşaviri onayı, durum brifingi |
| YÜKSEK | Kıdemli görüş + yönetim brifingi; gerekirse dış hukuk uzmanı |
| KRİTİK | Yönetim kurulu / icra kurulu bilgilendirme, dış uzman zorunlu, kriz yönetimi planı |

#### Otomatik eskalasyon tetikleyicileri (önem-olasılık matrisinden bağımsız)

- Düzenleyici kurum yazısı geldi
- Cezai sorumluluk söz konusu (TCK kapsamı)
- Bilişim suçu / siber olay
- Hassas veri ihlali (KVKK m.6 özel nitelikli)
- AYM bireysel başvuru süresi gözüküyor
- AİHM başvurusu için iç hukuk yolları tüketildi iddiası
- Sınır ötesi tarafın işin içine girmesi (MÖHUK uygulanır)
- Müvekkilin lisansının iptal riski (BDDK, EPDK, vb.)
- Tahkim klozu nedeniyle yargı yolu kapalı, ICC/ISTAC tahkimi başlamak üzere
- Yargılanan kişi yönetim kurulu üyesi / üst yönetici
- Medya ilgisi başladı veya başlamak üzere

### Adım 6 — Rapor

```markdown
## Risk Değerlendirme: [Konu]

### Özet
[1-2 cümle: ne, ne kadar büyük, ne aşamada]

### Olgular
[Tarihsel sıralama; ana taraflar; ana belgeler]

### Hukuki çerçeve
- Maddi hukuk: ...
- Usul: ...
- Süreler: ...
- Yetkili yer: ...

### Risk skoru
- Önem: [1-4] — gerekçe
- Olasılık: [1-4] — gerekçe
- Toplam: [DÜŞÜK / ORTA / YÜKSEK / KRİTİK]

### Olası sonuçlar
| Senaryo | Maliyet aralığı | Süre |
|---|---|---|
| En kötü | ... TL | ... yıl |
| Beklenen | ... TL | ... yıl |
| En iyi | ... TL | ... |

### Hafifletme stratejileri
1. ...
2. ...

### Eskalasyon kararı
[Tavsiye + gerekçe]

### Mevzuat ve içtihat doğrulaması
- ...

### Sonraki adımlar
1. ...
2. ...
3. Takvime ekle: [tarih — süre adı]
```

## Türk Pratiğine Özgü Notlar

**HMK m.107 belirsiz alacak davası:** Risk değerlendirilirken davacı tarafından "miktarı en az ... TL" ile açılan davaların **harç tamamlama riski** unutulmamalı; karşı taraf gerçek tutarı dilekçeyle netleştirebilir.

**TBK m.117 temerrüt + faiz kümülasyonu:** Risk hesaplarken yasal faiz vs. avans faiz oranı (ticari) farkı önemli; uzayan davalarda anaparayı geçebilir.

**Vekâlet ücreti yansıtması (AAÜT):** Karşı tarafa yükletilen vekâlet ücreti dava değerine bağlı; risk hesabında dahil et.

**İhtiyati tedbir teminat dengesi:** Tedbir kararı için teminat mektubu maliyeti + tedbirin uzun sürmesi halinde faiz kaybı + teminat tutarı bağlanması.

**Bilirkişi maliyeti:** Davanın **kaderi sıklıkla bilirkişiye bağlı**; harçtan ayrı önemli kalem.

## Notlar

- Risk değerlendirme tek seferlik değil; yeni belge, yeni karar veya yeni gelişmeyle yenilenir.
- Müvekkille paylaşılan risk raporu **savunmasız kayıt** oluşturabilir; iç dolaşımda saklanma şekli dikkatli kurgulanmalı.
