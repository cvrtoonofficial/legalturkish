---
name: icerik-kaldirma-bildirim
description: İnternette telif (FSEK 5846) veya sınai mülkiyet (6769 SMK) ihlali içeren içerikler için kaldırma talebi hazırlar. Türk hukukunda iki ana ray vardır: (1) **5651 sayılı Kanun m.9** (kişilik hakkı + içerik kaldırma; sulh ceza hâkimliği yolu) ve (2) **platform iç uyar-kaldır mekanizmaları** (YouTube Copyright, Meta IP Reports, vb.). Hangi rayda hareket edileceği duruma göre değişir.
---

# /fikri-sinai-haklar:icerik-kaldirma-bildirim — İçerik Kaldırma Bildirimi

> ABD'nin **DMCA §512** mekanizmasının Türk hukukundaki birebir karşılığı **yoktur**. Bu skill iki paralel rayı yönetir:
> 1. **Hukuki ray:** 5651 sayılı Kanun m.9 / m.9-A (içerik çıkarma, erişim engelleme) — sulh ceza hâkimliği başvurusu
> 2. **Platform rayı:** YouTube, Meta, X, TikTok, vb. dahili uyar-kaldır prosedürleri (FSEK uyarınca hak sahipliği beyanına dayalı)

## Davet

```
/fikri-sinai-haklar:icerik-kaldirma-bildirim
```

İhlal türünü (FSEK telif / marka tecavüzü / haksız rekabet / kişilik hakkı + IP karması) ve platformu sorar.

## İş Akışı

### Adım 1 — Hangi Ray?

| Senaryo | Önerilen ray |
|---|---|
| YouTube'a yüklenmiş telif eseri | Platform rayı (Content ID / YouTube Copyright Form) — hızlı, ücretsiz |
| Meta/Instagram'da sahte marka satışı | Platform rayı (Meta Brand Rights Protection) + ileri aşamada Türk yargısı |
| Web sitesinde tam içerik kopyalama | 5651 m.9 sulh ceza hâkimliği + FSEK |
| Türkiye'den erişilen yabancı korsan site | 5651 m.8 erişim engelleme + uluslararası boyut |
| Söz konusu içerik kişilik hakkı + telif | 5651 m.9 kişilik hakkı + paralel FSEK |
| Marka tecavüzü içeren reklam/satış | Platform + ihtarname + dava |

> **Not:** 5651 m.9 esasında **kişilik haklarının ihlali** için tasarlanmıştır. Telif ihlalinde uygulanabilmesi içtihatla genişlemiştir; bazı sulh ceza hâkimlikleri reddetmektedir. `yargi_mcp.search("5651 m.9 telif FSEK")` ile güncel içtihatı tara.

### Adım 2 — Hak Sahipliğini Belgele

Platform formları ve sulh ceza başvurusu **hak sahipliği belgesi** ister:

- **FSEK:** Eser örneği, ilk yayın tarihi, kayıt (varsa — meslek birliği üyeliği, bandrol), devir zinciri
- **Marka:** TPMK tescil belgesi (güncel)
- **Patent/tasarım:** Tescil belgesi + korumanın geçerliliği
- **Bağlantılı haklar:** Yapımcı/icracı sıfatını gösterir belgeler

### Adım 3 — İhlal Adresini ve İhlal Tipini Belirle

- Tam URL (ekran görüntüsü değil, **link**)
- Yayın tarihi
- Görüntülenme/erişim verileri
- Türkiye'den erişim doğrulaması (yer sağlayıcı tespiti için)
- Yer sağlayıcı / içerik sağlayıcı bilgileri (whois, BTK kayıtları)

### Adım 4a — Platform Rayı

Her büyük platformun kendi uyar-kaldır formu var. Genel yapı:

```
Hak sahibi: [Ad/Unvan]
Yetki: [Eser sahibi / Münhasır lisans alan / Vekil — vekâletname ekli]
İhlal eden içerik URL: [...]
Hak iddiasının türü: [Telif / Marka / Tasarım]
Hak sahipliği belgesi: [Ek]
İyiniyet beyanı: ["Bu içeriğin kullanımına yetki verilmediğini iyiniyetle beyan ederim"]
Yanıltıcı bildirim cezası beyanı: ["Yanıltıcı bildirim halinde doğacak sorumluluğu kabul ederim"]
İmza ve iletişim: [...]
```

