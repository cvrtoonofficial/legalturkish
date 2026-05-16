# Türk Hukuku Legal Plugin

**Versiyon:** 0.2.0
**Yayın:** 16 Mayıs 2026
**Lisans:** Apache 2.0

Anthropic'in `knowledge-work-plugins/legal` plugin'inin Türk hukukuna **yeniden yazılmış** versiyonu. Üzerine **fikri ve sınai haklar paketi** eklenmiştir.

## v0.2.0 Yenilikleri (Sprint 1)

- ✨ **`soguk-baslangic-mulakat`** — kurulum mülakatı + büro profili sistemi
- 📋 **`CLAUDE.md` profil** — tüm skill'lerin okuduğu büro kılavuzu
- 🔌 **Zorunlu MCP Çağrıları** — her skill mevzuat_mcp + yargi_mcp ile çalışma anında doğrulama yapar
- 📄 **Standart Hukuki Memo formatı** — yapılandırılmış, izlenebilir çıktı
- 🚨 **Eskalasyon tetikleyicileri** — cezai sorumluluk, KVKK m.6, AYM/AİHM, sınır ötesi durumlar için otomatik kontrol
- 📦 19 skill (önceki 18 + soğuk başlangıç)

## Skill Listesi

### Kurulum
- `soguk-baslangic-mulakat` — Önce bunu çalıştır

### Çekirdek hukuk
| Skill | Konu | Temel kanunlar |
|---|---|---|
| `sozlesme-inceleme` | Madde madde sözleşme inceleme | TBK 6098, TTK 6102, TKHK 6502, FSEK, KVKK |
| `gizlilik-sozlesmesi-triyaj` | NDA Yeşil/Sarı/Kırmızı | TBK 6098, TTK 6102, 6325 |
| `uyum-kontrol` | KVKK + sektörel | KVKK 6698, TKHK, 4054, 5651 |
| `hukuki-yazisma` | KVKK başvuru yanıtı, ihtarname yanıt, KEP | KVKK, TBK, TTK, CMK |
| `risk-degerlendirme` | Önem × olasılık matrisi | HMK, TCK, FSEK/SMK |
| `toplanti-brifingi` | Müzakere, duruşma, YK | HMK, TTK |
| `tedarikci-kontrol` | Sözleşme envanteri | TBK, TTK, KVKK |
| `brifing` | Günlük / konu / olay brifingi | — |
| `imza-akisi` | KEP, e-imza, ıslak, noter | TBK, TTK, 5070, TMK, 488 |

### Fikri ve sınai haklar
| Skill | Konu | Temel kanunlar |
|---|---|---|
| `marka-tescil-on-arastirma` | SMK m.5-6 knockout | SMK 6769 |
| `ihtarname-fsek-smk` | FSEK + SMK ihtarnamesi | FSEK 5846, SMK 6769, TBK |
| `icerik-kaldirma-bildirim` | 5651 m.9 + platform | 5651, FSEK |
| `tecavuz-triyaj` | YEŞİL/SARI/KIRMIZI sınıflandırma | FSEK, SMK |
| `fikri-haklar-klozu-inceleme` | FSEK m.48-52 | FSEK, SMK, TBK |
| `patent-serbestlik-analizi` | FTO triyajı | SMK 6769 |
| `acik-kaynak-uyum` | OSS lisans + FSEK | FSEK |
| `portfoy-takip` | TPMK yenileme | SMK |
| `dilekce-ihtarname` | HMK dilekçeleri + TBK ihtarnameler | HMK, TBK, İş K., FSEK/SMK |

## MCP Bağımlılıkları

```json
{
  "mevzuat_mcp": "Türk mevzuatı veritabanı",
  "yargi_mcp": "Yargı kararları (Yargıtay, Danıştay, AYM, BAM, KVKK, Rekabet, vb.)",
  "hukuk-rag": "Büro dosyaları üzerinde semantik arama (opsiyonel)"
}
```

## Mimari

```
turk-hukuk-legal/
├── .claude-plugin/plugin.json
├── .mcp.json
├── README.md (bu dosya)
├── LICENSE (Apache 2.0)
├── meta/
│   ├── CLAUDE-TEMPLATE.md
│   ├── MCP-PROTOCOL.md
│   └── CHANGELOG.md
└── skills/  (19 SKILL.md)
```

## Önemli

Çıktılar taslak niteliğindedir. Mevzuat ve içtihat referansları her kullanımda doğrulanmalıdır.
