---
name: trafik-kazasi-davasi
description: Trafik kazasından doğan maddi ve manevi tazminat, destekten yoksun kalma, bedensel zarar (geçici/sürekli iş göremezlik, maluliyet, tedavi giderleri) davalarını analiz eder. KTK 2918, TBK m.49+ haksız fiil, ZMSS, sigorta tahkim komisyonu, bilirkişi raporu ve maluliyet hesabı çerçevesinde çalışır. Kusur oranı tartışması, sigorta limiti aşımı, manevi tazminat takdiri, faiz başlangıç tarihi gibi pratik noktaları kapsar.
version: 0.4.0
last_legal_review: 2026-05-16
required_mcps:
  - mevzuat_mcp
  - yargi_mcp
optional_mcps:
  - literatur-mcp
  - hukuk-rag
applicable_laws:
  - 2918
  - 6098
  - 5684
  - 6100
---

# /turk-hukuk-legal:trafik-kazasi-davasi — Trafik Kazası Tazminat Analizi

> Trafik kazası davaları **çok katmanlı**: kusur tespiti (bilirkişi), zarar hesabı (maluliyet, gelir kaybı, tedavi), sigorta sorumluluğu (ZMSS), faiz hesabı. Bu skill her katmanı sistematik ele alır.

## Adım 0 — Zorunlu MCP Çağrıları

### 0.1 Profil okuma
- Müvekkil sürücü / yolcu / yaya / mağdur yakını?

### 0.2 Mevzuat (`mevzuat_mcp`)
- **KTK 2918** — özellikle m.84-94 (sorumluluk), m.92 (sigorta), m.95-99 (zorunlu sigorta)
- **TBK 6098** — m.49+ haksız fiil; m.55-58 manevi tazminat; m.71 organ teorisi
- **5684 sayılı Sigortacılık K.** — Sigorta tahkim m.30
- **HMK 6100** — m.106-107 belirsiz alacak

### 0.3 İçtihat (`yargi_mcp`)
- Yargıtay 4. HD ve 17. HD trafik kazası içtihatları (güncel daire teyit)
- Sigorta Tahkim Komisyonu kararları
- "kusur oranı bilirkişi yetersiz"
- "maluliyet hesabı destek tarifesi"

---

## ADIM 1 — Müvekkille Diyalog

```
Sor:
1. Kazada müvekkil hangi konumda?
   - Sürücü (kusurlu / kusursuz)
   - Yolcu (sürücüsünde kusur / başka aracın sürücüsünde kusur)
   - Yaya
   - Mağdurun yakını (ölümlü kaza)
2. Kaza tarihi + yeri + tutanağı?
3. Trafik kazası tespit tutanağı var mı (TKT)?
4. Polis raporu kusur oranını belirledi mi?
5. Sağlık durumu:
   - Hastane raporu var mı?
   - Geçici iş göremezlik (rapor)?
   - Sürekli iş göremezlik / maluliyet (heyet raporu)?
   - Ameliyat / tedavi devam ediyor mu?
6. Karşı tarafın sigortası:
   - ZMSS poliçesi var mı, geçerli mi?
   - İhtiyari Mali Sorumluluk var mı?
   - Kasko poliçesi var mı?
7. Sigorta şirketinden ödeme talep edildi mi?
   - Yapılan başvuru + cevap?
   - Sigorta Tahkim'e başvuru yapıldı mı (zorunlu)?
8. Müvekkilin geliri (tazminat hesabı için)?
9. Aile durumu (ölümlü kaza ise destek bireyleri)?
10. Hedef: tazminat tutarı + acil ihtiyati tedbir (ödeme) mi?
```

---

## ADIM 2 — Hukuki Çerçeve

### 2.1 Sorumluluk

| Konum | Hukuki dayanak |
|---|---|
| Sürücüye karşı | KTK m.85 + TBK m.49+ haksız fiil |
| Aracın işleticisine karşı | KTK m.85 + organ teorisi (TBK m.66, 71) |
| Aracın malikine karşı | KTK m.85 + işleten sıfatı |
| Sigortaya karşı | KTK m.91-92 — ZMSS doğrudan başvuru |

### 2.2 Sigorta katmanı

- **ZMSS (Trafik Sigortası):** Zorunlu, üçüncü kişi zararını karşılar; **limit** dahilinde
- **İhtiyari Mali Sorumluluk:** Üst sınır artışı
- **Kasko:** Aracın kendi zararını karşılar (üçüncü kişi değil)

ZMSS limit aşılırsa fark **sürücü/işleten/malik**ten istenir (TBK m.49+).

### 2.3 Zarar kalemleri

| Kalem | Hesap yöntemi |
|---|---|
| **Tedavi giderleri** | Fatura + reçete + ilaç + protez + ulaşım |
| **Geçici iş göremezlik** | Rapor süresi × günlük gelir |
| **Sürekli iş göremezlik (maluliyet)** | Heyet raporu maluliyet yüzdesi × gelir × maluliyet hesap formülü (PMF / aktif tarife) |
| **Destekten yoksun kalma** | Ölümlü kazada bağımlıların kaybı |
| **Manevi tazminat** | Hakimin takdiri — TBK m.56 |
| **Vekalet ücreti** | AAÜT |
| **Faiz** | TBK m.49 — olay tarihinden itibaren |

