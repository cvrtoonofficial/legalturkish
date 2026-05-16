---
name: chronology-builder
description: Bir davaya ilişkin olayların kronolojik dizilimini sistematik olarak çıkarır. Yüklenen belgelerden ve hukuk-rag taramasından tarih+olay+kaynak üçlüsünü çekip yapılandırılmış bir zaman çizelgesi oluşturur. Replik dilekçesi, tanık dinleme, müvekkil ifade hazırlığı ve duruşma savunması için omurga belge.
version: 0.2.0
last_legal_review: 2026-05-16
required_mcps:
  - hukuk-rag
optional_mcps:
  - mevzuat_mcp
  - yargi_mcp
applicable_laws:
  - 6100
---

# /turk-hukuk-legal:chronology-builder — Kronoloji Kurma

> Türk yargılamasında **kronoloji**, tarafların iddialarını anlamlı bir hikâye olarak sunmasının temel aracıdır. Hâkim, kronolojik bir zaman çizelgesi gördüğünde olayların gelişimini daha net kavrar; tanık ifadelerini bu çizelge üzerine yerleştirir.

## Adım 0 — Zorunlu MCP Çağrıları

### 0.1 Profil okuma
- `~/.claude/plugins/config/turk-hukuk-legal/CLAUDE.md`

### 0.2 `hukuk-rag` taraması (öncelikli)
Matter dosyasındaki belgelerden olay-tarih eşleşmesi:
```
mcp__hukuk-rag__hukuk_rag_ara(
  sorgu="tarih olay süreç",
  dava="<matter_collection>",
  top_k=20
)
```

Ek hedefli aramalar:
- "ihtarname tarih"
- "tebligat tarih"
- "ödeme tarihi"
- "fesih bildirimi"
- "duruşma tarihi"
- "imza tarihi"

### 0.3 `mevzuat_mcp` (yan)
- Süreyi tetikleyen olayların hukuki sonuçlarını doğrulamak için ilgili maddeler

---

## İş Akışı

### Adım 1 — Kapsam Tanımı

Kullanıcıya sor:
- Hangi matter için kronoloji? (matter ID)
- Zaman aralığı: tüm tarih / belirli aralık
- Granülerlik: günlük / saat bazlı / aylık özet
- Amaç:
  - [ ] Dava dilekçesi / replik
  - [ ] Tanık dinleme hazırlığı
  - [ ] Müvekkil ifade
  - [ ] Bilirkişi raporu için olgu özeti
  - [ ] Duruşma savunması
  - [ ] Müvekkile durum brifingi

### Adım 2 — Belge Tarama

#### Yüklenen belgelerden olay çıkarma

Her belgeyi şu açılardan tara:
- **Tarih bilgisi:** belge tarihi, içinde geçen tarihler
- **Olay:** ne oldu (sözleşme imzası, ödeme, fesih bildirimi, vb.)
- **Aktör:** kim yaptı (davacı / davalı / üçüncü kişi)
- **Kaynak:** hangi belge / sayfa / paragraf

#### `hukuk-rag` semantic arama

Hedefli sorgular:
```
mcp__hukuk-rag__hukuk_rag_ara(sorgu="<konu> tarih")
```

Konular:
- Sözleşme yapımı / değişiklikleri
- Ödeme tarihleri
- İhtarname / KEP gönderimleri
- Tebligat tarihleri
- Karşı taraf cevapları
- Olağanüstü olaylar
- Mahkeme aşamaları

#### Sözlü beyanlardan (varsa)

Müvekkille yapılmış toplantı notlarından da olay çekilir.

### Adım 3 — Olayları Yapılandır

Her olay aşağıdaki yapıda kaydedilir:

```yaml
- tarih: 2026-02-13
  saat: (varsa)
  olay: "Davacı, davalıya e-posta yoluyla ihtarname gönderdi"
  aktör: davacı
  konu: "FSEK kapsamında izinsiz eser kullanımı"
  kaynak:
    - belge: "Dava Dilekçesi EK-2A"
    - hukuk-rag-chunk: "Dava_Dilekçesi_0047"
  hukuki-sonuç: "Bildirim niteliği — savunma 3'e karşı (DMCA argümanı)"
  not: "13.02.2026 — arabuluculuk süreci öncesi"
```

### Adım 4 — Çakışan / Çelişen Olaylar

Bazen taraflar aynı olay için **farklı tarih veya yorum** verir:

```yaml
- tarih: ~2025-11 (yaklaşık)
  olay: "Davacının eserinin platforma yüklenmesi"
  aktör: bilinmiyor (3. kişi)
  davacı-iddiası: "İzinsiz, davacının bilgisi dışında"
  davalı-iddiası: (henüz cevap yok)
  not: "Bilirkişi tarafından platform log kayıtlarından net tarih tespit edilecek"
```

Bu çakışmalar **çelişki tablosu** olarak ayrı bölümde toplanır — replik dilekçesinde kullanılır.

### Adım 5 — Hukuki Kilometre Taşları

Bazı olaylar **süre tetikleyicisidir**:

| Olay | Tetiklenen süre |
|---|---|
| Tebligat | Cevap süresi başlangıcı (HMK m.127) |
| İhtarname gönderimi | Temerrüt başlangıcı (TBK m.117); zamanaşımı durması (TBK m.154) |
| Dava açma | Zamanaşımı kesilmesi |
| Karar tebliği | İstinaf süresi (HMK m.345) |
| KVKK ihlali öğrenme | 72 saat bildirim (KVKK m.12) |

