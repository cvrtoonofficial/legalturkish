---
name: sanatci-sozlesme-inceleme
description: Sanatçı sözleşmelerini (yapımcı sözleşmesi, dijital dağıtım, yayıncı, sync lisans, kayıt anlaşması) FSEK + TBK + MÖHUK çerçevesinde inceler. Amuse, Spotify, Apple Music, Epidemic Sound, Kobalt, AWAL, BandLab, DistroKid, TuneCore gibi yabancı platformların standart şartlarını analiz eder. Mali hakların ayrı sayımı (FSEK m.52), manevi hakların korunması (m.16-19), ileride yapılacak eserler sınırı (m.51), yetki sözleşmesi geçerliliği (MÖHUK + TKHK), sözleşme feshi koşulları, gelir dağılımı şeffaflığı denetler.
version: 0.4.0
last_legal_review: 2026-05-16
required_mcps:
  - mevzuat_mcp
  - yargi_mcp
optional_mcps:
  - literatur-mcp
  - hukuk-rag
applicable_laws:
  - 5846
  - 6098
  - 6502
  - 5718
---

# /turk-hukuk-legal:sanatci-sozlesme-inceleme — Sanatçı / Dijital Dağıtım Sözleşmesi İnceleme

> Sanatçıların yabancı/Türk platform ve yapımcılarla imzaladığı sözleşmeler, FSEK emredici hükümleri açısından sıklıkla **kısmen hükümsüz**dür. Bu skill o boşlukları tespit eder.

## Adım 0 — Zorunlu MCP Çağrıları

### 0.1 Profil okuma
- Müvekkilin statüsü (eser sahibi / icracı / yapımcı)
- Tüketici konumunda olabilir mi? (TKHK m.3)

### 0.2 Mevzuat (`mevzuat_mcp`)
- **FSEK m.48-52** — mali hak devri ve lisansı şekil/içerik şartları
- **FSEK m.16-19** — manevi haklar (devredilemez)
- **FSEK m.51** — ileride yapılacak eserler (3 yıl üst sınır)
- **TBK m.20-25** — genel işlem koşulları (haksız şart denetimi)
- **TBK m.115** — sorumluluk kaldırma emredici sınır
- **TKHK m.5** — haksız şart denetimi (tüketici durumunda)
- **MÖHUK m.20-26** — yabancı unsurlu sözleşme + tüketici

### 0.3 İçtihat (`yargi_mcp`)
- "FSEK 52 yazılı şekil ayrı sayım"
- "manevi hak devri geçersiz"
- "tüketici yetki klozu Yargıtay 13. HD"

### 0.4 Doktrin (`literatur-mcp` + `yoktez-mcp`)
- Sanatçı sözleşmesi, dijital dağıtım, sync lisansı üzerine doktrin

---

## ADIM 1 — Müvekkille Diyalog

```
Sor:
1. Sözleşme tipi: dijital dağıtım / sync / yapımcı kayıt / yayıncı / 360 deal?
2. Karşı taraf: yabancı şirket mi (Amuse, Spotify, Apple, Epidemic Sound,
   Kobalt, AWAL, BandLab, DistroKid, TuneCore, vb.) yoksa Türk yapımcı mı?
3. İmzalanma şekli: clickwrap (web sitesinde tıklama) mı, ıslak imza mı, e-imza mı?
4. İmza tarihi + müvekkilin yaşı (reşit miydi?)
5. Gelir paylaşımı: yüzde, sabit, hibrit?
6. Hangi haklar devredildi / lisansa konu?
7. Süre + coğrafi kapsam?
8. Sözleşme dili (Türkçe veya yabancı)?
9. Yetki / uygulanacak hukuk klozu?
10. Çıkış / fesih klozları?
11. Müvekkilin tüketici konumunda olduğunu iddia edebilir miyiz?
12. Sözleşmeden memnun musun, fesih mi istiyoruz, sadece anlama mı istiyoruz?
```

---

## ADIM 2 — Şekil Şartı Denetimi (FSEK m.52)

