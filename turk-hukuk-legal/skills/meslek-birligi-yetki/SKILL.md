---
name: meslek-birligi-yetki
description: Türk müzik sektöründeki meslek birliklerinin (MESAM, MSG, MÜYAP, MÜYABİR, SETEM, MÜZİKBİR) yetki sınırlarını, hangi haklara hangi birliğin yetkili olduğunu, FSEK m.42 vd. çerçevesinde birlik aracılığıyla / bireysel olarak takip edilebilecek davaları, bandrol uygulaması, mali hak takibi ve dağıtım sistemini analiz eder. Müzik telif davalarında "doğru tarafın doğru birliği aracılığıyla / bireysel olarak haklarını ileri sürüp sürmediğini" tespit eder.
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
---

# /turk-hukuk-legal:meslek-birligi-yetki — Meslek Birliği Yetki Analizi

> Müzik telif davalarında çoğu zaman gözden kaçan bir nokta: **hangi hakkın takibi için hangi birlik yetkili?** Bireysel takip mümkün mü? Birlik üyesi olunmaması davayı sakatlar mı? Bu skill bu soruları çözer.

## Adım 0 — Zorunlu MCP Çağrıları

### 0.1 Profil okuma
- CLAUDE.md — müvekkilin meslek birliği üyelik durumu

### 0.2 Mevzuat (`mevzuat_mcp`)
- **FSEK m.42 vd.** — meslek birlikleri rejimi
- Telif Hakları Kanunu Genel Tebliği (varsa)
- Meslek Birlikleri Tüzüğü

### 0.3 İçtihat (`yargi_mcp`)
- "meslek birliği yetki" Yargıtay 11. HD
- "FSEK 42 münhasır yetki"
- "bireysel takip mümkün"

---

## Türkiye Müzik Meslek Birlikleri Haritası

> Aşağıdaki yetki dağılımı **uygulama esaslıdır**; özel sözleşme ile değişebilir. Her vaka için `mevzuat_mcp` ile FSEK m.42 vd. doğrulanır.

### Eser sahipleri (besteci, söz yazarı, aranjör)

| Birlik | Yetki alanı | Tipik takip ettiği haklar |
|---|---|---|
| **MESAM** (Türkiye Musiki Eseri Sahipleri Meslek Birliği) | Eser sahipleri (besteci, söz yazarı) | Umuma iletim, çoğaltma, işleme, temsil, mekanik haklar |
| **MSG** (Musiki Eseri Sahipleri Grubu Meslek Birliği) | Eser sahipleri (alternatif birlik) | MESAM benzeri kapsam |

### Bağlantılı hak sahipleri

| Birlik | Yetki alanı | Tipik takip ettiği haklar |
|---|---|---|
| **MÜYAP** (Müzik Yapımcıları Meslek Birliği) | Fonogram yapımcıları | Fonogram üzerindeki bağlantılı haklar (FSEK m.80) |
| **MÜYABİR** (Müzik Yapımcıları Birliği) | Yapımcılar (alternatif) | MÜYAP benzeri |
| **SETEM** (Seslendiren Sanatçılar Meslek Birliği) | İcracılar (müzisyen, vokal) | İcracı sanatçıların bağlantılı hakları |
| **MÜZİKBİR** (Müzik Yapımcıları Sanatçılar Meslek Birliği) | Karma — yapımcı + icracı | Çift sınıf üyelik |

### Diğer ilgili birlikler (referans için)
- **SETEM** kapsamındaki icracı sanatçılar
- Tiyatro, sinema için ayrı meslek birlikleri (FİYAB, OYUNCU-BİR vb.)

---

## İş Akışı

### Adım 1 — Müvekkilin Statüsünü Belirle

```
Sor:
1. Müvekkil eser sahibi mi (besteci/söz yazarı), icracı mı, yapımcı mı, üçü de mi?
2. Hangi meslek birliğine üye? (üyelik kartı / tescil belgesi)
3. Üyelik tarihi ne zaman? (uyuşmazlık tarihinden önce mi sonra mı?)
4. Hangi haklarını birliğe devretmiş, hangilerini elde tutmuş?
   (Üyelik sözleşmesindeki yetki devri kapsamı kritik!)
```

### Adım 2 — Uyuşmazlığın Hangi Hakka Ait Olduğunu Tespit

| İhlal türü | Tipik haklar |
|---|---|
| Online platforma izinsiz yükleme | Umuma iletim (FSEK m.25 + bağlantılı haklar m.80) |
| Konser / canlı icra | Temsil hakkı (FSEK m.24) |
| Reklam müziği kullanımı | Senkron hakkı (mali hak kombinasyonu) |
| Karaoke / arka plan kullanımı | Umuma iletim + mekanik haklar |
| Sample / interpolation | Çoğaltma + işleme hakkı (FSEK m.21, 22) |
| Yapay zeka eğitim verisi | Çoğaltma + tartışmalı: yeni hak kategorisi |
| Yayın (radyo, TV) | Yayın hakkı (m.25 + bağlantılı) |
| CD/kaset basımı | Mekanik çoğaltma + dağıtım |

