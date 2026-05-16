---
name: aym-bireysel-basvuru
description: Anayasa Mahkemesi bireysel başvuru dilekçesi hazırlama skill'i (6216 sayılı Kanun). İç hukuk yollarının tüketildiğini ortaya koyar, ihlal edildiği iddia edilen anayasal hak ve özgürlüğü (Anayasa ve AİHS) tanımlar, 30 günlük süreyi takip eder, başvurunun şekil ve esas şartlarını sistematik kontrol eder. Genelde son derece sınırlı kabul edilen başvurular için kabul edilebilirlik kriterlerini önceden test eder.
version: 0.2.0
last_legal_review: 2026-05-16
required_mcps:
  - mevzuat_mcp
  - yargi_mcp
optional_mcps:
  - hukuk-rag
applicable_laws:
  - 6216
  - 2709
---

# /turk-hukuk-legal:aym-bireysel-basvuru — AYM Bireysel Başvuru

> AYM bireysel başvurusu, 6216 sayılı Kanun çerçevesinde **iç hukuk yolları tükendikten sonra**, Anayasa ve AİHS'te güvence altına alınan **temel hak ve özgürlüklerin** kamu gücü tarafından ihlali iddiasıyla yapılır. Süre 30 gün — kararın kesinleşmesinden itibaren. Kabul edilebilirlik çok katı; başvuruların büyük çoğunluğu **şekil ve esas yönünden** reddedilir.

## Adım 0 — Zorunlu MCP Çağrıları

### 0.1 Profil okuma
- `~/.claude/plugins/config/turk-hukuk-legal/CLAUDE.md`

### 0.2 Mevzuat (`mevzuat_mcp`)
- **Kanun 6216** — Anayasa Mahkemesinin Kuruluşu ve Yargılama Usulleri Hakkında Kanun (özellikle m.45-51 bireysel başvuru)
- **Anayasa (2709)** — Madde 148/3 bireysel başvuru hakkı + ilgili maddeler (m.10 eşitlik, m.13 sınırlama, m.17 yaşam, m.20 özel hayat, m.25-26 düşünce/ifade özgürlüğü, m.27 bilim ve sanat özgürlüğü, m.35 mülkiyet, m.36 hak arama özgürlüğü, m.40, vb.)
- **AİHS** karşılıkları (md.6 adil yargılanma, md.8 özel yaşam, md.10 ifade özgürlüğü, P1m1 mülkiyet)

### 0.3 AYM İçtihat (`yargi_mcp`)
```
yargi_mcp.search_anayasa_unified(query="<hak adı> bireysel başvuru kabul edilebilirlik")
```

Çekirdek aramalar:
- "iç hukuk yollarının tüketilmesi"
- "kabul edilebilirlik kriterleri"
- "anayasal hakka müdahale"
- "müdahalenin orantılılığı"

### 0.4 AİHM (gerekirse — sonraki adım için)
- AYM ret kararına karşı AİHM başvurusu hazırlığı için altyapı

---

## İş Akışı

### Adım 1 — Ön Eleme: Bireysel Başvuru Mümkün mü?

#### Kabul edilebilirlik şartları (6216 m.45-46)

| # | Şart | Kontrol |
|---|---|---|
| 1 | **Anayasal hak ihlali iddiası** | İhlal edildiği iddia edilen hak, **Anayasa'da güvence altına alınmış** ve aynı zamanda **AİHS** kapsamında olmalı |
| 2 | **Kamu gücü kullanımından** | Devlet eylemi/işlemi/ihmal/yargılama |
| 3 | **Kişisel etkilenme** | Başvurucu bizzat etkilenmiş olmalı (actio popularis kabul edilmez) |
| 4 | **İç hukuk yollarının tüketilmesi** | İstinaf → temyiz → karar düzeltme (varsa) — hepsi tüketilmeli, **kesin hüküm** verilmiş olmalı |
| 5 | **Süre** | Kararın kesinleşmesinden itibaren **30 gün** içinde başvuru |
| 6 | **Açıkça dayanaktan yoksun olmamalı** | Manifestly ill-founded değil |
| 7 | **Anayasal önem** | Sıradan yargılama hatası değil; **anayasal boyut** taşımalı |

#### Hangi hak ihlal edildiği iddia ediliyor?

Yaygın olanlar:
- **m.36 — Hak arama özgürlüğü / adil yargılanma** (AİHS m.6)
  - Mahkemeye erişim
  - Silahların eşitliği
  - Makul süre
  - Gerekçeli karar
  - Bilirkişi rapor değerlendirme
