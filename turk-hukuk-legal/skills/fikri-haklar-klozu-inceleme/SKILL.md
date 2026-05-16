---
name: fikri-haklar-klozu-inceleme
description: Sözleşmelerdeki fikri haklar (telif & sınai mülkiyet) klozlarını FSEK m.48-52 (telif devir & lisans şekil şartları), SMK m.148 (sınai hak devri) ve TBK genel hükümlere göre inceler. Yazılı şekil, mali hakların ayrı ayrı sayımı, ileride doğacak haklar sınırı, manevi hakların devredilemezliği gibi kritik noktaları kontrol eder.
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
  - 6098
---

# /fikri-sinai-haklar:fikri-haklar-klozu-inceleme — Fikri Haklar Klozu İnceleme

## Kritik Şartlar Kontrol Listesi



---

## Adım 0 — Zorunlu MCP Çağrıları

> Bu bölüm `meta/MCP-PROTOCOL.md` çerçevesini uygular. Skill çıktısı **bu çağrılar tamamlanmadan** üretilmez.

### 0.1 Profil okuma
- Dosya: `~/.claude/plugins/config/turk-hukuk-legal/CLAUDE.md`
- Yoksa → kullanıcıya `/turk-hukuk-legal:soguk-baslangic-mulakat` çalıştırması önerilir; bu skill yine generic modda çalışır ama çıktı başında **⚠️ Profil yok** uyarısı eklenir.

### 0.2 Mevzuat çekme (`mevzuat_mcp`)
Bu skill için temel kanun numaraları:

- **Kanun 5846** — anahtar kelimeler: "mali hak devri", "yazılı şekil", "manevi hak"
- **Kanun 6769** — anahtar kelimeler: "lisans", "devir", "sicil"
- **Kanun 6098**

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

