---
name: tecavuz-triyaj
description: Marka, patent, faydalı model, tasarım, coğrafi işaret (SMK 6769) ve telif (FSEK 5846) tecavüzü iddiasını triyaj eder. YEŞİL (eylem önerilir), SARI (uzman görüş alın), KIRMIZI (karmaşık, kıdemli vekil/uzman avukat zorunlu) olarak sınıflandırır. **Hukuki sonuç değil; eylem önerisi.**
version: 0.2.0
last_legal_review: 2026-05-16
required_mcps:
  - mevzuat_mcp
  - yargi_mcp
optional_mcps:
  - hukuk-rag
applicable_laws:
  - 5846
  - 6769
---

# /fikri-sinai-haklar:tecavuz-triyaj — Tecavüz Triyajı

## Davet



---

## Adım 0 — Zorunlu MCP Çağrıları

> Bu bölüm `meta/MCP-PROTOCOL.md` çerçevesini uygular. Skill çıktısı **bu çağrılar tamamlanmadan** üretilmez.

### 0.1 Profil okuma
- Dosya: `~/.claude/plugins/config/turk-hukuk-legal/CLAUDE.md`
- Yoksa → kullanıcıya `/turk-hukuk-legal:soguk-baslangic-mulakat` çalıştırması önerilir; bu skill yine generic modda çalışır ama çıktı başında **⚠️ Profil yok** uyarısı eklenir.

### 0.2 Mevzuat çekme (`mevzuat_mcp`)
Bu skill için temel kanun numaraları:

- **Kanun 5846** — anahtar kelimeler: "tecavüz", "bağımsız geliştirme", "mali hak"
- **Kanun 6769** — anahtar kelimeler: "marka tecavüz", "patent tecavüz", "tasarım tecavüz"

Her madde için: `mevzuat_mcp.search_within_kanun(mevzuat_no="<NO>", keyword="<KAVRAM>")`

Çağrı timeout / boş sonuç verirse: çıktıya `⚠️ MCP_TIMEOUT` etiketi ekle, madde numarasını **doğrulanacak** olarak işaretle.

### 0.3 İçtihat tarama (`yargi_mcp`)
Önerilen endpoint(ler):

- `yargi_mcp.search_bedesten_unified(...)`

Profilde tanımlı **yetkili daire** tercihi varsa sorguya dahil et (örn. "Yargıtay 11. HD" — daire yapısı `yargi_mcp.search` ile teyit edilmelidir).

### 0.4 Büro dosyası tarama (`hukuk-rag`, opsiyonel)
Eğer ilgili müvekkil dosyası varsa:
```
mcp__hukuk-rag__hukuk_rag_ara(
  sorgu="<konuya özgü>",
  dava="<profile.default_collection>",
  top_k=6
)
```

### 0.5 Çağrı çıktıları → Output ekleri
Tüm MCP yanıtları **Output / Ekler** bölümünde:
- **A. Doğrulanmış Mevzuat:** her madde için `[mevzuat_mcp:NNN:m.X]` izli atıf
- **B. İçtihat Referansları:** `[yargi_mcp:DAİRE:ESAS/KARAR]`
- **C. Büro Dosya Referansları:** `[hukuk-rag:KOLEKSİYON:chunk_id]`
- **D. MCP Çağrı Logu:** audit trail (hangi çağrı, ne sonuç verdi)

---
```
/fikri-sinai-haklar:tecavuz-triyaj
```

Tecavüz iddiasının türünü ve mevcut delilleri sorar.

## Triyaj Mantığı

### YEŞİL — Standart Eylem (örn. ihtarname taslağı, içerik kaldırma)
Şu kümülatif şartlar varsa:
- Tescilli ve geçerli hak (TPMK tescili güncel veya FSEK eseri açık)
- Birebir / yüksek derecede benzer ihlal (görsel + sescil + kavramsal)
- Net delil (ekran görüntüsü, satın alma, noter tespiti)
- Aynı / yakın sınıf veya pazar
- Karşı taraf tescilli karşı hak iddia etmiyor

