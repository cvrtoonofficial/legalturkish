---
name: matter-intake
description: Yeni bir dava, dosya veya konunun (matter) sistematik alımı — standart dizin yapısını oluşturur, matter.md özet dosyasını doldurur, tarafları kaydeder, kritik süreleri takvime ekler, hukuk-rag için yeni bir koleksiyon kurulumunu önerir, profile uygun yetkili mahkemeyi belirler. Her yeni dava bu skill'le başlamalıdır — dosya yönetiminin omurgasıdır.
version: 0.2.0
last_legal_review: 2026-05-16
required_mcps:
  - mevzuat_mcp
optional_mcps:
  - yargi_mcp
  - hukuk-rag
applicable_laws:
  - 6100
  - 1136
---

# /turk-hukuk-legal:matter-intake — Yeni Dosya / Dava Alımı

> Bu skill plugin'in **dosya yönetim omurgasıdır**. Her yeni vaka, sözleşme müzakeresi, ihtilaf veya uyum projesi bu skill'le başlamalıdır. Sonradan eklenen tüm skill çıktıları bu matter'a referansla kaydedilir.

## Adım 0 — Zorunlu MCP Çağrıları

> Bu bölüm `meta/MCP-PROTOCOL.md` çerçevesini uygular.

### 0.1 Profil okuma
- Dosya: `~/.claude/plugins/config/turk-hukuk-legal/CLAUDE.md`
- Yoksa kullanıcıya `/turk-hukuk-legal:soguk-baslangic-mulakat` önerilir.

### 0.2 Mevzuat çekme (`mevzuat_mcp`)
- **Kanun 6100 HMK** — anahtar kelimeler: "görevli mahkeme", "yetkili mahkeme", "dava şartları"
- Konunun özel mevzuatına göre ek aramalar

### 0.3 İçtihat tarama (`yargi_mcp`, opsiyonel)
- Benzer dava içtihatı için: `yargi_mcp.search_bedesten_unified(...)`

### 0.4 `hukuk-rag` koleksiyonu önerisi
- Yeni vaka için yeni `hukuk_rag` koleksiyonu önerilebilir
- Mevcut koleksiyonlar: `mcp__hukuk-rag__hukuk_rag_koleksiyonlar()`

---

## İş Akışı

### Adım 1 — Matter Kimliğini Tanımla

```
Yeni matter için aşağıdaki bilgileri topla:

1. Matter adı: (kısa, dosyaya isim olacak)
2. Matter tipi:
   - [ ] Dava (uyuşmazlık) — ilk derece / istinaf / temyiz / AYM / AİHM
   - [ ] Sözleşme müzakeresi
   - [ ] Uyum / danışmanlık projesi
   - [ ] İhtilaf öncesi danışmanlık / triyaj
   - [ ] M&A / due diligence
   - [ ] İdari süreç / kurum yazışması
   - [ ] Soruşturma / iç inceleme
3. Açılış tarihi: (bugün)
4. Aciliyet:
   - 🔴 Kritik (24 saat içinde aksiyon gerekiyor)
   - 🟡 Yüksek (1 hafta)
   - 🟢 Standart
5. Tahmin edilen süre: (1 ay / 3 ay / 1 yıl / belirsiz)
```

### Adım 2 — Tarafları Kaydet

#### Davacı / Müvekkil / İlk taraf
- Tam ad / unvan
- T.C. / Vergi no
- MERSIS (tüzel kişi ise)
- Tebligat adresi
- KEP / UETS
- Telefon, e-posta
- Vekâletname tipi (genel / özel)
- Vekâletname tarihi
- Müvekkille ilişki (yeni / mevcut)

#### Karşı taraf / Davalı
- Tam ad / unvan
- T.C. / Vergi no (varsa)
- MERSIS
- Tebligat adresi (varsa)
- KEP / UETS
- Vekili (varsa)

#### Üçüncü kişi(ler)
- (Müdahil, tanık, kefil, vb.)

### Adım 3 — Konunun Hukuki Çerçevesini Belirle