| Şart | Kontrol | Sonuç |
|---|---|---|
| Yazılı şekil | Imza var mı (ıslak/e-imza/clickwrap) | Clickwrap tartışmalı — Yargıtay genelde kabul ediyor ama emredici mali hak devirleri için kuşkulu |
| Mali hakların ayrı sayımı | Her FSEK m.21-25 hakkı tek tek mi sayılmış | "Tüm haklar" / "her amaçla" → m.52 ihlali, **bu hak yönünden hükümsüz** |
| İleride yapılacak eserler | Sözleşme gelecek eserler için mi | 3 yıl üst sınır (m.51); aşan kısım hükümsüz |
| Manevi hakların durumu | "Manevi haklar devredildi" yazıyor mu | Devir hükümsüz; sadece kullanım yetkisi mümkün (m.16-19) |
| Tarafların ehliyeti | Müvekkil reşit miydi? | Küçük adına velinin imzası şart |

---

## ADIM 3 — Standart Klozlar ve Yaygın Sorunları

### 3.1 Dijital dağıtım (Amuse, DistroKid, TuneCore, BandLab benzeri)

- **Gelir paylaşımı:** Genelde sanatçıya %85-100, platforma %0-15 + servis ücreti
- **Süre:** Süresiz / yıllık yenileme — her iki türü de geçerli ama tüketici durumunda esnek değerlendirme
- **Hak kapsamı:** Sadece dağıtım amaçlı **münhasır olmayan lisans** mı, yoksa fiilen tam mali hak devri mi? — Sözleşme dili "license to distribute" ile "transfer of rights" çok farklı
- **Çıkış:** Sanatçı sözleşmeden çıkarsa eserler kaldırılır mı? Geçmiş süre için telif iade edilir mi?

### 3.2 Yapımcı kayıt sözleşmesi

- **Mali hak devri** — yapımcıya (FSEK m.80 bağlantılı hak ek)
- **Münhasırlık** — çoğu yapımcı sözleşmesi münhasır; çıkış zor
- **Avans + recoupment** — verilen avans gelirden mahsup edilir; mahsup öncesi sanatçıya ödeme yok
- **Reversion (geri dönüş) klozları** — bazı sözleşmelerde belirli süreden sonra haklar geri döner; FSEK m.51 ile uyumlu
- **Sanatçı kontrolü** — eserin nasıl tanıtılacağı, kapağı, sunumu — manevi hakla bağlantılı

### 3.3 Sync lisans

- Tek seferlik kullanım (reklam, film, dizi)
- Belirli kapsam (örn. "1 yıl, TR + AB, TV + dijital")
- **Master ve publishing ayrımı** — iki taraf izni
- Sync fee + performance royalty ayrı kalemler

### 3.4 360 deal

- Yapımcı sanatçının **tüm gelir kaynaklarından** pay alır (konser, marka, satış)
- Türk hukukunda emsali sınırlı; **TBK m.27** dengesizlik denetimi devreye girer

### 3.5 Yabancı platform standart şartları

**Amuse, Spotify, Apple Music, Epidemic Sound, Kobalt:**

- Uygulanacak hukuk: genelde yabancı (İsveç, İngiltere, ABD)
- Yetki: yabancı mahkeme veya tahkim (LCIA, AAA, vb.)
- Anchor: kullanıcı dünya çapında lisans veriyor

**Sıkça karşılaşılan sorunlar:**
- Mali hak devri "transfer" olarak yazılmış (lisans değil)
- Manevi haklara dair açık koruma yok
- Tek taraflı değiştirme yetkisi (TBK m.20-25 dengesizlik)
- Fesih koşulları asimetrik
- Telif ödemesi şeffaflığı düşük

---

## ADIM 4 — Türk Hukuku Uygunluk Kontrolü

