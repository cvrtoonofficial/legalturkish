# Türk Hukuku için Claude — Legal Plugin

Anthropic'in `knowledge-work-plugins/legal` plugin'inin Türk hukukuna yeniden yazılmış versiyonu.
TBK, TTK, HMK, KVKK, FSEK, SMK 6769, İYUK, İş K., TKHK eksenli.

## Kurulum

### Claude Code

```bash
# Bu repo'yu marketplace olarak ekle
/plugin marketplace add https://github.com/<KULLANICI>/<REPO>

# Plugin'i kur
/plugin install turk-hukuk-legal@turk-hukuk-legal-marketplace

# Claude Code'u yeniden başlat
```

### Cowork

1. Cowork → Customize → Browse plugins
2. Bu repo URL'sini gir veya `turk-hukuk-legal/` klasörünü zip'le ve yükle

## Skill Listesi

### Çekirdek hukuk (9)
- `sozlesme-inceleme` — TBK/TTK/TKHK eksenli madde madde inceleme
- `gizlilik-sozlesmesi-triyaj` — YEŞİL/SARI/KIRMIZI NDA triyajı
- `uyum-kontrol` — KVKK + sektörel uyum
- `hukuki-yazisma` — KVKK başvuru yanıtı, ihtarname yanıtı, KEP
- `risk-degerlendirme` — Önem × olasılık matrisi
- `toplanti-brifingi` — Müzakere, duruşma, YK, kurum görüşmesi
- `tedarikci-kontrol` — Sözleşme envanteri, eksik belge, yenileme
- `brifing` — Günlük / konu / olay brifingi
- `imza-akisi` — KEP, e-imza, ıslak, noter karar matrisi

### Fikri ve sınai haklar (9)
- `marka-tescil-on-arastirma` — SMK m.5-6 knockout
- `ihtarname-fsek-smk` — FSEK + SMK ihtarnamesi
- `icerik-kaldirma-bildirim` — 5651 m.9 + platform
- `tecavuz-triyaj` — YEŞİL/SARI/KIRMIZI
- `fikri-haklar-klozu-inceleme` — FSEK m.48-52
- `patent-serbestlik-analizi` — SMK FTO
- `acik-kaynak-uyum` — OSS lisans + FSEK
- `portfoy-takip` — TPMK yenileme
- `dilekce-ihtarname` — HMK dilekçeleri + TBK ihtarnameleri

## MCP Bağımlılıkları

- `mevzuat_mcp` — Türk mevzuatı
- `yargi_mcp` — Yargı kararları
- `hukuk-rag` — Büro dosyaları (opsiyonel)

## Lisans

Apache 2.0. Üst proje: [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins) — Apache 2.0, Anthropic.

## Önemli

Plugin çıktıları taslaktır. Mevzuat ve içtihat referansları her kullanımda `mevzuat_mcp` ve `yargi_mcp` üzerinden güncel metne göre doğrulanmalıdır.
