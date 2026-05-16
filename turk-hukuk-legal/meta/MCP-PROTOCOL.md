# MCP Protokolü — Her Skill İçin Standart

Bu belge, plugin içindeki **tüm skill'lerin** MCP araçlarını nasıl kullanması gerektiğini standartlaştırır. Her SKILL.md başında yer alan **"Zorunlu MCP Çağrıları"** bloğu bu protokolü uygular.

## Amaç

1. **Doğruluk:** Mevzuat ve içtihat referansları training data değil, **çalışma anında MCP'den** çekilsin.
2. **İzlenebilirlik:** Her atıfın hangi MCP çağrısından geldiği takip edilebilir olsun.
3. **Tutarlılık:** Tüm skill'ler aynı tarama disiplini uygulasın.

## Standart MCP Çağrı Bloğu

Her skill'in **Adım 0**'ı (workflow'dan önce) bu bloğu çalıştırır:

```markdown
## Adım 0 — Zorunlu MCP Çağrıları

Skill çıktısı üretilmeden önce şu çağrılar yapılır:

### 0.1 Profil okuma
- Dosya: `~/.claude/plugins/config/turk-hukuk-legal/CLAUDE.md`
- Eğer profil eksikse, `/turk-hukuk-legal:soguk-baslangic-mulakat` çalıştırılması önerilir.

### 0.2 Mevzuat çekme (`mevzuat_mcp`)
Skill'in dayandığı her kanun maddesi için:
```
mevzuat_mcp.search_within_kanun(
  mevzuat_no="<KANUN_NO>",
  keyword="<ARANAN_KAVRAM>"
)
```

| Bu skill'in temel kanun no'ları | Aranacak anahtar kelimeler |
|---|---|
| (skill-specific listede tanımlı) | (skill-specific) |

Timeout veya hata durumunda: çıktıya **⚠️ MCP doğrulaması başarısız** etiketi ekle ve mevzuat numaralarını "doğrulanacak" olarak işaretle.

### 0.3 İçtihat tarama (`yargi_mcp`)
Spesifik endpoint seçimi:
- Yargıtay + BAM: `yargi_mcp.search_bedesten_unified(...)`
- AYM bireysel başvuru: `yargi_mcp.search_anayasa_unified(...)`
- KVKK Kurulu: `yargi_mcp.search_kvkk_decisions(...)`
- Rekabet Kurumu: `yargi_mcp.search_rekabet_kurumu_decisions(...)`
- BDDK: `yargi_mcp.search_bddk_decisions(...)`
- Emsal (BAM detaylı): `yargi_mcp.search_emsal_detailed_decisions(...)`
- Sayıştay: `yargi_mcp.search_sayistay_unified(...)`
- Uyuşmazlık Mahkemesi: `yargi_mcp.search_uyusmazlik_decisions(...)`
- Kamu İhale Kurulu: `yargi_mcp.search_kik_v2_decisions(...)`

### 0.4 Büro dosyası tarama (`hukuk-rag`, varsa)
Eğer ilgili müvekkil dosyası varsa:
```
mcp__hukuk-rag__hukuk_rag_ara(
  sorgu="<konu>",
  dava="<koleksiyon_adı>",
  top_k=8
)
```

Profilden default koleksiyon okunur; yoksa kullanıcıya hangi koleksiyon kullanılacağı sorulur.

### 0.5 Sonuç paketi
Her çağrının çıktısı **çıktı bölümünde** "Doğrulanmış Kaynak" olarak listelenir:
- Mevzuat: `[mevzuat_mcp:kanun#NNN:m.X — tarih]`
- İçtihat: `[yargi_mcp:DAİRE:ESAS/KARAR]`
- Büro dosya: `[hukuk-rag:KOLEKSİYON:CHUNK_ID]`
```

## Çıktı Formatı Standartı — Hukuki Memo

Tüm skill çıktıları aşağıdaki **Hukuki Memo** formatını izler:

```markdown
# [SKILL ADI] — [Konu Özeti]

**Tarih:** {tarih}
**Hazırlayan:** turk-hukuk-legal v{version}
**Profil:** {büro_adı}, {uzmanlık}, {ton}
**Müvekkil / Dosya:** {anonim ya da kullanıcı tarafından girilen}
**Skill versiyonu:** {skill_version}

---

## I. Olgular
[Sunulan bilginin yapılandırılmış özeti. Kronolojik veya konuya göre.]

## II. Hukuki Çerçeve
[İlgili mevzuat — her madde `mevzuat_mcp` ile doğrulandı]

| Mevzuat | Madde | Konu | Kaynak |
|---|---|---|---|
| 5846 FSEK | m.52 | Mali hakların ayrı sayımı | mevzuat_mcp:5846:m52 |

## III. Analiz
[Vakıaların hukuki çerçevede değerlendirilmesi]

## IV. Sonuç ve Öneri
[Spesifik aksiyon önerisi]

## V. Riskler ve Eskalasyon
- {risk seviyesi} — {gerekçe}
- Eskalasyon tavsiyesi: {kıdemli görüş / dış uzman / yönetim toplantısı / yok}

---

## Ekler

### A. Doğrulanmış Mevzuat Kaynakları
- [mevzuat_mcp:NNN:m.X] {tam atıf}

### B. İçtihat Referansları
- [yargi_mcp:DAİRE:ESAS/KARAR] {tarih, kısa özet}

### C. Büro Dosya Referansları (hukuk-rag)
- [hukuk-rag:KOLEKSİYON:chunk_id] {kısa özet}

### D. MCP Çağrı Logu (audit trail)
| Çağrı | Sonuç | Zaman |
|---|---|---|
| mevzuat_mcp.search_within_kanun(...) | ✓ {n sonuç} | {time} |
| yargi_mcp.search_bedesten_unified(...) | ✓ {n sonuç} | {time} |

### E. Eskalasyon Kontrolü
- [ ] Cezai sorumluluk işareti
- [ ] Hassas veri (KVKK m.6 özel nitelikli)
- [ ] Kamu kurumu muhatap
- [ ] AYM/AİHM boyutu
- [ ] Sınırötesi boyut (MÖHUK)
- [ ] Medya/itibari risk

### F. Versiyon & Doğrulama
- Skill versiyonu: {x.y.z}
- Bu çıktı için MCP doğrulaması yapıldı: ✓ / ⚠️ (kısmen) / ❌ (yapılamadı)
- Mevzuat son inceleme tarihi: {tarih}
```

## Eskalasyon Tetikleyicileri (Tüm skill'ler için ortak)

Aşağıdaki durumlar her skill'in **otomatik** eskalasyon işareti üretmesini gerektirir:

1. **Cezai sorumluluk olasılığı** (TCK kapsamı, FSEK m.71-72, vb.)
2. **KVKK m.6 özel nitelikli veri** (sağlık, biyometrik, çocuk, vb.)
3. **Düzenleyici kurum soruşturması açık** (BDDK, KVKK, Rekabet)
4. **AYM bireysel başvuru ya da AİHM yolu**
5. **Sınır ötesi taraflar** (MÖHUK uygulanır)
6. **Karşı taraf kamu kurumu / üniversite / yayıncı**
7. **Acil ihtiyati tedbir** (HMK m.389 ya da FSEK m.77, SMK m.159)
8. **Medya ilgisi** (potansiyel itibari/finansal risk)
9. **Anayasa şikâyeti içeren mevzuat itirazı**

Eskalasyon işaretlenirse skill **operasyonel çıktı** üretmeyi durdurabilir; yerine **uyarı + danışman önerisi** üretir.

## MCP Hata Davranışı

| Durum | Davranış |
|---|---|
| MCP timeout | Çıktıya `⚠️ MCP_TIMEOUT` etiketi ekle; ilgili referansları "doğrulanacak" olarak işaretle |
| MCP bağlı değil | Profil okumasında "MCP bağlı değil" uyarısı; skill yine çalışır ama belirgin disclaimer eklenir |
| MCP boş sonuç döndü | Çıktıya "İlgili içtihat bulunamadı (yargi_mcp boş)" notu ekle |
| MCP yanlış cevap (paradoks) | Çıktıya çelişki notu + manuel doğrulama önerisi |

## Versiyon Takibi

Her SKILL.md frontmatter'ı şu alanları içerir (v0.2.0+):

```yaml
---
name: <skill-adı>
description: <açıklama>
version: 0.2.0
last_legal_review: 2026-05-16
required_mcps:
  - mevzuat_mcp
  - yargi_mcp
optional_mcps:
  - hukuk-rag
applicable_laws:
  - 5846  # FSEK
  - 6098  # TBK
---
```