→ `/fikri-sinai-haklar:ihtarname-fsek-smk` veya `/fikri-sinai-haklar:icerik-kaldirma-bildirim` ile devam.

### SARI — Uzman Görüş Şart
- Tanınmış marka iddiası (SMK m.6/4, m.6/5)
- Önceye dayalı kullanım çakışması (m.6/3)
- Kötü niyet iddiası (m.6/9, m.25/1-c)
- Eser sahipliği uyuşmazlığı (FSEK m.8, 10, 11)
- İşlenme eseri (FSEK m.6) — özgünlük ve katkı oranı tartışmalı
- FSEK m.68 üç kat tazminat hesabında rayiç bedel tartışması
- Bağlantılı haklar (FSEK m.80) — yapımcı/icracı/yayın çakışması
- Meslek birliği yetki alanı (MESAM, MSG, MÜZİKBİR, vb. — FSEK m.42)
- Yazılım reverse engineering iddiası

→ Vekille toplantı + uzmanlık görüşü; muhtemel HMK m.400 delil tespiti.

### KIRMIZI — Karmaşık, Kıdemli Vekil Zorunlu
- Hükümsüzlük + tecavüz paralel ihtilaf (karşı dava riski)
- Patent FTO / zorunlu lisans (SMK m.129-137)
- Sınır ötesi tecavüz (uluslararası özel hukuk + WIPO, Paris Sözleşmesi)
- Ceza boyutu açık (FSEK m.71-72, TCK m.158/h, m.244 bilişim suçları)
- Kamu kurumu / üniversite / yayıncı muhatap
- Kolektif eser sahipliği (FSEK m.10) veya birden fazla devir zinciri
- Mahkeme aşamasında çelişik bilirkişi raporları
- Acil ihtiyati tedbir gerekliliği (HMK m.389+; SMK m.159; FSEK m.77)
- Açık kaynak lisans ihlali iddiası — copyleft etkisi

→ Kıdemli FSEK/SMK uzmanı + gerekirse patent vekili / marka vekili müşterek çalışma.

## İş Akışı

### Adım 1 — Hak Sahipliği Doğrula
- TPMK tescil belgesi (marka/patent/tasarım) güncel mi?
- Koruma süresi devam ediyor mu? (Marka: 10 yıl, yenilenebilir; Patent: 20 yıl; Faydalı model: 10 yıl; Tasarım: 5 yıl, 4 kez yenilenebilir — `mevzuat_mcp` ile teyit)
- FSEK eseri ise: yaratım tarihi, ilk yayım, devir zinciri belgeleri
- Lisans alan mı, devralan mı, asıl hak sahibi mi?

### Adım 2 — Tecavüz Eylemini Tanımla
| SMK alanı | Tecavüz halleri (SMK m.29/85/81 vb. — doğrulanacak) |
|---|---|
| Marka | İşareti aynısının/aynısının haricinde benzer şekilde ticarette kullanmak; ürün üretim, satış, ithalat, ihracat |
| Patent | İstemde tanımlı buluşun ticari kullanımı |
| Tasarım | Tasarımın bilgili kullanıcı üzerinde aynı genel izlenimi bırakması |
| Coğrafi işaret | Korumalı işareti şartlara aykırı kullanım |

FSEK tecavüz halleri (FSEK m.66, m.67 ve eserin türüne göre m.21-25 mali haklara müdahale).

### Adım 3 — Delilin Kalitesi
- ✅ Noter tespiti / HMK m.400 delil tespiti
- 🟡 Ekran görüntüsü + arşiv linki
- 🟡 Satın alma + fatura
- 🔴 Sadece dolaylı duyum

Delil kalitesi mahkeme aşamasında **HMK m.198+ delil değerlendirme** sürecinde belirleyicidir.

### Adım 4 — Karşı Tarafın Hak Pozisyonu
- Kendi tescili var mı?
- Önceye dayalı kullanım iddiası var mı (m.6/3)?
- Lisans / sözleşme iddiası var mı?
- Tüketici kafa karışıklığı mı yoksa parodi/eleştiri (FSEK m.31 vd. — sınırlamalar) mı?

