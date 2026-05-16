# Büro Profili — Türk Hukuku Legal Plugin v0.4.0

> Bu dosya `/turk-hukuk-legal:soguk-baslangic-mulakat` skill'i tarafından doldurulur.
> Tüm diğer skill'ler bu profili **çağrılırken** okur ve çıktıyı kalibre eder.
>
> **Profil eksik kalırsa:** çıktılar "generic" — büronun pratiğine, müvekkil tipine, ihtisas mahkemesi tercihine göre kişiselleştirilmemiş.

---

## 1. Kimlik

| Alan | Değer |
|---|---|
| Tam ad | |
| Mahlas (varsa) | |
| Pratiğin tarafı | (asıl taraf / üçüncü kişi adına / hibrit) |
| T.C. / Vergi no | |
| Tebligat adresi | |
| KEP / UETS adresi | |
| Telefon / e-posta | |
| Sosyal kimlik (sektörel) | (örn. müzisyen, yapımcı, distribütör) |
| Meslek birliği üyelikleri | (MESAM/MSG/MÜYAP/SETEM/MÜZİKBİR/diğer) — üyelik no + tarih |
| TPMK marka vekili sicili | (varsa) |
| Avukatlık ehliyeti | (yoksa — asıl taraf olarak yürütüyor) |
| Standart antet (görsel ref) | (logo dosya yolu varsa) |

## 2. Maruz Olunan Dava Türleri (öncelik sırasıyla)

- [ ] Müzik telif (FSEK) — aktif (X İstanbul davası, vb.)
- [ ] Sanatçı / dijital dağıtım sözleşmesi (Amuse, Spotify, vb.)
- [ ] Sınır ötesi sözleşme (Amuse İsveç — gelecek)
- [ ] Trafik kazası (maddi/manevi tazminat)
- [ ] İdari vergi (VUK + İYUK)
- [ ] Marka / sınai mülkiyet (SMK)
- [ ] AYM bireysel başvuru
- [ ] Diğer: ...

## 3. Saldırganlık Tonu (Assertion Posture)

**Default ton:** {STANDART / ÖLÇÜLÜ / MUHAFAZAKÂR / DEĞİŞKEN}

Bu ton şu skill'lerin default davranışını belirler:
- `dilekce-ihtarname`
- `ihtarname-fsek-smk`
- `dava-strateji-analiz`
- `karsi-arguman-onleme`
- `sinirostesi-sozlesme-fesih`

| Skill | Standart | Ölçülü | Muhafazakâr |
|---|---|---|---|
| Dilekçe | Doğrudan men + tazminat + kısa süre | Müzakere kapısı açık | Görüşme önceli |
| İhtarname | 14 gün, dava ihtarı | 30 gün, uzlaşma | Görüşme talebi |
| Strateji | Sherlock+keskin | Dengeli | Diplomatik |

## 4. Onay Matrisi

| İşlem | Karar verici / Limit |
|---|---|
| Mahkemeye dilekçe | Müvekkil onayı zorunlu |
| Karşı tarafa ihtarname | Müvekkil onayı + ton seçimi |
| Sözleşme imzası — değer × | Müvekkil + (avukat denetimi yoksa) |
| İhtiyati tedbir talebi | Acil ise müvekkil + sonradan teyit |
| AYM bireysel başvuru | Süre kritik — hazırlık başlasın, müvekkil son onay |
| Yabancı yargı / tahkim cevap | Müvekkil + kıdemli görüş tavsiyesi |

## 5. Yetkili Mahkeme Tercihleri

| Konu | Tercih edilen yer |
|---|---|
| Fikri ve sınai haklar hukuk mahkemesi | İstanbul Anadolu / Avrupa |
| BAM (FSEK/SMK) | İstanbul BAM 16. HD (`yargi_mcp` ile doğrula) |
| Asliye Hukuk (trafik) | İstanbul (büyükşehir) |
| Vergi mahkemesi | İstanbul |
| Tüketici mahkemesi | İstanbul (sınır ötesi sözleşme fesih için kritik) |
| Sigorta Tahkim Komisyonu | İstanbul (5684 SK m.30) |
| AYM | Ankara |
| AİHM | Strasbourg (uzun vade) |

## 6. Standart Pozisyonlar

### Sözleşme inceleme

- **FSEK m.52** ayrı sayım zorunlu — sanatçı sözleşmelerinde kırmızı çizgi
- **FSEK m.16-19** manevi haklar devredilemez — kullanım yetkisi olarak değerlendir
- **FSEK m.51** ileride yapılacak eserler 3 yıl üst sınır
- **TBK m.115** kasıt + ağır kusur sorumluluk emredici
- **TKHK m.5** tüketici durumda haksız şart denetimi

### NDA / gizlilik
- Karşılıklı tercih
- 2-3 yıl, ticari sırlar 5+
- Rekabet etmeme / çalışan ayartmama → NDA dışı

### İhtarname & dilekçe ton tercihi
- İlk ihtarname: standart 14 gün
- TBK m.117 temerrüt: 7 gün
- İş akdi fesih: İş K. m.19 verify

### Sınır ötesi
- Yabancı yetki klozu → MÖHUK m.26 + AY m.36 argümanı hazırlanır
- Tüketici konumu kanıtlanırsa Türk yargısı yetki argümanı güçlü

