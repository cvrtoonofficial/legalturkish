---
name: patent-serbestlik-analizi
description: Türkiye'de pazara çıkarılacak bir ürün/teknolojinin Sınai Mülkiyet Kanunu (6769) m.85 kapsamında üçüncü kişilerin patent ve faydalı model haklarına tecavüz oluşturup oluşturmayacağına dair ön analiz (Freedom-to-Operate triajı) yapar. **Hukuki görüş değildir**; patent vekilinin profesyonel FTO görüşünün yerine geçmez.
---

# /fikri-sinai-haklar:patent-serbestlik-analizi — Patent Serbestlik Analizi (FTO Triajı)

## Davet

```
/fikri-sinai-haklar:patent-serbestlik-analizi
```

Ürünün/teknolojinin teknik tanımını ve pazara giriş tarihini sorar.

## İş Akışı

### Adım 1 — Teknik Tanım Topla
- Ürünün/sürecin teknik özellikleri (claim element ile karşılaştırılabilir nitelikte)
- Hangi alt sistemler / bileşenler
- Hangi pazar (TR yeterli mi, AB ve diğerleri var mı?)
- Pazara giriş tarihi (planlama)

### Adım 2 — Patent Tarama
- **TR:** TPMK Patent Araştırma servisi (turkpatent.gov.tr)
- **EP:** Espacenet (worldwide.espacenet.com)
- **WIPO Patentscope:** patentscope.wipo.int
- **USPTO:** patents.uspto.gov (ABD aile patentleri için)

> Bu skill veritabanlarına doğrudan bağlanmaz. Patent vekiliyle birlikte yapılır.

### Adım 3 — İstem Analizi (Claim Charting)
Tehlikeli patentlerin **bağımsız istemleri**ni ürünle eleman eleman karşılaştır. **Tüm elemanları okunuyorsa (read on)** tecavüz şüphesi var (literal infringement).

| İstem elemanı | Ürün karşılığı | Karşılanıyor mu? | Notlar |
|---|---|---|---|
| ... | ... | ✅/❌/❓ | ... |

**Eşdeğerler doktrini (equivalents):** Literal okunmasa da işlevsel olarak aynı sonucu doğuran teknik özellikler de tecavüz oluşturabilir (Yargıtay 11. HD içtihatı — `yargi_mcp.search`).

### Adım 4 — Savunma Stratejileri
| Strateji | Hukuki temel | Risk |
|---|---|---|
| **Hükümsüzlük talebi** (mahkemede karşı dava) | SMK m.138, 144 — yenilik ve buluş basamağı yokluğu | Patent geçerliyse zarar büyür |
| **Önceki kullanım hakkı** | SMK m.146 (doğrulanacak) | Sıkı belge gerekir |
| **Tükenmiş hak** | Birinci satış sonrası | Sadece patentli ürünün kendisi |
| **Tarifeli istisna (özel kullanım)** | SMK kişisel ve ticari olmayan kullanım istisnası | Ticari ürün için geçerli değil |
| **Lisans alma** | Müzakere | Maliyet |
| **Ürün tasarımını değiştirme (design-around)** | İstemden çıkma | Mühendislik maliyeti |

### Adım 5 — Risk Skoru

| Renk | Anlam |
|---|---|
| 🟢 YEŞİL | Belirgin engelleyici patent bulunamadı |
| 🟡 SARI | Yakın patent var; istem analizi vekil tarafından yapılmalı |
| 🔴 KIRMIZI | Bağımsız istem birebir okunuyor; tasarım değişikliği / lisans şart |

### Adım 6 — Çıktı

```markdown
## Patent Serbestlik Analizi (Ön)

**Ürün:** [...]
**Hedef pazar:** [...]
**Pazara giriş hedefi:** [...]

### Taranan veritabanları
- TPMK: [tarama yapıldı / yapılacak]
- Espacenet: [...]

### Potansiyel engelleyici patentler
| Patent no | Sahibi | Bağımsız istem | Çakışma riski |
|---|---|---|---|
| ... | ... | ... | 🟢/🟡/🔴 |

### Risk skoru: [...]

### Önerilen sonraki adımlar
1. Patent vekiline tam FTO görüşü
2. Risk taşıyan istemler için tasarım değişikliği
3. Hükümsüzlük taraması (paralel)

### Mevzuat: SMK 6769 m.85 (tecavüz halleri), m.144 (hükümsüzlük), m.146 (önceki kullanım) [mevzuat_mcp ile doğrulanmalı]
```

## Disclaimer

Ön analizdir; **profesyonel FTO görüşü patent vekili tarafından düzenlenir**. Mahkeme önünde delil değildir.