---

## ADIM 3 — Sigorta Tahkim Komisyonu (5684 SK m.30)

ZMSS'den kaynaklanan tazminat talepleri için **zorunlu** ön başvuru:
1. Müvekkil önce sigorta şirketine yazılı başvuru
2. 15 iş günü cevap beklenir
3. Cevap olumsuz/yetersizse Sigorta Tahkim Komisyonu'na başvuru
4. Tahkim hakem kararı **bağlayıcı** ama itiraz yolu var (Yargıtay 17. HD verify)

> Tahkim sürecinin başlamadığı veya tükenmediği durumda mahkeme davası **usulden reddedilir**. Süreç kritik.

---

## ADIM 4 — Bilirkişi Stratejisi

### Trafik kazası bilirkişisi tipik olarak:
- Kazanın oluş şeklini yeniden inşa eder
- Kusur oranını her sürücüye dağıtır
- Bedensel zarar varsa **maluliyet hesabı** ayrı bilirkişiye

### Lehimize bilirkişi soruları (`bilirkisi-soru-uretici` skill ile)

- Karşı sürücünün hangi trafik kuralını ihlal ettiği (KTK m.X)
- Müvekkilin kazadan kaçınma imkânının olmadığı
- Kazanın oluş anında karşı sürücünün hızının limit üzerinde olduğunun çarpışma analizinden tespiti
- Maluliyet raporunun **iyileşmenin tamamlandığı** dönemden alındığı (PMF tarifesine göre)

---

## ADIM 5 — Karşı Tarafın Olası Savunmaları

| Savunma | Önleyici cevap |
|---|---|
| "Müşterek kusur" | Polis raporu + tanık ifadesi + çarpışma analizi |
| "Müvekkilin emniyet kemeri yoktu" | Çocuk koltuğu / kurallar; emniyet kemeri ihmali kısmen kusur ama tamamen değil |
| "Maluliyet raporu erken" | Tedavi tamamlanmış mı doğrula; gerekirse ek heyet raporu |
| "Manevi tazminat abartılı" | Yargıtay 4./17. HD emsâl tutarlarına atıf |
| "Sigorta limiti yeterli" | Limit aşımı yoksa sigortadan; aşımı varsa fark sürücüden |
| "Faiz başlangıcı dava tarihinden" | TBK m.49 — olay tarihinden işler (yargı yerleşik) |

---

## ADIM 6 — Strateji

### Adım 1 — ZMSS sürecini tüket
- Sigortaya yazılı başvuru
- 15 iş günü bekle
- Tahkim'e başvuru (gerekirse)

### Adım 2 — Mahkemeye git (sigorta yetmezse)
- Asliye Hukuk + sigorta + sürücü + işleten birlikte dava
- Dava değeri: belirsiz alacak (HMK m.107)
- İhtiyati tedbir / ihtiyati haciz talebi (büyük zarar varsa)

### Adım 3 — Bilirkişi & maluliyet
- Bilirkişi sorularını önceden hazırla (`bilirkisi-soru-uretici`)
- Maluliyet için heyet raporu (Adli Tıp veya sağlık kurulu)

### Adım 4 — Faiz hesabı
- TBK m.49 + 4. HD içtihatı — olay tarihinden işler
- Yasal faiz vs. avans faiz ayrımı

---

## Standart Çıktı Formatı

```markdown
# Trafik Kazası Davası Analizi — {kaza_no}

## I. Olgular
- Kaza tarihi/yeri
- Taraflar + konumlar
- Kusur dağılımı (mevcut bilirkişi)

## II. Müvekkilin Statüsü ve Talepleri
## III. Sigorta Katmanı Analizi
## IV. Zarar Kalemleri ve Hesap
| Kalem | Hesap | Tahmin tutar |
|---|---|---|

## V. Sigorta Tahkim Komisyonu Süreci
## VI. Bilirkişi Stratejisi
## VII. Karşı Tarafın Olası Savunmaları + Cevaplar
## VIII. Strateji (Sigorta + Mahkeme)
## IX. Faiz Hesabı

## Ekler
A. Doğrulanmış Mevzuat
B. İçtihat (4./17. HD + Sigorta Tahkim)
C. Maluliyet tarifesi referansları
D. MCP Çağrı Logu
```

## Eskalasyon Tetikleyicileri

1. **Ölümlü kaza** — destekten yoksun kalma + manevi
2. **Çocuk maluliyeti** — özel hesap, kıdemli görüş
3. **Karşı sürücünün bilinçli ihlali / alkol** — ceza boyutu (TCK m.85)
4. **Sigorta şirketi iflas** — Tasfiye sürecinde Tahkim
5. **Yurt dışından gelen / giden taşıt** (Yeşil Kart Sistemi)

## Notlar

- ZMSS başvurusunda **kayıt** kritik — geri dönüş olmadığında dava açılamaz.
- Manevi tazminat hâkimin takdiri ama Yargıtay'ın emsâl tutarları belirleyici — yargi_mcp ile son yıl davalarında ortalama tara.
- Faiz hesabı toplam tutarın **yarısına** ulaşabilir uzayan davalarda — başlangıç tarihi kritik.
- Yargıtay 4. HD ve 17. HD daire numaraları zaman içinde değişmiş olabilir; her kullanımda `yargi_mcp` ile doğrulanır.
