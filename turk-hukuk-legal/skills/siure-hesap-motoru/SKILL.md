---
name: siure-hesap-motoru
description: HMK, İYUK, CMK, İİK ve özel mevzuat sürelerini hesaplar. Tebliğden itibaren süreler, adli tatil (HMK m.102), resmî tatil, hafta sonu kaydırması, hak düşürücü süre vs. zamanaşımı ayrımı, geriye doğru ve ileriye doğru hesaplama. Cevap dilekçesi (m.127 — 2 hafta), istinaf (m.345), temyiz (m.366), bilirkişi rapor itirazı (m.281), KVKK m.13 (30 gün), TPMK marka itirazı (2 ay), ihtiyati tedbirden sonra dava açma (m.397) gibi süreleri kapsar.
version: 0.2.0
last_legal_review: 2026-05-16
required_mcps:
  - mevzuat_mcp
optional_mcps:
  - yargi_mcp
applicable_laws:
  - 6100
  - 2577
  - 5271
  - 2004
  - 6698
  - 6769
---

# /turk-hukuk-legal:siure-hesap-motoru — Hukuki Süre Hesaplama Motoru

> Türk yargı pratiğinde **süreler kritiktir** — hak düşürücü süreler kaçırıldığında dava reddedilir, zamanaşımı süreleri gözden kaçırıldığında hak kaybı doğar. Bu skill **takvim hesabını otomatize eder**, ama hâkim takdiri içeren konularda manuel teyit önerilir.

## Adım 0 — Zorunlu MCP Çağrıları

### 0.1 Profil okuma
- `~/.claude/plugins/config/turk-hukuk-legal/CLAUDE.md`

### 0.2 Mevzuat çekme (`mevzuat_mcp`)
Süre hesabının dayandığı kanun maddesi her zaman doğrulanır:
- **Kanun 6100 HMK** — anahtar: "süre", "tebliğ", "adli tatil" (m.92-105, 102 adli tatil)
- **Kanun 2577 İYUK** — anahtar: "süre", "tebliğ" (idari davada farklı kurallar)
- **Kanun 5271 CMK** — anahtar: "süre" (ceza yargılaması)
- **Kanun 2004 İİK** — anahtar: "süre" (icra-iflas)
- Konuya özel: KVKK 6698 m.13, SMK 6769 itiraz süreleri

