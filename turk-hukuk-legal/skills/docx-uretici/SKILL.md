---
name: docx-uretici
description: Bir skill çıktısını (dilekçe, ihtarname, strateji memo, kronoloji, bilirkişi soru listesi vb.) profesyonel Microsoft Word (.docx) dosyasına dönüştürür. UYAP standardına yakın yazı tipi (Times New Roman 12pt), satır aralığı, kenar boşlukları, sayfa numarası, başlık hiyerarşisi, antet ve imza bloğu uygular. Çıktı doğrudan mahkemeye, KEP'e veya müvekkile sunulmaya hazır seviyededir.
version: 0.4.0
last_legal_review: 2026-05-16
required_mcps: []
optional_mcps:
  - mevzuat_mcp
  - yargi_mcp
applicable_laws: []
---

# /turk-hukuk-legal:docx-uretici — Profesyonel Word Çıktısı

> Skill'lerin Markdown çıktılarını **mahkemeye/KEP'e/müvekkile sunulabilir kalitede** DOCX dosyasına dönüştürür. UYAP'a yüklenecek metin için tasarlandı.

## Adım 0 — Bağlam

### 0.1 Giriş kaynakları
Bu skill diğer skill'lerin çıktısını alır:
- `dilekce-ihtarname` → dilekçe DOCX
- `ihtarname-fsek-smk` → ihtarname DOCX
- `dava-strateji-analiz` → strateji memo + dilekçe DOCX
- `chronology-builder` → kronoloji tablosu DOCX
- `bilirkisi-soru-uretici` → bilirkişi sorular listesi DOCX
- `aym-bireysel-basvuru` → AYM dilekçesi DOCX
- Veya manuel olarak verilen Markdown / Düz metin

### 0.2 Profil okuma
- `CLAUDE.md`'deki **antet** (büro / müvekkil bilgileri), **imza bloğu**, **yazı tipi tercihleri**

---

## İş Akışı

### Adım 1 — Belge Tipini Tanımla

| Tip | Format özellikleri |
|---|---|
| Dilekçe (mahkeme) | Antet yok, başlıkta mahkeme adı, "DAVACI/DAVALI" tablo formatı, dipnot yok, sayfa numarası alt-orta, imza sağ-alt |
| İhtarname (noter) | Antet var (büro/müvekkil), "İHTAR EDEN/MUHATAP", numaralı paragraf, imza |
| Strateji memo (iç) | "GİZLİ — İÇ ÇALIŞMA" filigranı, esnek format |
| AYM bireysel başvuru | Standart başvuru formu yapısı, ekler listesi |
| Bilirkişi soruları | Numaralı liste + alt-numaralı (1.1, 1.2), tablo opsiyonel |
| Kronoloji | Tablo (tarih, olay, kaynak), portre veya yatay |

### Adım 2 — Format Standardı

#### Yazı tipi
- **Ana metin:** Times New Roman 12pt
- **Başlıklar:** Times New Roman 14pt (H1), 13pt (H2), 12pt bold (H3)
- **Tablo içi:** Times New Roman 11pt
- **Alıntı/mevzuat metni:** Times New Roman 11pt, italik veya çerçeve içinde

#### Sayfa düzeni
- Kenar boşlukları: 2.5 cm (üst), 2.5 cm (alt), 3 cm (sol), 2 cm (sağ)
- Satır aralığı: 1.15 — 1.5 (UYAP genelde 1.15 kabul eder)
- Paragraflar arası: 6pt
- Sayfa numarası: alt-orta, "Sayfa X / Y"

#### Stil sözlüğü (her belge için)
- **Mevzuat alıntısı:** "..." kalın italik, kaynak parantez içinde
- **İçtihat alıntısı:** çerçeveli kutu, kaynak alta
- **Madde işaretleri:** numaralı liste (1., 2., 3.) — birden fazla seviye varsa (1.1, 1.2, 2.1)
- **Müvekkil bilgi tablosu:** ince çerçeveli, sol-yaslı

#### Antet (ihtarname / iç memo için)
- Büro adı: 14pt bold
- Adres + iletişim: 10pt
- Sayfa üst-sağ: tarih + ref no
- Logo: opsiyonel (CLAUDE.md'de path verilmişse)

#### İmza bloğu
```
Saygılarımla,

[Tarih]

[Asıl Taraf / Vekil]
[İmza alanı — boşluk]
[Ad Soyad]
[Sicil / kimlik no varsa]
[KEP / UETS adresi]
```

### Adım 3 — Üretme

Python'da `python-docx` kütüphanesi ile veya Pandoc ile dönüşüm. Bu skill çağrıldığında Claude:

1. Giriş kaynağını okur (Markdown / başka skill çıktısı)
2. Belge tipini tespit eder
3. `meta/DOCX-TEMPLATES.md`'deki ilgili template'i seçer
4. Python script çalıştırarak DOCX üretir
5. Dosyayı kullanıcının çıktı klasörüne yazar
6. Önizleme: ilk sayfanın markdown taslağını gösterir

### Adım 4 — Önizleme & Onay

DOCX üretilmeden önce:
1. Kullanıcıya **biçim taslağı** gösterilir (Markdown halinde)
2. Kullanıcı onaylar veya değişiklik ister
3. Onay sonrası DOCX üretilir

### Adım 5 — Dosya Adlandırma Standardı

```
{TARIH}_{TIP}_{MATTER_ID}_{KISA_KONU}.docx

Örnekler:
2026-05-16_dilekce-dava_X-Istanbul_FSEK-tecavuz.docx
2026-05-16_ihtarname_Amuse_sozlesme-fesih.docx
2026-05-16_strateji-memo_X-Istanbul_replik-hazirlik.docx
```

### Adım 6 — Ek Versiyonlar

Eğer büro tipik olarak Word eklenti dışı format gerekirse:
- **PDF** — UYAP'a yüklemeden önce kilit dosya
- **Markdown** — düzenleme ve git takibi için
- **TXT** — düz metin yedek

## Çıktı

```markdown
## DOCX Üretildi

**Dosya:** [TARIH]_[TIP]_[MATTER]_[KONU].docx
**Yol:** ~/Documents/matters/{matter_id}/04-dilekceler/...
**Boyut:** ... KB
**Sayfa sayısı:** ...
**Format kontrolü:**
- [✓] Yazı tipi (Times New Roman 12pt)
- [✓] Kenar boşlukları (2.5 / 2.5 / 3 / 2 cm)
- [✓] Sayfa numarası (alt-orta)
- [✓] Başlık hiyerarşisi
- [✓] İmza bloğu

**Önizleme:** ... (ilk paragraf)

**Sonraki adımlar:**
1. Dosyayı Word'de aç ve son kontrolü yap
2. UYAP'a yükle veya KEP üzerinden gönder
3. matter.md'ye gönderim tarihini işle
```

## Notlar

- Bu skill **content üretmez** — sadece **format dönüştürür**. Content başka skill'den gelmeli.
- DOCX üretimi için `python-docx` veya `pandoc` yüklü olmalı.
- Belge versiyonlamasında her büyük revizyon ayrı dosya olarak kaydedilir (v1, v2, ...).
- Mahkemeye sunum öncesi DOCX → PDF dönüşümü önerilir (UYAP genelde PDF kabul eder).