- **m.20 — Özel hayatın gizliliği** (AİHS m.8)
- **m.25-26 — Düşünce ve ifade özgürlüğü** (AİHS m.10)
- **m.27 — Bilim ve sanat özgürlüğü**
- **m.35 — Mülkiyet hakkı** (AİHS P1m1)
- **m.17 — Yaşam hakkı / işkence yasağı** (AİHS m.2, 3)
- **m.10 — Eşitlik / ayırımcılık yasağı**
- **m.40 — Etkili başvuru hakkı**

### Adım 2 — İç Hukuk Yollarının Tüketildiğini Belgele

Şu zincirin tamamlandığını göster:

```
İlk derece mahkemesi kararı
         ↓
İstinaf (BAM) — yetkili olduğu hallerde
         ↓
Temyiz (Yargıtay / Danıştay)
         ↓
[Karar düzeltme, varsa]
         ↓
Kesinleşme
         ↓
30 gün içinde AYM
```

**Tüketilme istisnaları:**
- Yargı yolu kapalıysa (bazı idari işlemlerde)
- Yargı yolu **etkili değilse** (uygulamada işlemiyorsa)
- Yargı yolu **erişilemezse**

### Adım 3 — Olayların Anayasal Boyutu

AYM başvurusunun en kritik kısmı: olayların **neden anayasal boyut taşıdığı**nın gösterilmesi. Sıradan yargılama hatası kabul edilmez.

Örnek formülasyonlar:
- "Yerel mahkemenin bilirkişi raporunu hiç değerlendirmeden karar vermesi, gerekçeli karar hakkını (Anayasa m.36 + AİHS m.6/1) ihlal eder."
- "Davalı tarafın delillerinin değerlendirilmemesi, silahların eşitliği ilkesini ihlal eder."
- "Makul süre içinde karar verilmemesi (5 yıl), adil yargılanma hakkının zaman boyutunu ihlal eder."
- "Mülkiyet hakkına yönelik kamulaştırmanın orantısız tazminat ile yapılması, Anayasa m.35 + AİHS P1m1 ihlali oluşturur."

### Adım 4 — Müdahale ve Orantılılık Testi

AYM, hakka yapılan müdahaleyi **üç aşamalı test** ile inceler:

1. **Hak ihlali var mı?** — Müdahale tespit ediliyor mu?
2. **Müdahalenin meşru amacı var mı?** — Kanun ile öngörülmüş; meşru amaç güdüyor mu?
3. **Müdahale orantılı mı?** — Demokratik toplumda gerekli mi; uygun mu; orantılı mı?

Başvurunun **III. aşamada** orantılılığı sorguladığı durumlarda kabul şansı en yüksektir.

### Adım 5 — Dilekçeyi Yapılandır

#### Bireysel başvuru dilekçesi şablonu

```
ANAYASA MAHKEMESİ BAŞKANLIĞINA
sunulmak üzere

BAŞVURUCU: Abdullah Babayiğit (T.C. ..., adres ...)
VEKİLİ: Av. ...
KARAR VEREN MAKAM: [son karar veren mahkeme/idari makam]
KARAR TARİHİ: [son kesinleşen karar tarihi]
TEBLİĞ TARİHİ: [kesinleşmiş kararın tebliği]
BAŞVURUNUN SÜRESİ: 30 gün — son gün: ...

KONU: Anayasa'nın {ilgili maddeler} ve AİHS'nin {ilgili maddeleri} kapsamında
ihlal edilen temel hak ve özgürlüklerimin tespiti ile gerekli tedbirlerin
alınması talebidir.

I. OLAYLAR
[Olayların kronolojik anlatımı — chronology-builder skill'i ile uyumlu]

II. İÇ HUKUK YOLLARININ TÜKETİLMESİ
[Süreç zinciri belgelenmiş şekilde]
- İlk derece: ...
- İstinaf: ...
- Temyiz: ...
- Karar düzeltme (varsa): ...
- Kesinleşme tarihi: ...

III. İHLAL İDDİALARI
III.A. Anayasa m.{X} (AİHS m.{Y}) — {Hak Adı} İhlali
- Müdahale: ...
- Hukuki dayanak yokluğu / orantısızlık: ...
- AYM ve AİHM içtihatından destekleyici örnekler

III.B. [Başka hak ihlali varsa]

IV. KABUL EDİLEBİLİRLİK ŞARTLARININ KARŞILANMASI
- İç hukuk tüketildi: ✓
- Süresinde başvuru: ✓
- Anayasal boyut: ✓ (gerekçe)
- Kişisel etkilenme: ✓
- Açıkça dayanaktan yoksun değil: ✓

V. TALEPLER
1. Başvurunun KABUL EDİLEBİLİR olduğuna,
2. {Hak adı} hakkımın İHLAL EDİLDİĞİNİN TESPİTİNE,
3. {ihlal niteliğine göre} ihlalin sonuçlarının ortadan kaldırılması için
   yeniden yargılama yapılmasına veya tazminat ödenmesine,
4. Yargılama giderleri ve vekâlet ücretinin {idare/karşı taraf}a yükletilmesine,
karar verilmesini saygıyla arz ve talep ederim.

[Tarih, başvurucu adı, vekil imzası]

EKLER:
1. Vekâletname
2. Kararlar (ilk derece, istinaf, temyiz, kesinleşme)
3. İlgili belgeler
4. Önceki dilekçeler ve eklerin örnekleri
```