### 0.3 Resmi tatil & adli tatil verisi
- Adli tatil: HMK m.102 — **20 Temmuz - 31 Ağustos** (her yıl `mevzuat_mcp` ile doğrula; HSK kararıyla değişebilir)
- Resmî tatiller: 2429 sayılı Ulusal Bayram ve Genel Tatiller Hakkında Kanun
  - 1 Ocak (Yılbaşı)
  - 23 Nisan (Ulusal Egemenlik ve Çocuk Bayramı)
  - 1 Mayıs (Emek ve Dayanışma Günü)
  - 19 Mayıs (Atatürk'ü Anma, Gençlik ve Spor Bayramı)
  - 15 Temmuz (Demokrasi ve Milli Birlik Günü)
  - 30 Ağustos (Zafer Bayramı)
  - 29 Ekim (Cumhuriyet Bayramı)
  - Ramazan Bayramı (3 gün — hicri takvime göre değişir)
  - Kurban Bayramı (4 gün — hicri takvime göre değişir)
- Tatil hesabı için her yıl güncel **Resmî Gazete'den dini bayram tarihleri** alınmalıdır.

---

## İş Akışı

### Adım 1 — Süre Tipini Tanımla

| Tip | Özellik | Uzatılabilir mi? |
|---|---|---|
| **Hak düşürücü süre** | Kaçırılırsa hak biter, hâkim re'sen gözetir | Hayır (kural olarak) |
| **Zamanaşımı** | Kaçırılırsa talep edilebilir ama karşı tarafın itirazıyla reddedilir | Hayır (tahkik aşamasında ileri sürülmezse vazgeçilmiş sayılır) |
| **Düzenleyici süre** | Kaçırma sonucu ağır değil | Çoğu zaman evet |
| **Cezai süre** | Ceza yargılaması özel kuralları | CMK m.40 uyarınca |

### Adım 2 — Başlangıç ve Bitiş Noktası

**Süre ne zaman başlar?**

| Olay | Başlangıç |
|---|---|
| Tebligat → süre başlar | Tebliğin **ertesi günü** (HMK m.92/2) |
| Kararın **açıklanması** | Bazı durumlarda |
| Resmî Gazete'de **ilan** | Bazı düzenlemelerde |
| **Öğrenme** | İdari işlemlerde (örn. zımni ret) |
| Olayın **gerçekleşmesi** | Zamanaşımı için |

**Süre nasıl biter?**

- **Adli tatil içine düşerse:** Tatil bitiminde işlemeye devam eder (HMK m.102)
- **Resmî tatil günü:** Süre, tatilin **sona erdiği günü izleyen iş günü**ne uzar (HMK m.93)
- **Hafta sonu:** Pazar günü tatil sayılır; sürenin son günü pazar ise pazartesi'ye uzar

### Adım 3 — Süre Türleri Referans Tablosu

> Aşağıdaki tablo **`mevzuat_mcp` ile her kullanımda doğrulanır**. Mevzuat değişebilir.

#### Hukuk yargılaması (HMK 6100)

| İşlem | Süre | Madde |
|---|---|---|
| Cevap dilekçesi | 2 hafta | m.127 |
| Cevaba cevap (replik) | 2 hafta | m.136 |
| İkinci cevap (düplik) | 2 hafta | m.136 |
| İhtiyati tedbir kararı sonrası dava | 2 hafta | m.397 |
| Bilirkişi raporuna itiraz | 2 hafta | m.281 |
| Belirsiz alacak — talep artırımı | Tahkikat sonuna kadar | m.107 |
| İstinaf | 2 hafta (tebliğden) | m.345 (verify) |
| Temyiz | 2 hafta (tebliğden) | m.366 (verify) |
| Karar düzeltme | Belirli durumlarda | m.378 (verify) |
| Kesinleşmiş hükmün iadesi | 3 ay (öğrenmeden), 10 yıl üst sınır | m.376 (verify) |

#### İdari yargılama (İYUK 2577)

| İşlem | Süre |
|---|---|
| İptal davası | 60 gün (genel) / 30 gün (özel hallerde) |
| Tam yargı davası | 60 gün |
| İstinaf (BAM) | 30 gün |
| Temyiz (Danıştay) | 30 gün |
| Zımni ret oluşumu | 60 gün (idari başvuruya cevap gelmezse) |

#### Ceza yargılaması (CMK 5271)

| İşlem | Süre |
|---|---|
| Soruşturmaya itiraz (sulh ceza) | 15 gün |
| Karara itiraz | 7 gün |
| İstinaf | 7 gün |
| Temyiz | 15 gün |
| Yargılamanın yenilenmesi | Süresiz (CMK m.311+) |

#### İcra-iflas (İİK 2004)

| İşlem | Süre |
|---|---|
| Ödeme emrine itiraz | 7 gün (icra mahkemesine) |
| Şikâyet | 7 gün |
| İhalenin feshi | 7 gün |

#### KVKK 6698

| İşlem | Süre |
|---|---|
| İlgili kişi başvurusuna yanıt | 30 gün (m.13) |
| Veri ihlali bildirimi | 72 saat (m.12 + Kurul kararları) |
| Kurul kararına dava | 30 gün (İYUK genel kuralı) |

#### SMK 6769 (TPMK süreçleri)

| İşlem | Süre |
|---|---|
| Marka başvurusuna itiraz (3. kişi) | 2 ay (ilan tarihinden) |
| YİDD (Yeniden İnceleme ve Değerlendirme Dairesi) kararına itiraz | 2 ay |
| Marka yenileme | Koruma sona ermeden 6 ay önce |
| Patent yıllık ücreti | Her yıl başvuru tarihinden itibaren |

#### Zamanaşımı / Hak düşürücü süreler

| Konu | Süre | Dayanak |
|---|---|---|
| Haksız fiil — genel | 2/10 yıl (TBK m.72) | TBK |
| Sözleşmesel — genel | 10 yıl (TBK m.146) | TBK |
| Tüketici ayıbı | 2 yıl (TKHK m.11) | TKHK |
| İş alacakları | 5 yıl (genel) | İş K. m.32 |
| Kıdem tazminatı | 5 yıl | İş K. |
| Marka hükümsüzlüğü — sessiz kalma | 5 yıl (kullanıcının bilgisi varsa) | SMK m.157 (verify) |
| AYM bireysel başvuru | 30 gün (kararın kesinleşmesinden) | 6216 SK |
| AİHM başvurusu | 4 ay (eski 6 ay; iç hukuk yolu tükendikten) | AİHS Madde 35 |

### Adım 4 — Hesaplama

#### Algoritma

1. **Başlangıç günü** belirle (tebligat tarihi varsa o günün **ertesi**)
2. **Süre miktarı**nı uygula (gün / hafta / ay / yıl)
3. **Adli tatil etkisi**:
   - Süre adli tatil **içine düşerse**, tatil günleri sayılmaz; süre tatil bitiminde devam eder
   - Süre adli tatil **boyunca duruyorsa** (HMK m.102 — sınırlı istisnalar dışında), tatil bitiminde 1 hafta ek (m.102/3)
4. **Resmî tatil & hafta sonu**:
   - Sürenin son günü resmî tatile veya hafta sonuna denk gelirse, ertesi iş gününe uzar
5. **Son gün** hesaplanır

#### Örnek Hesap

```
Senaryo: Cevap dilekçesi süresi
- Tebligat tarihi: 1 Temmuz 2026 (Çarşamba)
- Süre: 2 hafta (HMK m.127)
- Başlangıç: 2 Temmuz (ertesi gün)
- Sonu: 16 Temmuz (Perşembe)
- Adli tatil etkisi: 20 Temmuz başlıyor, son gün adli tatil dışında → etkilenmez
- Resmî tatil: 15 Temmuz Demokrasi Günü — son gün 16 Temmuz olduğu için etkilenmez
- ✅ Son tarih: 16 Temmuz 2026 Perşembe
```

```
Senaryo: Tebligat 18 Temmuz 2026
- Başlangıç: 19 Temmuz
- 2 hafta → normalde 2 Ağustos
- Adli tatil 20 Temmuz - 31 Ağustos — süre tatil içine düşüyor
- Son gün adli tatil sonrası 1 hafta ek (HMK m.102/3 — verify)
- ✅ Son tarih: 7 Eylül 2026 (1 Eylül + 1 hafta) — verify
```

### Adım 5 — Riskler ve Uyarılar

#### Sık karşılaşılan tuzaklar

1. **Tebliğden itibaren vs. öğrenmeden itibaren** — bazı sürelerde "öğrenmeden" kuralı uygulanır (idari işlemlerde)
2. **Hafta sayma** — "iki hafta" 14 takvim günü; bazı düzenlemelerde "iş günü" sayılır (CMK örn.)
3. **Adli tatil istisnaları** — ihtiyati tedbir, delil tespiti, çocuk haklarına ilişkin işlemler adli tatilde de görülür (HMK m.102/1)
4. **Resmî tatil + hafta sonu üst üste** — Pazartesi resmî tatilse ve sürenin son günü Pazartesi'yse, sürelilik Salı'ya uzar (zincirleme)
5. **Birleşen süreler** — bazen iki ayrı süre aynı olaya bağlanır (örn. ihtiyati tedbir kararı sonrası **hem 2 hafta dava açma hem de zamanaşımı süresi** ayrı işler)

### Adım 6 — Takvim Entegrasyonu

Skill çıktısı **takvime atılabilir formatta** üretilir:
- iCal (.ics) çıktısı
- Google Calendar / Outlook ek bilgisi
- `matter.md` üzerinden süre satırı

Önceden kurulu takvim MCP varsa otomatik ekleme önerilir.

---

## Standart Çıktı Formatı (Hukuki Memo)

```markdown
# Süre Hesabı — {konu}

**Hesaplanan süre:** {N gün/hafta/ay}
**Dayanak:** {kanun + madde}
**Başlangıç:** {tarih}
**Hesaplanan son gün:** {tarih}

## I. Olgular
[Başlangıç olayı: tebligat / öğrenme / olay tarihi]

## II. Hukuki Çerçeve
[Süre dayanağı — mevzuat_mcp ile doğrulandı]

## III. Hesaplama Detayı
| Adım | Tarih | Not |
|---|---|---|
| Başlangıç | ... | tebligat ertesi günü (HMK m.92/2) |
| Ham bitiş | ... | süre × gün |
| Adli tatil etkisi | ... | yok / ek 1 hafta / vb. |
| Tatil/hafta sonu kaydırması | ... | ... |
| **Son tarih** | **...** | |

## IV. Sonuç ve Öneri
- Son tarih: ...
- Güvenlik payı önerisi: son tarih - 3 iş günü
- Aksiyon: ...

## V. Riskler
- ...

## Ekler
A. Doğrulanmış Mevzuat
B. İçtihat (gerekli ise süre yorumu)
C. Takvim ekleme önerisi (.ics)
D. MCP Çağrı Logu
E. Eskalasyon Kontrolü
F. Versiyon & Doğrulama
```

## Eskalasyon Tetikleyicileri

1. Süre **24 saatten az** kaldı → 🚨 acil müdahale
2. Süre **hak düşürücü** ve hesap belirsiz → kıdemli görüş
3. Adli tatil etkisi tartışmalı → manuel kontrol
4. Tebligat geçerliliği şüpheli → ayrı inceleme (Tebligat Kanunu)
5. Süre AYM/AİHM bağlamında → özel uzmanlık

## Notlar

- Bu skill bir araç; **kesin teyit avukatın sorumluluğundadır**.
- Yıllık güncelleme: resmî tatiller ve dini bayramlar her yıl değişir; profile şu komutla yıllık tatil listesi sorulmalı: `Bu yıl için resmî tatil ve dini bayram tarihleri nelerdir? mevzuat_mcp veya web search ile doğrula`.
- Adli tatil tarihleri HSK tarafından her yıl ilan edilir; mevzuat_mcp ile yıllık teyit.
