---
name: acik-kaynak-uyum
description: Yazılım projelerinde kullanılan açık kaynak (OSS) bileşenlerini FSEK (5846) m.52 yazılı şekil şartı, bileşenlerin lisans türü (permissive / weak copyleft / strong copyleft / network copyleft) ve dağıtım modelinize göre uyumluluk açısından inceler. AGPL, GPL, LGPL, MPL, MIT, Apache, BSD ailelerini Türk hukukuyla birlikte değerlendirir.
---

# /fikri-sinai-haklar:acik-kaynak-uyum — Açık Kaynak Lisans Uyumu

## Lisans Tipi Çerçevesi

| Tip | Örnek | Tetikleyici | Etki |
|---|---|---|---|
| **Permissive** | MIT, Apache 2.0, BSD-3 | Atıf | Düşük; ticari kullanımda sorun yok |
| **Weak copyleft** | LGPL, MPL 2.0 | Modifikasyon | Modifiye edilen dosya açılır; statik link sorunlu |
| **Strong copyleft** | GPL-2.0, GPL-3.0 | Dağıtım | Türev eser dağıtılırsa tüm kod GPL altında olmalı |
| **Network copyleft** | AGPL-3.0 | Network'ten erişim de "dağıtım" sayılır | SaaS modelinde tetikler |

## Türk Hukukuyla Etkileşim

- **FSEK m.2/1** — Bilgisayar programları **eser** olarak korunur
- **FSEK m.52** — Mali hak devri yazılı şekil + ayrı ayrı sayma. OSS lisansları **lisans** niteliğindedir; yazılı şekil tartışmasında dijital lisans metni de yazılı kabul edilir (yerleşik içtihat — `yargi_mcp` ile doğrulanabilir).
- **FSEK m.38** — Kişisel kullanım istisnası; ticari yazılım dağıtımı kapsam dışı.
- **TBK m.27** — Kanuna aykırı sözleşme şartları batıldır. Bazı GPL şartları (örn. yetki feragati üst sınırı) TBK ile çelişebilir; sözleşme bütününün geçersizliği genelde aranır.

## İş Akışı

1. Yazılım Bill of Materials (SBOM) topla
2. Her bileşenin lisansını tespit (SPDX-License-Identifier)
3. Dağıtım modeline göre tetikleyicileri kontrol et:
   - On-premise dağıtım → GPL tetikler
   - SaaS (sadece network) → AGPL tetikler, GPL tetiklemez
   - Mobil uygulama → store dağıtımı dağıtım sayılır
4. Lisans uyumluluk matrisi çıkar (örn. Apache 2.0 + GPL-2.0 only çatışması)
5. Atıf yükümlülükleri listesi (NOTICE dosyası, third-party-licenses metni)
6. Patent retaliation şartlarına dikkat (Apache 2.0 §3, GPL-3.0 §11)

## Çıktı

```markdown
## OSS Uyum Raporu

### Bileşen envanteri
| Bileşen | Versiyon | Lisans | Tip |
|---|---|---|---|

### Tetikleyici tespiti
- [Bileşen X — GPL-3.0; dağıtım modeli on-premise → tetikleyici aktif]

### Uyumsuzluk uyarıları
- [Apache 2.0 + GPL-2.0 only çatışma]

### Atıf yükümlülükleri
- [NOTICE dosyasına eklenecek bileşenler]

### Türk hukuku notları
- FSEK m.2 ve m.52 — OSS lisansı yazılı lisans kabulü için içtihat referansı

### Önerilen aksiyon
- ...
```