**Önemli yanıltıcı bildirim riski:** Platform rayında yanıltıcı / kötü niyetli kaldırma talebi **karşı tarafa tazminat** doğurur (TBK m.49 + platform sözleşmesi). Özellikle parodi / eleştiri / haber kullanımı (FSEK m.36-38 — istisnalar) durumlarında dikkat.

### Adım 4b — Hukuki Ray (5651 m.9)

Sulh ceza hâkimliğine başvuru yapılır. Tipik içerik:

```
SAYIN ... SULH CEZA HÂKİMLİĞİ'NE

KONU: 5651 sayılı Kanunun 9. maddesi uyarınca [URL] adresindeki içeriğin çıkarılması / erişimin engellenmesi talebi.

BAŞVURUCU:
[Bilgiler + vekâletname]

OLAY VE TALEP:
1. Müvekkilim, [eser/marka/...] üzerinde [FSEK m.X / SMK m.X] uyarınca hak sahibidir.
2. [URL] adresinde tarafımızca tespit edilen içerik, müvekkilin haklarını [...] şekilde ihlal etmektedir.
3. [Önceki uyarı/ihtarname yapıldıysa] ...
4. İçeriğin acilen çıkarılması; içerik çıkarılmıyorsa Türkiye'den erişiminin engellenmesi gerekmektedir.

DELİLLER:
- Hak sahipliği belgesi (Ek-1)
- İçerik ekran görüntüsü + URL (Ek-2)
- Noter tespit zaptı (varsa — Ek-3)

TALEP:
... URL adresindeki içeriğin 5651 m.9/3 uyarınca [içerik çıkarma / erişim engelleme] kararı verilmesini saygıyla arz ve talep ederim.
```

> **Not:** 5651 m.9'un birden fazla fıkrası ve farklı yargı yolları (sulh ceza hâkimliği, BTK kararı, idari süreç) var. Tam metin `mevzuat_mcp.search_within_kanun(mevzuat_no="5651", keyword="erişimin engellenmesi")` ile doğrulanmalıdır.

### Adım 5 — Süre Yönetimi

- Platform rayında: 24-72 saat (büyük platformlar SLA)
- Sulh ceza hâkimliği: 5651 m.9/5 — talep 24 saat içinde karara bağlanır (mevzuat doğrulamasıyla)
- Karşı bildirim (counter-notice) varsa platform içeriği geri yükleyebilir → tahkim ya da dava

### Adım 6 — Eskalasyon Triggerları

Sadece taslak üretme, **eskalasyon işaretle**:

- Hak sahipliği zinciri tartışmalı (eser sahipliği uyuşmazlığı)
- İçerik gazetecilik / kamu yararı kapsamında olabilir (FSEK m.36-38)
- Yer sağlayıcı yurt dışında ve uluslararası dilekçe gerek
- Platform yanıt vermiyor, idari yola gidilecek
- Bilişim suçu boyutu var (TCK m.243-246)

### Adım 7 — Çıktı

```markdown
## İçerik Kaldırma Bildirimi Taslağı

**Ray:** [Platform / 5651 m.9 / Paralel]
**Platform:** [YouTube / Meta / X / Web sitesi]
**Hak türü:** [FSEK telif / Marka / ...]
**Aciliyet:** [Yüksek / Normal]

---

### Bildirim/Başvuru metni
[Yukarıdaki şablonların ilgili olanı]

### Ekler kontrol listesi
- [ ] Hak sahipliği belgesi
- [ ] İhlal URL'leri tam liste
- [ ] Ekran görüntüleri (noter tespit varsa öncelikli)
- [ ] Vekâletname
- [ ] İyiniyet beyanı

### Mevzuat doğrulaması
- 5651 m.9: [mevzuat_mcp ile doğrulandı / doğrulanmadı]
- FSEK m.X: [...]
- SMK m.X: [...]

### Yanıltıcı bildirim riski uyarısı
[Parodi / haber / kamu yararı istisnaları gözden geçirildi mi?]

### Sonraki adımlar
1. Avukat kontrolü
2. Platform sevki / sulh ceza başvurusu
3. Yanıt için süre takvimi
4. Karşı bildirim halinde plan
```

## Disclaimer

5651 ve FSEK içtihatı dinamik. Her başvuruda güncel karar tarama yapılmalı.