### Adım 6 — Şekil Şartları (6216 m.47)

- **Yazılı** başvuru
- AYM web sayfasındaki **Bireysel Başvuru Formu** doldurulmalı (UYAP üzerinden de mümkün)
- Karar örnekleri ile birlikte
- Harç (varsa — adli yardım talebi mümkün)

### Adım 7 — AYM Ret Kararı Halinde AİHM Yolu

AYM başvurusu reddedilirse — **AİHM** başvurusu için **4 ay** süre var (eski 6 ay; 2022 protokol değişikliği).

```
AYM ret kararı → 4 ay içinde AİHM başvurusu (Strasbourg)
```

AİHM başvurusu ayrı bir uzmanlık alanı; bu skill kapsamı dışında ama **hazırlık altyapısı** zaten sağlanmış olur.

---

## Standart Çıktı Formatı (Hukuki Memo)

```markdown
# AYM Bireysel Başvuru — {matter_adi}

**Karar veren makam:** ...
**Kesinleşme tarihi:** ...
**Başvuru son tarihi:** ... (30 gün)
**İhlal iddiası:** Anayasa m.{X} + AİHS m.{Y}
**Skill versiyonu:** 0.2.0

## I. Olayların Özeti
## II. İç Hukuk Yollarının Tüketilmesi
## III. İhlal Edildiği İddia Edilen Haklar
## IV. Kabul Edilebilirlik Analizi
| Kriter | Durum | Not |
|---|---|---|
| İç hukuk tüketildi | ✓ | ... |
| Süresinde | ✓ | ... |
| Anayasal boyut | ✓ | ... |
| Kişisel etkilenme | ✓ | ... |
| Açıkça dayanaktan yoksun olmama | ✓ | ... |

## V. Esas Hakkında Argümanlar (orantılılık testi)
## VI. Talep
## VII. Dilekçe Taslağı (tam metin)
## VIII. Sonraki Adımlar
- Vekâletname düzenleme
- Karar örneklerinin eki olarak hazırlanması
- AYM web sayfası üzerinden gönderim
- AİHM hazırlık (red halinde 4 ay)

## Ekler
A. Doğrulanmış Mevzuat (6216, Anayasa)
B. AYM İçtihat Referansları (yargi_mcp)
C. AİHS karşılık maddeleri
D. İç hukuk süreç belgeleri (hukuk-rag)
E. MCP Çağrı Logu
F. Eskalasyon Kontrolü
G. Versiyon & Doğrulama
```

## Eskalasyon Tetikleyicileri

1. Sürenin **24 saatten az** kalması → 🚨 acil
2. **İç hukuk yolu tartışmalı** — tüketildiği iddiası kesin değil
3. **Açıkça dayanaktan yoksun** sınırına yakın — ön kabul edilebilirlik testi gerekli
4. Olay **AİHM önünde önceden incelenmiş** mi? (mükerrer başvuru yasağı)
5. **Birden fazla başvurucu** olduğunda kollektif başvuru stratejisi
6. **Tedbir talebi** içeriyorsa (6216 m.49/5) — özel acil işlem

## Notlar

- AYM bireysel başvuruları **çok katı incelenir**; istatistiksel olarak büyük kısmı reddedilir. Başvuru kabul edilebilirlik analizinin **gerçekçi** yapılması gerekir.
- Karar **gerekçeli** beklenir; gerekçesiz reddler kendisi anayasal sorun yaratır.
- AYM, ihlal tespitinden sonra **yeniden yargılama** kararı verebilir veya **tazminat** belirleyebilir.
- AYM **mevzuata ilişkin somut norm denetimi** (m.150 vd.) ile **bireysel başvuru** (m.148/3) farklı yollardır; bu skill sadece bireysel başvuru için.
