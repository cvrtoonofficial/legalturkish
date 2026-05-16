# Türk Hukuku için Claude — Legal Plugin (v0.4.0)

[![Version](https://img.shields.io/badge/version-0.4.0-blue)]() [![License](https://img.shields.io/badge/license-Apache--2.0-green)]() [![Skills](https://img.shields.io/badge/skills-22-purple)]() [![MCPs](https://img.shields.io/badge/MCPs-6-orange)]()

Türk hukuku için **odaklanmış** Claude plugin'i. Kullanıcı pratiğindeki spesifik dava türlerine optimize: müzik telif (FSEK), sanatçı sözleşmesi (Amuse/Spotify/Kobalt), sınır ötesi sözleşme fesih, trafik kazası, idari vergi.

## v0.4.0 Yenilikleri — Odaklanma

- ⭐ **`dava-strateji-analiz`** — Sherlock 5-adımlı yöntem (merkez skill)
- 📝 **`docx-uretici`** — Mahkemeye sunulabilir profesyonel Word çıktısı
- 🎵 Müzik özelinde: `meslek-birligi-yetki` + `sanatci-sozlesme-inceleme`
- 🌍 Sınır ötesi: `sinirostesi-sozlesme-fesih` (Amuse/İsveç senaryosu)
- 🚗 Trafik kazası: `trafik-kazasi-davasi` (KTK + sigorta tahkim)
- 💰 Vergi: `vergi-uyusmazligi-analiz` (VUK + İYUK + GİB özelgeleri)
- 📚 Akademik destek: `dergipark-doktrin-arastirma` (literatur + yoktez MCP)
- 🛡️ **`karsi-arguman-onleme`** — Hâkim/davalı argümanlarını öngörme
- ➕ 5 Türk MCP entegrasyonu (mevzuat, yargi, literatur, yoktez, markapatent)
- 🗑️ 13 kullanılmayan skill silindi (sade kalite > kapsamlı görüntü)

## Hızlı Kurulum

### MCP Bağlantıları (Claude Desktop)

Settings → Connectors → Add Custom Connector:
```
mevzuat-mcp      https://mevzuat.surucu.dev/mcp
yargi-mcp        https://yargimcp.surucu.dev/mcp
literatur-mcp    https://literatur-mcp.surucu.dev/mcp
yoktez-mcp       https://yoktezmcp.fastmcp.app/mcp
markapatent-mcp  https://markapatent-mcp.fastmcp.app/mcp
```

(MCP'ler Said Sürücü tarafından açık ve ücretsiz kullanıma sunulmuştur — kendi sunucunda da host edebilirsin.)

### Plugin Kurulum (Claude Code)

```
/plugin marketplace add https://github.com/cvrtoonofficial/legalturkish
/plugin install turk-hukuk-legal@turk-hukuk-legal-marketplace
```

### İlk çalıştırma — kritik

```
/turk-hukuk-legal:soguk-baslangic-mulakat
```

15-25 dakikalık mülakat sonunda büro profilin `~/.claude/plugins/config/turk-hukuk-legal/CLAUDE.md` dosyasına yazılır. Diğer tüm skill'ler bu profili okur.

## Skill Listesi (22)

### 🛠️ Kurulum & Yönetim (4)
- `soguk-baslangic-mulakat` — büro profili
- `matter-intake` — yeni dava alımı
- `chronology-builder` — olayların kronolojisi
- `siure-hesap-motoru` — HMK + İYUK süreleri

### ⚖️ Strateji Çekirdek (3)
- **`dava-strateji-analiz`** ⭐ — Sherlock 5-adım
- `karsi-arguman-onleme` — hâkim/davalı argümanlarını öngör
- `bilirkisi-soru-uretici` — HMK m.266-289

### 📜 Dilekçe & Yazışma (3)
- `dilekce-ihtarname` — HMK dilekçeleri + ihtarname
- `ihtarname-fsek-smk` — FSEK/SMK ihtarname
- `docx-uretici` — profesyonel Word çıktısı

### 🎵 Fikri Haklar & Müzik (6)
- `tecavuz-triyaj` — FSEK/SMK tecavüz YEŞİL/SARI/KIRMIZI
- `fikri-haklar-klozu-inceleme` — FSEK m.48-52
- `icerik-kaldirma-bildirim` — 5651 m.9 + platform
- `meslek-birligi-yetki` — MESAM/MSG/MÜYAP/SETEM/MÜZİKBİR
- `sanatci-sozlesme-inceleme` — Amuse, Spotify, Kobalt vb.
- `marka-tescil-on-arastirma` — TPMK (markapatent-mcp)

### 🌍 Sınır Ötesi (1)
- `sinirostesi-sozlesme-fesih` — Amuse/İsveç MÖHUK + TKHK

### 🚗 Trafik Kazası (1)
- `trafik-kazasi-davasi` — KTK + sigorta tahkim + maluliyet

### 💰 Vergi (1)
- `vergi-uyusmazligi-analiz` — VUK + İYUK + GİB

### 📚 Akademik Destek (1)
- `dergipark-doktrin-arastirma` — literatur + yoktez MCP

### 🏛️ Anayasal (1)
- `aym-bireysel-basvuru` — 6216 SK

### 📝 Sözleşme İnceleme (1)
- `sozlesme-inceleme` — TBK/TTK genel

## Sherlock Felsefesi

Bu plugin'in farkı: **AI sadece yazmaz — düşünür.**

1. **Dilekçe yazmadan önce sorar** — müvekkille mutlaka diyaloga geçer
2. **Lehe içtihatı tarar** — yargi_mcp ile bizim taraf lehine kararları çıkarır
3. **Karşı tarafın zayıflığını bulur** — TMK m.2 + usul hataları
4. **Eşleştirir** — bizim olgular ↔ lehe içtihat + karşı zayıflık
5. **Karşı argümanları öngörür** — hâkim ve davalının olası savunmalarına önceden cevap hazırlar
6. **Sherlock üslubuyla yazar** — soğuk, kanıtlı, çelişki gösterici

## MCP Entegrasyonu

| MCP | Görev | Plugin'de kullanım |
|---|---|---|
| **mevzuat_mcp** | Kanun, KHK, CBK, Yönetmelik, Tebliğ | Her skill Adım 0'da doğrulama |
| **yargi_mcp** | Yargıtay, Danıştay, AYM, BAM, KVKK, Rekabet, GİB, Sigorta Tahkim | İçtihat tarama (spesifik endpoint) |
| **literatur_mcp** | DergiPark akademik makaleler | Doktrin desteği (yeni alanlar) |
| **yoktez_mcp** | YÖK Ulusal Tez Merkezi | Monografik akademik destek |
| **markapatent_mcp** | TÜRKPATENT sicili | Marka/patent ön araştırma |
| **hukuk_rag** | Büro dosyaları | Vaka-spesifik referans |

## Mimari

```
legalturkish/
├── .claude-plugin/marketplace.json   # v0.4.0
├── turk-hukuk-legal/
│   ├── .claude-plugin/plugin.json    # v0.4.0
│   ├── .mcp.json                      # 6 MCP
│   ├── README.md
│   ├── LICENSE                        # Apache 2.0
│   ├── meta/
│   │   ├── CLAUDE-TEMPLATE.md         # büro profili
│   │   ├── MCP-PROTOCOL.md            # standart MCP protokolü
│   │   └── CHANGELOG.md
│   └── skills/                        # 22 SKILL.md
└── README.md
```

## Lisans

Apache 2.0. Üst proje ilham: [anthropics/claude-for-legal](https://github.com/anthropics/claude-for-legal). MCP'ler: [Said Sürücü](https://github.com/saidsurucu).

## Önemli

Plugin çıktıları **taslak** niteliğindedir. Mevzuat ve içtihat referansları her kullanımda 6 MCP üzerinden güncel metne göre doğrulanır.