#### Maddi hukuk
- Ana norm: ... (örn. FSEK m.66-70, TBK m.49+, SMK m.149)
- Yan normlar: ...

#### Usul hukuku
- Yargı kolu:
  - [ ] Hukuk (HMK 6100)
  - [ ] Ceza (CMK 5271)
  - [ ] İdari (İYUK 2577)
  - [ ] İş (HMK + 7036 SK arabuluculuk dava şartı)
  - [ ] Aile (HMK + TMK 4721)
  - [ ] Tüketici (TKHK 6502)
  - [ ] Fikri ve Sınai Haklar (HMK + FSEK/SMK)
  - [ ] İcra (İİK 2004)
  - [ ] Vergi (VUK + İYUK)
  - [ ] Tahkim (4686 SK + tahkim kuralları)

#### Görevli & yetkili mahkeme
> `mevzuat_mcp.search_within_kanun(mevzuat_no="6100", keyword="görevli")` ile teyit

- Görevli mahkeme: ... (asliye hukuk / asliye ticaret / fikri ve sınai haklar / iş / tüketici / aile / vb.)
- Yetkili yer: ... (HMK m.5-19 yetki kuralları)
- İhtisas mahkemesi: (varsa) İstanbul Anadolu/Avrupa Fikri ve Sınai Haklar HM, vb.

### Adım 4 — Standart Dizin Yapısı Oluştur

Bürünün dosya sisteminde:

```
<matter-id>/
├── 00-vekaletname-musvekkil/         # vekâletname, müvekkil bilgileri, ücret sözleşmesi
├── 01-belgeler-tescil/               # tescil belgeleri, sicil çıktıları, MERSIS
├── 02-deliller/                       # ekran görüntüleri, noter tespiti, fatura, fotoğraf
├── 03-yazismalar/                     # ihtarname, KEP, e-posta, faks
├── 04-dilekceler/                     # dava açılış, cevap, replik, düplik, istinaf, temyiz
├── 05-ictihat-mevzuat/                # araştırma notları, içtihat çıktıları
├── 06-bilirkisi/                      # bilirkişi raporları, itiraz dilekçeleri, ek soru
├── 07-mahkeme-evraklari/              # tutanaklar, duruşma notları, ara kararlar
├── 08-fatura-ucret/                   # vekâlet ücreti, harç, masraf takibi
├── 09-kararlar/                       # ilk derece, BAM, Yargıtay, AYM kararları
└── matter.md                          # dosya özet ve canlı durum
```

### Adım 5 — matter.md Şablonunu Doldur

```markdown
# Matter: {matter_adi}

## Kimlik
- Matter ID: {YIL-NO}
- Açılış tarihi: {tarih}
- Matter tipi: {tip}
- Durum: AKTİF / BEKLEMEDE / KAPALI
- Aciliyet: 🔴/🟡/🟢

## Taraflar
### Müvekkil (Davacı)
- ...

### Karşı Taraf (Davalı)
- ...

### Diğer
- ...

## Hukuki Çerçeve
- Maddi hukuk: {kanun + madde}
- Usul: {HMK/CMK/İYUK}
- Görevli mahkeme: ...
- Yetkili yer: ...
- Esas no: (açıldıktan sonra)

## Süreler ve Kilometre Taşları
| Tarih | Olay | Aksiyon | Durum |
|---|---|---|---|
| ... | İhtarname gönderildi | — | ✓ |
| ... | Cevap süresi sonu | Cevap hazırla | ⏳ |
| ... | İlk duruşma | Hazırlık | ⏳ |

## Talepler / Hedefler
1. ...
2. ...

## Risk Değerlendirmesi
- Önem: ...
- Olasılık: ...
- Tahmini maliyet aralığı: ...

## Çalışma Geçmişi (kronolojik log)
- {tarih}: Matter intake yapıldı
- {tarih}: ...

## İlgili Skill Çağrıları
- /turk-hukuk-legal:tecavuz-triyaj — {tarih, sonuç}
- /turk-hukuk-legal:ihtarname-fsek-smk — {tarih, sonuç}
- ...

## Hukuk RAG Koleksiyonu
- Koleksiyon adı: {matter_id_normalized}
- Yüklenen belgeler: {sayı}
```

