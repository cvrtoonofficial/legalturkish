# CHANGELOG

## [0.4.0] — 2026-05-16 — Sprint 3: Odaklı Plugin (Müzik/Trafik/Vergi/Amuse)

### Ana değişiklik: Plugin odaklandı

Kullanıcının pratiğine uygunluk için **13 skill silindi**, **9 yeni skill eklendi**. Plugin artık spesifik dava türlerine (müzik telif/FSEK, sanatçı sözleşmesi, sınır ötesi fesih, trafik kazası, idari vergi) yoğunlaşır.

### Eklenen — Yeni Skill'ler (9)

- **`dava-strateji-analiz`** ⭐ — Sherlock 5-adımlı yöntem (Adım 1A müvekkille diyalog → lehe içtihat tarama → karşı zayıflık analizi → eşleştirme → karşı argüman öngörme → güçlü yazım)
- **`docx-uretici`** — Profesyonel Word çıktısı (Times New Roman 12pt, UYAP standardına yakın)
- **`meslek-birligi-yetki`** — MESAM/MSG/MÜYAP/SETEM/MÜZİKBİR yetki haritası (FSEK m.42 vd.)
- **`sanatci-sozlesme-inceleme`** — Amuse, Spotify, Epidemic Sound, Kobalt, AWAL dijital dağıtım/sync/yapımcı sözleşmesi
- **`sinirostesi-sozlesme-fesih`** — Yabancı yetki klozlu sözleşmelerin Türk mahkemesinde feshi (MÖHUK m.26 + TKHK + AİHS m.6)
- **`trafik-kazasi-davasi`** — KTK 2918 + TBK m.49+ + Sigorta Tahkim Komisyonu + maluliyet hesabı
- **`vergi-uyusmazligi-analiz`** — VUK + İYUK + GİB özelgeleri + Danıştay 3/4/9. Daire
- **`dergipark-doktrin-arastirma`** — literatur-mcp + yoktez-mcp ile akademik destek
- **`karsi-arguman-onleme`** — Hâkim/davalının olası argümanlarını önceden öngörme

### MCP entegrasyon genişletildi

`.mcp.json` artık **6 MCP** içeriyor (önceki 3'ten):
- mevzuat_mcp (https://mevzuat.surucu.dev/mcp)
- yargi_mcp (https://yargimcp.surucu.dev/mcp)
- **literatur_mcp** (https://literatur-mcp.surucu.dev/mcp) — yeni
- **yoktez_mcp** (https://yoktezmcp.fastmcp.app/mcp) — yeni
- **markapatent_mcp** (https://markapatent-mcp.fastmcp.app/mcp) — yeni
- hukuk_rag (lokal)

### CLAUDE-TEMPLATE.md güncellendi

- Müzik / sanatçı kimliği alanları (meslek birliği üyeliği, mahlas, TPMK vekil sicili)
- Maruz olunan dava türleri (FSEK, Amuse, trafik, vergi, AYM)
- Sherlock üslubu detayları
- 6 MCP'nin kullanım haritası
- Yargıtay/Danıştay daire tercihleri (4. ve 17. HD trafik, 11. HD FSEK, 13. HD tüketici, vb.)

### Silinen — 13 skill (kullanıcı pratiğinde yok)

- gizlilik-sozlesmesi-triyaj
- uyum-kontrol
- hukuki-yazisma
- risk-degerlendirme
- toplanti-brifingi
- tedarikci-kontrol
- brifing
- imza-akisi
- acik-kaynak-uyum
- portfoy-takip
- patent-serbestlik-analizi
- dsar-responder
- pia-generator

### Korunan + güçlendirilecek (13 skill)

- soguk-baslangic-mulakat (büro profili)
- matter-intake (yeni dava alımı)
- chronology-builder (kronoloji)
- siure-hesap-motoru (süre hesabı)
- dilekce-ihtarname (HMK uyumlu — Sherlock toniyle güncellenecek)
- ihtarname-fsek-smk (FSEK/SMK ihtarname)
- tecavuz-triyaj (FSEK tecavüzü triyajı)
- fikri-haklar-klozu-inceleme (FSEK m.48-52)
- icerik-kaldirma-bildirim (5651 m.9)
- sozlesme-inceleme (TBK/TTK eksenli)
- marka-tescil-on-arastirma (TPMK — markapatent-mcp entegre)
- bilirkisi-soru-uretici (HMK m.266-289)
- aym-bireysel-basvuru (6216 SK)

### Yeni felsefe / disiplin

- **"AI yazmadan önce sorar"** disiplini — her skill müvekkille diyalogla başlar
- **Sherlock yöntemi** — soğuk, kanıtlı, çelişki gösterici üslup
- **Karşı argüman öngörme** — yazmadan önce karşı tarafın muhtemel cevaplarını çürüt
- **5 MCP eş zamanlı** — mevzuat + içtihat + doktrin + tez + sicil

## [0.3.0] — Sprint 2 (atlanmış — v0.4.0'a katıldı)

- matter-intake, chronology-builder, siure-hesap-motoru, bilirkisi-soru-uretici, aym-bireysel-basvuru, dsar-responder (sonra silindi), pia-generator (sonra silindi)

## [0.2.0] — 2026-05-16 — Sprint 1: Profil Sistemi + MCP Protokolü

- soguk-baslangic-mulakat, CLAUDE-TEMPLATE.md, MCP-PROTOCOL.md, CHANGELOG.md
- Tüm skill'lere "Adım 0 — Zorunlu MCP Çağrıları" + "Standart Çıktı Formatı" blokları
- Frontmatter zenginleştirme (version, last_legal_review, required_mcps, applicable_laws)

## [0.1.0] — 2026-05-15 — İlk Yayın

- 18 skill, mevzuat_mcp + yargi_mcp + hukuk-rag entegrasyonu

---

## Yol Haritası

### v0.5.0 (Sprint 4) — Adaptasyon ve İyileştirme
- Mevcut 13 skill'i v0.4.0 standartlarına yükselt (Adım 1A müvekkille diyalog, Sherlock üslubu)
- UYAP yardımcı (şablon rehber — riskli olmayan tarafta)
- KEP bildirim hazırlık (TTK m.18/3)

### v0.6.0 (uzun vade)
- Scheduled agents: Resmî Gazete monitör, UYAP duruşma günü kontrolü
- AAÜT (Avukatlık Asgari Ücret Tarifesi) hesap aracı
- AİHM başvuru hazırlık (AYM ret sonrası 4 ay süreci)