### Adım 5 — Yargı Sürecinin Tahmini
- Yetkili mahkeme: **Fikri ve sınai haklar hukuk mahkemesi** (sınırlı sayıda ilde). Bulunmayan illerde **Asliye Hukuk Mahkemesi sıfatıyla bakan ihtisas mahkemesi** (HSK kararıyla).
- Süre: İhtiyati tedbir hızlı (saatler-günler); esas dava 1-3 yıl, BAM + Yargıtay temyiziyle 3-7 yıl.
- Maliyet: Yargı harcı + bilirkişi + vekâlet ücreti
- İhtilafın boyutu uluslararası ise WIPO Madrid / EUIPO paralel süreçleri

### Adım 6 — Triyaj Skoru Hesapla

```python
puanlama = {
    "hak_sahipligi_net": +2,
    "ihlal_net": +2,
    "delil_kuvvetli": +2,
    "karsi_iddia_zayıf": +1,
    "uluslararasi_boyut": -1,
    "hukumsuzluk_riski": -2,
    "ceza_boyutu": -1,
    "tanınmıs_marka_iddiasi": -1,
}
```

| Puan | Renk |
|---|---|
| ≥6 | 🟢 YEŞİL |
| 3-5 | 🟡 SARI |
| ≤2 | 🔴 KIRMIZI |

### Adım 7 — Çıktı

```markdown
## Tecavüz Triyaj Raporu

**Hak türü:** [Marka / Patent / FM / Tasarım / Coğrafi işaret / FSEK]
**Tescil no:** [...]
**Tecavüz iddiası:** [Özet]
**Delil paketi:** [Liste]

---

### Sınıflandırma: [🟢 / 🟡 / 🔴]

### Gerekçe
- ...

### Önerilen sonraki adım
- [🟢 → ihtarname-fsek-smk]
- [🟡 → vekil toplantısı + uzman görüş]
- [🔴 → kıdemli FSEK/SMK uzmanı + paralel hükümsüzlük tarama]

### Süre disiplini
- İhtiyati tedbir için makul süre (gecikme = haktan vazgeçme yorumu)
- Hak düşürücü süreler [`mevzuat_mcp` ile doğrula]

### Mevzuat & İçtihat referansları
- [yargi_mcp sonuçları]
```

## Disclaimer

Triyaj **eylem önerisi**dir, hukuki sonuç değildir. Her vaka kendi içinde değerlendirilir.


---

## Standart Çıktı Formatı (Hukuki Memo)

Skill nihai çıktısı **`meta/MCP-PROTOCOL.md` §Çıktı Formatı Standartı** şablonunu izler:

```markdown
# [SKILL] — [Konu]

**Tarih:** {tarih}
**Profil:** {büro}, {ton}
**Skill versiyonu:** {version}

## I. Olgular
## II. Hukuki Çerçeve
## III. Analiz
## IV. Sonuç ve Öneri
## V. Riskler ve Eskalasyon

## Ekler
### A. Doğrulanmış Mevzuat
### B. İçtihat Referansları
### C. Büro Dosya Referansları
### D. MCP Çağrı Logu
### E. Eskalasyon Kontrolü
### F. Versiyon & Doğrulama
```

## Eskalasyon Tetikleyicileri (otomatik kontrol)

Skill çıktısı üretilirken şu durumlardan biri tespit edilirse **operasyonel çıktı durdurulur**, yerine eskalasyon raporu üretilir:

1. Cezai sorumluluk olasılığı (TCK kapsamı)
2. KVKK m.6 özel nitelikli veri
3. Düzenleyici kurum soruşturması (BDDK, KVKK, Rekabet)
4. AYM / AİHM yolu açık
5. Sınır ötesi taraf (MÖHUK)
6. Kamu kurumu / yayıncı muhatap
7. Acil ihtiyati tedbir gerekliliği
8. Medya / itibari risk