### Adım 6 — Süre Takvimine Ekle

İlk anda bilinen tüm süreler takvime eklenir:
- Cevap süresi (HMK m.127 — 2 hafta)
- İstinaf (HMK m.345 — 2 hafta, mevzuat_mcp ile doğrula)
- Temyiz (HMK m.366)
- Bilirkişi raporuna itiraz (HMK m.281 — 2 hafta)
- İhtiyati tedbir kararı sonrası dava açma (HMK m.397)
- KVKK ilgili kişi başvurusu yanıt (m.13 — 30 gün)

Skill, **`siure-hesap-motoru`** ile entegre çalışır — sürelerin **adli tatil, resmî tatil, hafta sonu kaydırması** otomatik hesaplanır.

### Adım 7 — `hukuk-rag` Koleksiyonu Önerisi

Yeni matter için yeni `hukuk_rag` koleksiyonu oluşturulması önerilir:
- Koleksiyon adı: matter_id'nin slug hali (örn. `cvrtoon_x_istanbul`)
- Yüklenecek belgeler:
  - Dava dilekçesi (varsa)
  - Tescil belgeleri
  - Önceki yazışmalar
  - Karşı taraf dilekçeleri (geldikçe)

Profil'in `default_collection` alanı bu yeni koleksiyona güncellenebilir (kullanıcı isterse).

### Adım 8 — İlişkili Matter'lar

Mevcut matter'lar arasında ilişki var mı?
- Aynı taraflar arası başka dosya
- Önceki ihtarname / arabuluculuk
- Üst dosya (örn. ana ihtilaf + alt davalar)

Eğer ilişki varsa `matter.md`'de "İlişkili matter'lar" bölümüne yazılır.

---

## Standart Çıktı Formatı (Hukuki Memo)

Skill nihai çıktısı **`meta/MCP-PROTOCOL.md` §Çıktı Formatı Standartı** şablonunu izler:

```markdown
# matter-intake — {matter_adi}

**Tarih:** {tarih}
**Profil:** {büro}, {ton}
**Skill versiyonu:** 0.2.0

## I. Matter Özeti
[Taraflar, konu, aciliyet, tahmin]

## II. Hukuki Çerçeve
[Görevli & yetkili mahkeme, ana norm]

## III. Yapılan İşlemler
[Dizin oluşturuldu, matter.md dolduruldu, süreler eklendi, hukuk-rag koleksiyonu önerildi]

## IV. Sonraki Adımlar
1. Müvekkille kick-off görüşmesi
2. Belge toplama
3. ...

## V. Riskler ve Eskalasyon
- ...

## Ekler
A. Doğrulanmış Mevzuat (görevli/yetkili mahkeme)
B. İçtihat Referansları
C. matter.md dosyası (yeni)
D. MCP Çağrı Logu
E. Eskalasyon Kontrolü
F. Versiyon & Doğrulama
```

## Eskalasyon Tetikleyicileri

1. Cezai sorumluluk potansiyeli → ek olarak ceza yargı koluna bilgi
2. KVKK m.6 özel nitelikli veri içeriyorsa → kıdemli inceleme
3. Düzenleyici kurum hâlihazırda soruşturma açmış
4. AYM / AİHM yolu açık
5. Sınır ötesi (MÖHUK)
6. Acil ihtiyati tedbir gerek
7. Medya / itibari risk

## Notlar

- Her matter için yeni bir `hukuk_rag` koleksiyonu öneririm — ama tek koleksiyonda birden fazla matter da tutabilirsin.
- Matter ID format önerisi: `{yil}-{tip}-{sira_no}` (örn. `2026-fsek-001`)
- Matter kapanınca `matter.md` durumu `KAPALI` olur ve arşiv klasörüne taşınır.