| Kontrol noktası | Hukuki sonuç (uygun değilse) |
|---|---|
| FSEK m.52 ayrı sayım | "Tüm haklar" ifadesi hükümsüz; sözleşmenin spesifik mali hak yönünden zayıf |
| FSEK m.16-19 manevi hak | "Devir" ifadesi hükümsüz; kullanım yetkisi olarak yorumlanır |
| FSEK m.51 ileri eser | 3 yılı aşan kapsam hükümsüz |
| TBK m.27 emredici hüküm | Kanuna aykırı kısmen geçersizlik |
| TBK m.20-25 GİK denetimi | Sürpriz şart / dengesizlik → şart geçersiz |
| TBK m.115 sorumluluk | "Tüm sorumluluk kaldırıldı" hükümsüz (kasıt+ağır kusur) |
| TKHK m.5 (tüketici ise) | Haksız şart → geçersiz |
| MÖHUK m.20-26 (yabancı unsur) | Yabancı hukuk seçimi tüketici aleyhine ise sınırlı (m.26/2) |

---

## ADIM 5 — Çıkış / Fesih Stratejisi

### 5.1 Sözleşmesel fesih

- Belirsiz süreli: TBK m.347 / sözleşmeye göre genelde ihbarlı fesih hakkı
- Belirli süreli: süre sonuna kadar bağlayıcı, **haklı sebepler** istisna

### 5.2 Haklı sebepler

- Karşı tarafın ifa etmemesi (ödeme yapmama, hesap vermeme)
- Sözleşmenin temel amacına aykırı kullanım
- Önemli aldatma / hata

### 5.3 Hükümsüzlük iddiası

- FSEK m.52 ihlali → ilgili mali hak yönünden hükümsüz
- TBK m.27 ihlali → kısmî geçersizlik veya bütünüyle geçersizlik

### 5.4 Yabancı sözleşmeden çıkış

Eğer yetki klozu yabancı mahkeme ise:
- **Türk hukuku zorunlu uygulamaları** (FSEK emredici hükümleri) yine geçerli
- **Tüketici koruması (TKHK + MÖHUK m.26)** Türk mahkemesini yetkili kılabilir
- Detay için → `/turk-hukuk-legal:sinirostesi-sozlesme-fesih` skill'i

---

## Standart Çıktı Formatı

```markdown
# Sanatçı Sözleşmesi İnceleme — {sozlesme_tipi}, {karsi_taraf}

## I. Sözleşme Özeti
- Tip: ...
- Taraflar: ...
- İmza tarihi: ...
- Süre + kapsam: ...

## II. Türk Hukuku Uygunluk Denetimi (kontrol listesi)
[Her madde ✓/⚠️/❌]

## III. Kırmızı Bayraklar
1. **[Madde X — FSEK m.52 ihlali]** Mali hakların ayrı sayımı yapılmamış
   → İlgili mali hak yönünden hükümsüz argümanı
2. ...

## IV. Sarı Bayraklar
[Müzakere değiştirilebilir noktalar]

## V. Yeşil — Kabul Edilebilir
[Sorunsuz maddeler]

## VI. Çıkış Senaryoları
- Sözleşmesel fesih: ...
- Haklı sebep fesih: ...
- Hükümsüzlük iddiası: ...
- Yabancı yetki kaldırma argümanı (varsa): ...

## VII. Karşı Tarafa Argümanı Bizim Yapacağımız Yanıtlar
[Sherlock yöntemi — adım 3 örüntüsü]

## Ekler
A. Doğrulanmış Mevzuat
B. İçtihat Referansları
C. Doktrin (varsa)
D. MCP Çağrı Logu
```

## Notlar

- Amuse, Spotify gibi platformlar **clickwrap** ile imza alır — Türk hukukunda **mali hak devri için yazılı şekil tartışması** kritik (FSEK m.52).
- Sanatçı **tüketici** sayılması her vaka için tartışılır — TKHK m.3 müvekkilin ticari/profesyonel kullanım dışında işlem yaptığını gösterirse mümkün.
- Sözleşme yabancı dilse Türkçe tercüme yapılmalı; **805 SK** "İktisadi Müesseselerde Mecburi Türkçe Kullanılması Hakkında Kanun" tartışılır.
- Yabancı tahkim klozları Türk hukukunda dolaylı olarak uygulanır (Türk mahkemesi yetki tartışması) — sınır ötesi skill ile entegre.