## 7. MCP & Veritabanı Bağlantıları (v0.4.0 — 6 MCP)

### Bağlı MCP'ler

| MCP | URL / komut | Görev |
|---|---|---|
| **mevzuat_mcp** | https://mevzuat.surucu.dev/mcp | Türk mevzuatı (Kanun, KHK, CBK, Yönetmelik, Tebliğ) |
| **yargi_mcp** | https://yargimcp.surucu.dev/mcp | Yargıtay, Danıştay, AYM, BAM, KVKK, Rekabet, GİB özelgeleri, vb. |
| **literatur_mcp** | https://literatur-mcp.surucu.dev/mcp | DergiPark akademik makaleler |
| **yoktez_mcp** | https://yoktezmcp.fastmcp.app/mcp | YÖK Ulusal Tez Merkezi |
| **markapatent_mcp** | https://markapatent-mcp.fastmcp.app/mcp | TÜRKPATENT sicili (marka/patent/tasarım) |
| **hukuk_rag** | uvx hukuk-rag | Büro dosyaları üzerinde semantik arama |

### `hukuk_rag` koleksiyonları

| Koleksiyon | Dosya / Konu | Durum | Default? |
|---|---|---|---|
| cvrtoon_x_istanbul | X İstanbul davası | aktif | evet |
| (yeni dava açıldıkça eklenecek) | | | |

### `yargi_mcp` tercih edilen daireler (verify ile)

| Konu | Daire | Endpoint |
|---|---|---|
| FSEK/SMK | Yargıtay 11. HD | `search_bedesten_unified` |
| Trafik kazası | Yargıtay 4. HD ve 17. HD | `search_bedesten_unified` |
| Vergi | Danıştay 3., 4., 9. Daire + VDDK | `search_bedesten_unified` |
| KVKK | KVKK Kurulu | `search_kvkk_decisions` |
| AYM bireysel başvuru | AYM | `search_anayasa_unified` |
| Sigorta Tahkim | Komisyon | (sigorta tahkim ayrı) |
| Tüketici | Yargıtay 13. HD | `search_bedesten_unified` |

### `mevzuat_mcp` favori kanun numaraları

5846 (FSEK) · 6769 (SMK) · 6098 (TBK) · 6102 (TTK) · 6100 (HMK) · 6698 (KVKK) · 5651 · 4857 (İş K.) · 6502 (TKHK) · 2577 (İYUK) · 213 (VUK) · 2918 (KTK) · 5684 (Sigortacılık) · 4721 (TMK) · 6216 (AYM) · 5718 (MÖHUK) · 6325 (Arabuluculuk)

## 8. Tohum Belgeler

| Belge | Yol / Referans | Skill |
|---|---|---|
| Dava Dilekçesi (X İstanbul) | hukuk-rag:cvrtoon_x_istanbul | dilekce-ihtarname, dava-strateji-analiz |
| Sanatçı sözleşmesi örneği | (yüklenecek) | sanatci-sozlesme-inceleme |
| İhtarname örneği | (yüklenecek) | ihtarname-fsek-smk |
| Vergi tarhiyatı örneği (varsa) | (yüklenecek) | vergi-uyusmazligi-analiz |
| Trafik kazası dosyası (varsa) | (yüklenecek) | trafik-kazasi-davasi |

## 9. Çıktı Tercihleri

- **Tarih formatı:** gg.aa.yyyy
- **Para birimi:** TL (USD/EUR gerektiğinde)
- **Numaralandırma stili:** 1., a), (i)
- **Atıf stili:** "5846 sayılı FSEK m.X" + ilgili fıkra
- **Vurgu:** **kalın** + *italik* karma, BÜYÜK HARF sadece başlık ve KONU'da
- **DOCX:** Times New Roman 12pt, satır aralığı 1.15
- **Sayfa düzeni:** 2.5/2.5/3/2 cm kenar boşlukları, sayfa no alt-orta

## 10. Etik ve Saldırganlık Tonu Detayları

### Sherlock yöntemi tercih edilen üslup

- Soğuk + keskin: "Davalının iddiası, kendi başına çelişkili olmakla birlikte..."
- Detektif gözlemiyle: "Bu durum, dava dilekçesi m.X ile kıyaslandığında..."
- Mantıksal zincir: "Karşı iddia kabul edildiği takdirde, mantıksal sonuç olarak..."
- Saldırgan dilden uzak: karşı tarafın çelişkilerini ortaya koy, kişiselleştirme

### Karşı tarafın kişiliğini değil **iddialarını** çürüt

- "Davalı kötü niyetlidir" demek yerine: "Davalının davranışı, TMK m.2 hakkın kötüye kullanımı kapsamında değerlendirilmesi gereken çelişkili bir örüntü göstermektedir."

## 11. Versiyon

- Plugin: v0.4.0
- Profil sürümü: v0.4
- Son güncelleme: 2026-05-16
- Mevzuat son inceleme: 2026-05-16

---

## Kullanım

Her skill çağrıldığında bu profil **okunarak** çıktı kalibre edilir. Skill çıktısının başında:

> 📋 Profil yüklendi: {Kimlik}, Ton={ton}, Yetkili yer tercihi={yer}, Default RAG koleksiyonu={koleksiyon}
