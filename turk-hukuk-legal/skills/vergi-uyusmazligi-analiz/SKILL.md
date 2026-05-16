---
name: vergi-uyusmazligi-analiz
description: İdari vergi uyuşmazlıklarını (tarhiyat itirazı, vergi inceleme, uzlaşma, vergi mahkemesi iptal, tam yargı davası, BAM ve Danıştay süreci) analiz eder. VUK + İYUK + GİB özelgeleri + yargi_mcp GİB endpoint'i ile entegre. Ön tarh, takdir, re'sen ve ikmâlen tarhiyat farklarını, hak düşürücü süreleri (30/60 gün), ihtirazi kayıt sistemini ve uzlaşma stratejisini kapsar.
version: 0.4.0
last_legal_review: 2026-05-16
required_mcps:
  - mevzuat_mcp
  - yargi_mcp
optional_mcps:
  - literatur-mcp
  - hukuk-rag
applicable_laws:
  - 213
  - 2577
  - 3065
  - 193
  - 5520
  - 488
---

# /turk-hukuk-legal:vergi-uyusmazligi-analiz — İdari Vergi Uyuşmazlığı

> Vergi davaları **özel usule** tabidir: İYUK + VUK + sektörel mevzuat. Süreler kısa, uzlaşma fırsatları kritik, GİB özelgelerinin etkisi yüksek.

## Adım 0 — Zorunlu MCP Çağrıları

### 0.1 Profil okuma

