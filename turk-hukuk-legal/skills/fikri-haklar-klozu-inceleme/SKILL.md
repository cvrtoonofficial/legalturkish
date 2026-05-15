---
name: fikri-haklar-klozu-inceleme
description: Sözleşmelerdeki fikri haklar (telif & sınai mülkiyet) klozlarını FSEK m.48-52 (telif devir & lisans şekil şartları), SMK m.148 (sınai hak devri) ve TBK genel hükümlere göre inceler. Yazılı şekil, mali hakların ayrı ayrı sayımı, ileride doğacak haklar sınırı, manevi hakların devredilemezliği gibi kritik noktaları kontrol eder.
---

# /fikri-sinai-haklar:fikri-haklar-klozu-inceleme — Fikri Haklar Klozu İnceleme

## Kritik Şartlar Kontrol Listesi

### FSEK (Telif) klozu için
1. **Yazılı şekil zorunluluğu** — FSEK m.52: Mali hakların devri ve lisansı yazılı olmalı. Şifahi devir geçersiz.
2. **Devredilen mali hakların ayrı ayrı sayımı** — FSEK m.52: "Tüm mali haklar" gibi genel ifade yetersiz; FSEK m.21-25'teki haklar (işleme, çoğaltma, yayma, temsil, umuma iletim, vb.) tek tek sayılmalı.
3. **Manevi hakların devredilemezliği** — FSEK m.16-19: Eseri umuma sunma (m.14), adın belirtilmesi (m.15), eserde değişiklik yapılmasını men (m.16) hakları **devredilemez**. Yalnızca kullanım yetkisi verilebilir.
4. **İleride yapılacak eserler** — FSEK m.51: Henüz yaratılmamış eserlere ilişkin sözleşmeler **3 yıllık üst sınır** altında değerlendirilir (genel bir devir geçersiz; periyodik tazeleme gerekir).
5. **Mali hakkın türünden bağımsız teamül vb. yorum yasağı** — FSEK m.52/2: Sözleşmede açıkça yazılmayan hak devredilmemiş sayılır.
6. **Süre ve yer sınırı** — Açık ifade gerekir; aksi takdirde kısıtlı yorum.

### SMK (Marka/Patent/Tasarım/Faydalı Model) klozu için
1. **Devir yazılı şekle bağlı** — SMK m.148 (doğrulanacak); sicil kaydı için TPMK'ya bildirim
2. **Tescile bağlı haklar** — Tescilsiz devir TPMK siciline işlenmedikçe üçüncü kişilere etkili değil
3. **Lisans türü** — Münhasır / yarı münhasır / münhasır olmayan açıkça belirtilmeli
4. **Alt lisans (sub-license)** — Yasak ya da izinli olduğu açıkça yazılmalı
5. **Coğrafi kapsam** — Marka/patent ülkesel; tescil ülkesinde geçerli

### Yazılım sözleşmesi özel (FSEK m.2/1 yazılım eseridir)
1. Kaynak kod sahipliği vs. lisans
2. İstihdam ilişkisinde yaratılan eser — FSEK m.18/2 ve iş hukuku etkisi
3. Açık kaynak bileşenleri (copyleft tetikleyici mi?)
4. Backdoor, telemetri, model eğitim verisi kullanımı

### İstihdam ilişkisi
- FSEK m.18/2: Hizmet akdi ile yaratılan eserler — eser sahipliği çalışan, kullanım hakkı işveren (sözleşmede aksi yazmazsa)
- SMK m.113–122: Çalışan buluşları — hizmet buluşu vs. serbest buluş ayrımı, makul bedel hakkı

## İş Akışı

1. Sözleşme metnini al
2. Fikri haklara dair maddeleri çıkar
3. Yukarıdaki kontrol listesini uygula
4. Kırmızı bayrakları işaretle (eksik şekil, devredilemez hak devri, ileride yapılacak eser üst sınırı)
5. Önerilen redline metni üret
6. `yargi_mcp.search("FSEK 52 yazılı şekil")` ile içtihat referansı çek

## Çıktı

```markdown
## Fikri Haklar Klozu İnceleme Raporu

### Tespit edilen klozlar
- Madde X — telif devri
- Madde Y — marka lisansı
- ...

### Kırmızı bayraklar
1. [FSEK m.52 ihlali] Mali haklar genel ifadeyle devredilmiş; "tüm mali haklar" → ayrı ayrı sayım gerek
2. [FSEK m.16-19 ihlali] Manevi hak "devri" yazılmış → devredilemez; kullanım yetkisi olarak yeniden formüle
3. ...

### Önerilen redline
[Madde madde önerilen metin]

### Mevzuat ve içtihat
- mevzuat_mcp ile doğrulanan maddeler: [...]
- yargi_mcp içtihat: [...]
```