### Adım 3 — Yetki Eşleştirmesi

#### Bireysel olarak takip edilebilir haller

- Müvekkil meslek birliği üyesi **değilse** → bireysel takip mümkün, FSEK m.42 engellemez
- Müvekkil üye ama uyuşmazlık konusu **hak birliğe devredilmemişse** → bireysel takip
- **Manevi haklar** (FSEK m.14-19) **her zaman bireyseldir** — devredilemez (meslek birliği takip edemez)
- Üye olunmadan önce doğmuş hak (geriye etkili devir geçersiz)

#### Meslek birliği aracılığıyla takip edilmesi gereken haller

- Müvekkil üye + uyuşmazlık konusu hak birliğe devredilmiş → birliğin **münhasır yetkisi**
- FSEK m.42 — "Meslek birliği üyelerinin haklarını korumak için **gerekli her türlü** hukuki işlemi yapma" yetkisi
- Tarife uygulanması, lisans dağıtımı, telif ödemeleri birlik aracılığıyla

#### Tartışmalı durumlar

- **Üye + birliğe devredilmiş + bireysel takip iddiası** → bu durumda Yargıtay 11. HD içtihatı çelişkili (`yargi_mcp` ile güncel tarama şart):
  - Bazı kararlarda bireysel takip kabul edilmez (münhasır yetki)
  - Bazı kararlarda birliğin "ek yetki" kapsamında olduğu, üyenin de bireysel takip edebileceği

### Adım 4 — Karşı Tarafın Kötü Niyet / Lisans İddiası

Karşı taraf "meslek birliğinden lisans aldık" derse:
- Lisans **hangi kapsamda**? (sadece umuma iletim, tüm haklar değil)
- Lisans **hangi süre için**?
- Lisans **hangi platform / kanal** için?
- Müvekkilin **manevi haklarına** yine de saygı zorunlu (FSEK m.14-19 devredilemez)

### Adım 5 — Husumet Yönünden Strateji

Davada doğru husumeti kurmak için:

**Senaryo A:** Müvekkil **üye değil** → Bireysel takip, husumet doğrudan müvekkil
**Senaryo B:** Müvekkil üye + ihlal birliğin yetki alanında → Birliğin müvekkille birlikte / yerine taraf olması (HMK m.59-66 dava arkadaşlığı)
**Senaryo C:** Müvekkil üye + ihlal birlik dışı haklarda (örn. manevi hak) → Bireysel takip

### Adım 6 — Tarife & Tazminat Hesabında Meslek Birliğinin Rolü

- Birlik **standart tarife** yayınlar (Resmî Gazete'de ilan)
- Tazminat hesabında **emsal tarife** referans alınabilir
- FSEK m.68 üç kat rayiç bedel → birliğin tarifesi rayiç bedel için somut delil

---

## Standart Çıktı Formatı (Hukuki Memo)

```markdown
# Meslek Birliği Yetki Analizi — {matter_adi}

## I. Müvekkilin Statüsü
- Eser sahibi / icracı / yapımcı
- Üye olduğu birlik(ler): ...
- Üyelik tarihi: ...
- Devredilen haklar: ...
- Elde tutulan haklar: ...

## II. İhlalin Hangi Hakka Yöneldiği
- FSEK m.X (mali hak) + m.80 (bağlantılı hak)
- ...

## III. Yetki Sonucu
- [✓] Bireysel takip mümkün — gerekçe
- [✓] Birlik aracılığıyla takip zorunlu — gerekçe
- [⚠️] Tartışmalı — uzman görüş gerek

## IV. Strateji
- Davada husumet kurulumu
- Birlikle iş birliği gerekli mi?
- Karşı tarafın "birlik lisansı" iddiasına önleyici cevap

## V. Tarife & Tazminat Hesabında Birliğin Rolü
- Emsal tarife referansı

## Ekler
A. Doğrulanmış Mevzuat (FSEK m.42 vd., m.80, m.14-19)
B. İçtihat (yargi_mcp — yetki konusu güncel kararlar)
C. Üyelik belgesi referansı
D. MCP Çağrı Logu
```

## Eskalasyon Tetikleyicileri

1. **Çok birlik üyeliği** + çelişkili yetki devri → kıdemli görüş
2. **Birliğe karşı dava** (üye - birlik ihtilafı) — özel
3. **Yabancı meslek birliği** + uluslararası boyut (MÖHUK)
4. **Bandrol uygulaması** (FSEK m.81) ihlali — ceza boyutu

## Notlar

- Birlik isim ve yetki sınırları zaman içinde değişebilir; her vaka için `mevzuat_mcp` ile **FSEK m.42 vd.** + birlik tüzüğü teyit edilmelidir.
- **MÜYAP, MÜYABİR, MÜZİKBİR arasında yetki çakışması** zaman zaman gündeme gelir — bu skill çakışmayı tespit edip uzman görüş tavsiyesi verir.
- Eski **MESAM Tarifesi vs MSG Tarifesi** farkı emsal değer hesabında belirleyici olabilir.