### 0.2 Mevzuat (`mevzuat_mcp`)
- **VUK 213** — m.30 (re'sen tarh), m.134-141 (vergi incelemesi), m.376 (ceza ve indirim), Ek m.1 (uzlaşma)
- **İYUK 2577** — m.7 (süre), m.11 (üst makama başvuru), m.27 (yürütmeyi durdurma)
- **GVK 193, KVK 5520, KDVK 3065, ÖTVK** — uyuşmazlık konusuna göre
- **VUK Ek m.1** — Uzlaşma kapsamı

### 0.3 İçtihat & GİB Özelgeleri (`yargi_mcp`)
- Danıştay 3. / 4. / 9. Daire (vergi)
- Danıştay Vergi Dava Daireleri Kurulu (VDDK)
- `yargi_mcp` GİB özelge endpoint'i — 18.000+ özelge

---

## ADIM 1 — Müvekkille Diyalog

```
Sor:
1. Tarhiyat tipi:
   - Ön tarh (VUK m.20)
   - İkmâlen (VUK m.29) — yapılmış tarhiyatın eksikliği
   - Re'sen (VUK m.30) — defter/belge yok / yetersiz
   - Takdir (VUK m.31) — takdir komisyonu marifetiyle
2. Hangi vergi türü? (KDV, KV, GV, ÖTV, Damga, Stopaj, vb.)
3. Tarhiyatın doğduğu olay (vergiyi doğuran olay)?
4. Tarhiyat tutarı + cezası (vergi ziyaı, özel usulsüzlük, vb.)?
5. Tebliğ tarihi (süre başlangıcı kritik)?
6. Vergi incelemesi yapıldı mı?
   - İnceleme raporu var mı?
   - Mükellefe savunma hakkı verildi mi (VUK m.140)?
   - İncelemenin başlama-bitiş süreleri (VUK Ek m.7) aşıldı mı?
7. Uzlaşma denenedi mi?
   - Tarhiyat öncesi uzlaşma (VUK Ek m.11)
   - Tarhiyat sonrası uzlaşma (VUK Ek m.1)
8. GİB özelgesi var mı (varsa numarası)?
9. İhtirazi kayıt tutuldu mu (tartışmalı vergi ödenirken)?
10. Yürütmeyi durdurma talep edilecek mi (İYUK m.27)?
11. Hedef: tam iptal / kısmi iptal / uzlaşma?
```

---

## ADIM 2 — Süre Kontrolü (kritik)

| İşlem | Süre |
|---|---|
| Tarhiyata karşı dava açma | 30 gün (tebliğden) — İYUK m.7 |
| Üst makama başvuru | 60 gün — İYUK m.11 (zımni ret 60 gün) |
| Düzeltme talebi | VUK m.116 — düzeltme yolları |
| Uzlaşma başvurusu | 30 gün (tebliğden) — VUK |
| Yürütmeyi durdurma | Davanın açılmasıyla birlikte talep |
| BAM istinaf | 30 gün |
| Danıştay temyiz | 30 gün |
| AYM bireysel başvuru | 30 gün (kesinleşmeden) |

> **Süreler hak düşürücüdür** — `siure-hesap-motoru` skill ile entegre.

---

## ADIM 3 — Strateji Seçimi

### 3.1 Uzlaşma vs. Dava karar matrisi

| Durum | Strateji |
|---|---|
| Vergi ziyaı cezası ağır + tarhiyat şüpheli | Uzlaşma denemeden dava (uzlaşma sonrası dava açılmaz) |
| Açık idari hata + iptal şansı yüksek | Doğrudan dava + yürütmeyi durdurma |
| Tartışmalı yorum + ödeme yapılmak isteniyor | İhtirazi kayıt ile öde + dava |
| Cezada indirim yeterli | Uzlaşma + ödeme |
| GİB özelgesinin mükellef lehine bağladığı durum | Dava + özelge atfı |

### 3.2 Yürütmeyi durdurma (İYUK m.27)

Şartlar:
- Uygulamayla telafi imkânsız zarar
- Açıkça hukuka aykırılık

Trafik kazasından farklı: vergi davalarında yürütmeyi durdurma genelde **teminat şartı**na bağlı veya teminat aranmaksızın karar verilir.

---

## ADIM 4 — Lehe Argüman Tarama (Sherlock yöntemi)

### Sıkça başarılı argümanlar

1. **Re'sen tarhiyat gerekçesizliği** — VUK m.30 sebebinin yetersiz olması
2. **İnceleme süresinin aşılması** — VUK Ek m.7 (genelde 6 ay)
3. **GİB özelgesinin yok sayılması** — özelge mükellef için bağlayıcı
4. **Defterlerin reddi gerekçesizliği** — re'sen tarh için sebep yetersiz
5. **Savunma hakkının ihlali** — VUK m.140 mükellefe açıklama hakkı
6. **Takdir komisyonu kararı dayanaksız** — VUK m.31
7. **Vergi ziyaı kastı yok** — sadece kusur varsa ceza indirimli (VUK m.344)
8. **Zamanaşımı** — vergiyi doğuran olaydan 5 yıl (VUK m.114)

### `yargi_mcp` ile spesifik tarama

```
yargi_mcp.search("vergi inceleme süre aşımı iptal Danıştay")
yargi_mcp.search("özelge mükellef lehine bağlayıcı")
yargi_mcp.search("re'sen tarh gerekçesiz")
yargi_mcp.search_kvkk_decisions için ilgili → vergi kurullarındaki KVKK boyutları
```

---

## ADIM 5 — Karşı Tarafın (İdarenin) Olası Savunmaları

| İdarenin savunması | Önleyici cevap |
|---|---|
| "Mükellef defter/belge sunmadı" | Sunulan tüm belgeler + savunma hakkının kullanıldığı kanıtla |
| "Re'sen tarhiyat haklıydı" | VUK m.30 sebebinin somut gerekçesizliği |
| "Özelge bağlayıcı değil" | VUK m.413 — özelgeye uygun işlem cezasız |
| "İnceleme süresi makul" | VUK Ek m.7 6 ay; aşılma kanıtı |
| "Vergi ziyaı kastı var" | Tasdikli defterler + kayıt düzenliliği |

---

## Standart Çıktı Formatı

```markdown
# Vergi Uyuşmazlığı Analizi — {tarhiyat_no}

## I. Olgular
- Vergi türü + tutarı
- Tarhiyat tipi
- Tebliğ tarihi
- Hangi olaydan?

## II. Süre Durumu (kritik)
- Dava süresi son tarihi: ...
- Uzlaşma süresi (varsa): ...
- Yürütmeyi durdurma talep edilecek mi: ...

## III. Hukuki Çerçeve
[VUK + İYUK + GVK/KVK/KDVK ilgili maddeleri]

## IV. Lehe Argümanlar
1. [Argüman + ilgili madde + içtihat]
2. ...

## V. İdarenin Olası Savunmaları + Cevaplar
## VI. Strateji
- Uzlaşma denemesi mi, doğrudan dava mı?
- Yürütmeyi durdurma talebi mi?
- İhtirazi kayıt mı?
## VII. GİB Özelgesi Analizi (varsa)

## Ekler
A. Doğrulanmış Mevzuat
B. Danıştay İçtihatı (yargi_mcp)
C. GİB Özelgesi referansları
D. MCP Çağrı Logu
```

## Eskalasyon Tetikleyicileri

1. **Kaçakçılık iddiası** (VUK m.359 ceza boyutu)
2. **Birden fazla vergi türü** + büyük tutar
3. **VUK m.376 indirim + uzlaşma** çakışması
4. **Anayasal hak ihlali** iddiası (AYM)

## Notlar

- Vergi davası **çok hızlı** süreçlidir; ihtirazi kayıt veya itiraz yapmadan ödeme yapılırsa dava kabul edilmez veya zayıflar.
- GİB özelgesi mükellef lehineyse **idarenin sonradan aksini iddia etmesi** çelişkili davranıştır.
- BAM (vergi yönünden) artık devrede; bazı davalar doğrudan Danıştay'a değil önce BAM'a gider — `mevzuat_mcp` ile teyit.