Skill, kronolojide bu olayları **🔔** simgesiyle vurgular; tetiklenen süreleri otomatik hesaplama için `siure-hesap-motoru` skill'ine devreder.

### Adım 6 — Kronoloji Çıktı Formatları

#### A. Tablo formatı (default — dilekçeye yapıştırılabilir)

| # | Tarih | Saat | Olay | Aktör | Kaynak |
|---|---|---|---|---|---|
| 1 | 15.10.2025 | — | Davacı, eserin platformda izinsiz kullanımını tespit etti | Davacı | EK-6 İçerik Tespit Belgesi |
| 2 | 13.02.2026 | 14:30 | İhtarname e-posta yoluyla gönderildi | Davacı vekili | EK-2A |
| 3 | 03.03.2026 | — | Arabuluculuk son tutanağı | Arabulucu | EK-3 |
| 4 🔔 | 15.03.2026 | — | Dava açıldı (HMK m.107 belirsiz alacak) | Davacı | Dava Dilekçesi |

#### B. Narrative (replik için akıcı metin)

```
Olayların gelişimi şöyledir:

Ekim 2025'te davacı, eserlerinin davalı platformda izinsiz olarak yer aldığını
tespit etmiş ve İçerik Tespit Belgesi (EK-6) düzenletmiştir. Bu tespit sonrasında,
13.02.2026 tarihinde davalıya e-posta yoluyla ihtarname gönderilmiş (EK-2A),
ihlal eylemlerinin durdurulması talep edilmiştir. Davalının verdiği yanıtlar
sonuç vermediğinden, 03.03.2026 tarihinde 6325 sayılı Kanun m.18/A uyarınca
zorunlu arabuluculuk süreci başlatılmış (EK-3); anlaşmazlığın çözüm bulamaması
üzerine 15.03.2026 tarihinde işbu dava açılmıştır.
```

#### C. Mind map / nedensel zincir

Karmaşık davalar için olayları **neden-sonuç ağı** olarak gösterir:
```
[15.10.2025: Tespit] → [13.02.2026: İhtarname] → [03.03.2026: Arabuluculuk başarısız]
                                                          ↓
                                                  [15.03.2026: Dava]
```

### Adım 7 — Hukuki Çerçeve İlişkilendirme

Her önemli olayın hangi hukuki sonucu doğurduğu işaretlenir:
- Olay → hukuki nitelendirme → ilgili madde

Örnek:
- "13.02.2026: İhtarname e-posta" → "Hukuki bildirim niteliği" → "TBK m.117 + ilgili içtihat"

### Adım 8 — Çapraz Doğrulama

Skill, sunulan belge tarihlerini tutarlılık için kontrol eder:
- Çelişki var mı? (örn. ihtarname tarihinden önce dava açılmış görünüyor)
- Süre uyumu var mı? (örn. cevap 14 günde gelmiş mi?)

Tutarsızlıklar **uyarı kutusunda** çıktıya eklenir.

---

## Standart Çıktı Formatı (Hukuki Memo)

```markdown
# Kronoloji — {matter_adi}

**Tarih aralığı:** {ilk olay} — {son olay}
**Toplam olay:** {N}
**Amaç:** {replik / tanık prep / müvekkil ifade / vb.}
**Skill versiyonu:** 0.2.0

## I. Yönetici Özeti
[3-5 cümle — olayların ana hikâyesi]

## II. Detaylı Kronoloji
[Tablo formatında — tarih, olay, aktör, kaynak]

## III. Çelişkili Olaylar (Davacı vs. Davalı iddiaları)
[Tarafların farklı yorumladığı olaylar]

## IV. Hukuki Kilometre Taşları (süre tetikleyiciler)
[🔔 işaretli olaylar ve tetiklenen süreler]

## V. Olası Boşluklar / Eksik Bilgi
[Hâlâ tarih veya detayı net olmayan olaylar — sonradan tamamlanacak]

## VI. Narrative Anlatım
[Dilekçeye yapıştırılabilir akıcı metin]

## Ekler
A. Doğrulanmış Mevzuat (süre tetikleyici hükümler)
B. İçtihat Referansları (varsa)
C. hukuk-rag Kaynak Referansları (her olay için chunk_id)
D. MCP Çağrı Logu
E. Eskalasyon Kontrolü
F. Versiyon & Doğrulama
```

## Eskalasyon Tetikleyicileri

1. Kronolojide **kritik tarih boşluğu** var ve dava süresi yakın
2. Çelişkili tarihler **bilirkişi incelemesi** gerektiriyor (özellikle dijital olaylar)
3. **Sahtelik iddiası** var (CMK 5271 m.207 vd. — manevi delil)
4. Olaylar **birden fazla yargı kolu** kapsıyorsa (hukuk + ceza + idari)
5. Olay zinciri **AYM/AİHM iç hukuk yolları tüketildi** iddiasını destekliyor

## Notlar

- Kronoloji **canlı** bir belgedir; dava ilerledikçe güncellenir.
- Karşı taraf cevap dilekçesi sunduktan sonra **karşı kronoloji** çıkarılıp çakışmalar netleştirilir.
- Tanıkların **dinlenmeden önce** kronolojiye göre hazırlanması, tutarlı ifade için kritiktir.
