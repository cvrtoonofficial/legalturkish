---
name: sozlesme-inceleme
description: Bir sözleşmeyi büronun standart pozisyonlarına göre madde madde inceler — Türk Borçlar Kanunu (6098), Türk Ticaret Kanunu (6102), Tüketicinin Korunması Hakkında Kanun (6502) ve gerekirse özel mevzuat eksenli. Sapmaları işaretler, alternatif metin önerir, ticari etkisini özetler. Tedarikçi sözleşmesi, müşteri sözleşmesi, lisans, dağıtım, hizmet, danışmanlık, distribütörlük, çerçeve sözleşmesi tipleri için uygundur.
version: 0.2.0
last_legal_review: 2026-05-16
required_mcps:
  - mevzuat_mcp
  - yargi_mcp
optional_mcps:
  - hukuk-rag
applicable_laws:
  - 6098
  - 6102
  - 6502
  - 5846
  - 6769
  - 6698
---

# /turk-hukuk-legal:sozlesme-inceleme — Sözleşme İnceleme

Sözleşme: @$1



---

## Adım 0 — Zorunlu MCP Çağrıları

> Bu bölüm `meta/MCP-PROTOCOL.md` çerçevesini uygular. Skill çıktısı **bu çağrılar tamamlanmadan** üretilmez.

### 0.1 Profil okuma
- Dosya: `~/.claude/plugins/config/turk-hukuk-legal/CLAUDE.md`
- Yoksa → kullanıcıya `/turk-hukuk-legal:soguk-baslangic-mulakat` çalıştırması önerilir; bu skill yine generic modda çalışır ama çıktı başında **⚠️ Profil yok** uyarısı eklenir.

### 0.2 Mevzuat çekme (`mevzuat_mcp`)
Bu skill için temel kanun numaraları:

- **Kanun 6098** — anahtar kelimeler: "sorumluluk", "borçlu", "ifa", "fesih"
- **Kanun 6102** — anahtar kelimeler: "haksız rekabet", "ticari", "şirket"
- **Kanun 6502** — anahtar kelimeler: "ayıp", "tüketici", "haksız şart"
- **Kanun 5846** — anahtar kelimeler: "mali hak", "manevi hak", "lisans"
- **Kanun 6769**
- **Kanun 6698** — anahtar kelimeler: "veri sorumlusu", "veri işleyen"

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
## Davet

```
/turk-hukuk-legal:sozlesme-inceleme [dosya | URL | metin]
```

Sözleşme dosya yüklemesi (PDF, DOCX), CLM/bulut depolama linki veya yapıştırılan metin olarak verilebilir.

## İş Akışı

### Adım 1 — Bağlam Topla

Şu bilgiler olmadan inceleme yüzeysel kalır:

1. **Hangi taraftasın?** (alıcı / satıcı, kiracı / kiralayan, lisans alan / veren, asıl / vekil)
2. **Son tarih?** (önceliklendirmeyi etkiler — ay sonu kapanışta sadece kırmızı bayraklar; bolca süre varsa sarı bayraklara da inilebilir)
3. **Hassasiyet alanı?** (örn. "veri koruma kritik", "fikri haklar önemli", "süre esnekliği lazım")
4. **Ticari bağlam?** (anlaşma büyüklüğü, müvekkilin stratejik önemi, mevcut ilişki, sözleşme yenileme mi yeni mi)

Kısmi bağlam verilirse mevcutla devam edilir, varsayımlar belirtilir.

### Adım 2 — Büro Standart Pozisyonlarını Yükle

`buro.local.md` dosyasında tanımlı:
- **Tercih edilen pozisyonlar** (örn. sorumluluk sınırı 12 aylık fatura tutarı)
- **Kabul edilebilir aralık** (eskalasyonsuz onaylanabilir)
- **Yükseltme tetikleyicileri** (kıdemli görüş veya yönetim onayı gerektiren maddeler)

Standart yoksa, Türk pratiğinde yaygın "piyasa standardı" değerlerle ilerle ve bunu açıkça belirt.

### Adım 3 — Sözleşmenin Tipini ve Hukuki Çerçevesini Belirle

| Sözleşme tipi | Ana mevzuat |
|---|---|
| Genel ticari sözleşme | TBK (6098), TTK (6102) |
| Tüketici sözleşmesi | TKHK (6502) — emredici hükümler ön planda |
| Mal satım | TBK m.207 vd., TTK m.23 vd. (ticari satım) |
| Hizmet | TBK m.393 vd. (hizmet sözleşmesi), eser sözleşmesi farklı (m.470 vd.) |
| Eser | TBK m.470 vd. |
| Vekâlet | TBK m.502 vd. |
| Komisyon, simsarlık | TBK m.532+ |
| Kira (konut/çatılı işyeri) | TBK m.299-356 — özel emredici koruma |
| Adi şirket | TBK m.620 vd. |
| Dağıtım, distribütörlük | TBK kıyasen + TTK |
| Lisans / mali hak devri | FSEK m.48-52 (yazılı şekil + ayrı sayma) |
| Yazılım | FSEK m.2/1 (yazılım eseri) |
| Sigorta | TTK m.1401 vd. |
| Kıymetli evrak | TTK 3. Kitap |

Sözleşme tipi belirsizse hibrit (mixed contract) olarak işle; ağırlıklı niteliğine göre baskın hükümleri uygula (TBK m.27/2 — kısmi geçersizlik).

### Adım 4 — Madde Madde Tarama

Aşağıdaki ana madde gruplarını sistematik tarayın. Her grubu büro pozisyonu × emredici hükümler matrisinde değerlendirin.

#### 4.1 Sorumluluk sınırlaması

**Kontrol edilecek:**
- Sorumluluk üst sınırı (sabit tutar / aylık fatura çarpanı / sınırsız)
- Karşılıklı mı tek taraflı mı
- Sınırın istisnası olan kalemler (örn. fikri haklar tecavüzü, KVKK ihlali, gizlilik ihlali, kasıt ve ağır kusur)
- Dolaylı, ek, özel, cezai zarar dışlamaları

**Emredici sınırlar (Türk hukuku özel notlar):**
- **TBK m.115:** Kasıt ve ağır kusurdan doğan sorumluluğu önceden kaldırma anlaşmaları **kesin hükümsüzdür**. "Tüm sorumluluk kaldırılır" tipi maddeler bu sınırı aşar.
- **TBK m.116:** İfa yardımcısının ağır kusurundan sorumluluk anlaşma ile kaldırılamaz.
- **TKHK** kapsamında tüketici aleyhine sorumluluk sınırlaması daha sıkı denetlenir.
- **TTK ticari hayat** — basiretli tacir prensibi (TTK m.18), iki taraf da tacirse standart hükümlere uyum beklenir.

**Sık hatalar:**
- Üst sınırın altında "tüm zararlar" şeklinde geniş istisna — sınır fiilen sıfırlanır
- Karşı tarafa lehine asimetrik istisnalar
- Kasıt ve ağır kusurun dışlanmaması (emredici sınır)

#### 4.2 Tazminat ve garanti

- Garanti süresi (ayıba karşı tekeffül — TBK m.219 vd., TTK m.23 ticari satımda muayene ve ihbar)
- Ayıp ihbarı süresi — ticari satımda 2 gün/8 gün/6 ay sınırları
- Onarım/değişim/bedel indirimi/sözleşmeden dönme seçimlilik
- Garanti dışı bırakılan zararlar
- Üçüncü kişi taleplerinden korunma

**Türk hukuku özel notlar:**
- TBK m.219 satıcı, malın vaat ettiği özelliklerden ve yararlanma amacına uygunluktan sorumludur. Bu emredici nitelikli — sözleşmeyle tamamen kaldırılamaz.
- Tüketici sözleşmelerinde TKHK 6502 m.11 ayıp hakları **2 yıl** ve daha sıkı.

#### 4.3 Fikri ve sınai haklar

- Önceki mevcut fikri haklar (background IP) — kimde kalır?
- Gelişmiş haklar (foreground IP) — kime ait?
- Lisans / devir kapsamı, süre, coğrafi alan, münhasırlık
- Alt lisans yetkisi
- İade / iptal hakkı

**Kritik Türk hukuku şartları:**
- **FSEK m.48-52:** Mali hak devri ve lisansı **yazılı şekle bağlı**. Devredilen haklar **ayrı ayrı sayılmalı** (m.52); "tüm mali haklar" gibi genel ifade yetersizdir.
- **FSEK m.16-19:** Manevi haklar (eseri umuma sunma, ad belirtme, eserde değişiklik yapmama) **devredilemez**. Sözleşmede "manevi haklar devredilir" yazıyorsa hükümsüzdür; sadece kullanım yetkisi kurulabilir.
- **FSEK m.51:** İleride yapılacak eserlere ilişkin mali hak devir sözleşmeleri 3 yıllık üst sınır altında değerlendirilir.
- **SMK m.148 vd.** (verify): Marka, patent, tasarım devri yazılı şekle bağlı ve TPMK siciline kaydı üçüncü kişilere etkililik için şart.
- **SMK m.113-122** (verify): Çalışan buluşları — istihdam ilişkisinde yapılan buluşların rejimi ayrı.

**Sık hatalar:**
- Mali hakların "toplu" devri
- Manevi hakların devri yazılması (otomatik hükümsüz)
- Yazılım sözleşmesinde kaynak kod sahipliği belirsizliği
- Açık kaynak bileşenlerin lisans tetikleyicileri görmezden gelinmesi

#### 4.4 Veri koruma (KVKK)

- Veri işleme amacı, hukuki sebep
- Veri sorumlusu / veri işleyen ayrımı
- Alt veri işleyen onay mekanizması
- Veri ihlali bildirim süresi (KVKK m.12 + Kurul kararları — 72 saat eğilim)
- Yurt dışı veri aktarımı mekanizması (KVKK m.9 — açık rıza, yeterli koruma, taahhütname)
- Saklama süresi ve sona erdirme yükümlülüğü
- Denetim hakkı

**Türk hukuku özel notlar:**
- KVKK m.11 ilgili kişi haklarına yanıt yükümlülüğü her zaman veri sorumlusunda kalır; veri işleyene devredilemez.
- VERBİS kaydı yükümlülüğü tarafların ayrı ayrı sorumluluğudur.
- KVKK Kurulu kararları zaman zaman süreler ve gereklilikler için pratik standart koyar — `yargi_mcp.search_kvkk_decisions` ile güncel hat doğrulanmalı.

#### 4.5 Gizlilik

- Gizli bilgi tanımı (kapsam, tanım nesnel mi)
- Saklama yükümlülüğü süresi (genelde 2-5 yıl, ticari sır için daha uzun olabilir)
- İstisnalar (kamusal alan, bağımsız geliştirme, kanuni zorunluluk)
- Çalışan ve danışmana paylaşım hakkı
- Sona ermeden sonra iade veya imha

#### 4.6 Garantiler ve beyanlar

- Tarafların yetki ve ehliyet beyanı
- Üçüncü kişi haklarına tecavüz etmediği beyanı (özellikle yazılım/içerik tedarikinde)
- KVKK uyum beyanı
- Açık kaynak beyanları

#### 4.7 Süre ve fesih

- Sözleşme süresi (belirli / belirsiz)
- Otomatik yenileme tetiği (önceden bildirim süresi)
- Bedelsiz fesih (terminate for convenience)
- Haklı sebebe dayalı fesih (TBK m.435 hizmet için, m.484 eser için, vb.)
- Fesih sonrası yan yükümlülükler (gizlilik, sorumluluk, garanti devamı)

**Türk hukuku özel notlar:**
- Konut ve çatılı işyeri kirasında TBK m.347 vd. uzatma rejimi emredici niteliklidir; sözleşmeyle aleyhe değiştirilemez.
- Hizmet sözleşmesinde haklı sebebe dayalı derhal fesih hakkı tarafların önceden vazgeçemediği bir haktır (TBK m.435).

#### 4.8 Uygulanacak hukuk & uyuşmazlık çözümü

- Uygulanacak hukuk seçimi
- Yetkili mahkeme (HMK m.17 — kesin yetki istisnaları, m.18 yetki sözleşmesi)
- Tahkim (4686 sayılı MTK, ISTAC, ICC)
- Arabuluculuk zorunluluğu (özellikle ticari uyuşmazlıklarda dava şartı arabuluculuk — 6325 SK)

**Türk hukuku özel notlar:**
- 6325 SK m.18/A: Ticari uyuşmazlıklarda dava açmadan **arabulucuya başvuru dava şartıdır**. Sözleşmede aksi yazsa da bu kural uygulanır.
- İş uyuşmazlıkları için 7036 SK ile arabuluculuk dava şartıdır.
- HMK m.17: Kesin yetki halleri (taşınmaz davalarının bulunduğu yer, vb.) — sözleşmeyle değiştirilemez.

#### 4.9 Devir, alt yüklenicilik

- Sözleşmenin devri (yazılı izin şartı)
- Kontrol değişikliği klozu
- Alt yüklenici çalıştırma
- Tarafların değişmesi halinde devamı

#### 4.10 Mücbir sebep

- Kapsam (yetkili tanımı; pandemi, savaş, doğal afet, idari karar, vb.)
- Bildirim süresi
- Fesih hakkı kazanma eşiği

**Türk hukuku notu:** Mücbir sebep TBK'da genel olarak m.136 (ifa imkânsızlığı) ve m.138 (aşırı ifa güçlüğü) ile düzenlenmiştir. Sözleşme klozu bu hükümleri tamamen bertaraf edemez ama tanım/bildirim/sonuç netleştirir.

#### 4.11 Ödeme şartları

- Vade (genelde net 30 / net 60 / net 90)
- Geç ödeme faizi (TBK m.120 — taraflar arasında belirlenmemişse yasal faiz; ticari işlerde avans faiz oranı)
- Vergi yansıtması
- Fiyat ayarlaması (TÜFE / döviz)

### Adım 5 — Sapma Sınıflandırması

Her madde için:

- 🟢 **YEŞİL:** Büro standart pozisyonu karşılanıyor veya kabul edilebilir aralıkta
- 🟡 **SARI:** Sapma var, müzakerede değişiklik istenmeli, gerekirse kıdemli görüş
- 🔴 **KIRMIZI:** Yükseltme tetikleyici, sözleşme bu haliyle imzalanmamalı

### Adım 6 — Sözleşmeyi Bütüncül Değerlendir

Maddeler arası etkileşim:
- Sorumluluk sınırı düşük ama tazminat istisnası geniş = fiilen sınırsız
- Fikri hak devri geniş ama garanti yok = alıcı korumasız
- KVKK ek protokolü eksik ama veri işleme öngörülüyor = uyum boşluğu
- Mücbir sebep dar ama sözleşmeden dönme kuralları sıkı = kilitlenme riski

### Adım 7 — Çıktı

```markdown
## Sözleşme İnceleme Raporu

**Sözleşme:** [tanım]
**Müvekkilin tarafı:** [...]
**Sözleşme tipi:** [...]
**Genel risk düzeyi:** [Düşük / Orta / Yüksek]

---

### Yönetici özeti
[3-5 cümle: imzalanabilir mi, kaç kırmızı bayrak var, ana endişe]

### Kırmızı bayraklar
1. **[Madde X]** — [sapma] | Risk: [ne olabilir] | Öneri: [değişiklik metni]
2. ...

### Sarı bayraklar
1. ...

### Yeşil — kabul edilebilir
[Madde özet listesi]

### Müzakere önceliği
| Öncelik | Madde | İstenecek değişiklik | Geri çekilme pozisyonu |
|---|---|---|---|
| 1 | ... | ... | ... |

### Mevzuat doğrulaması
- TBK m.X: [mevzuat_mcp ile doğrulandı / doğrulanacak]
- FSEK m.52: [...]
- KVKK m.11: [...]

### İçtihat referansları (yargi_mcp)
- ...

### Sonraki adımlar
1. Müvekkille kırmızı bayrakların önceliklendirilmesi
2. Müzakere için redline taslağı
3. Karşı tarafa gönderim
```

## Sık Karşılaşılan Sözleşme Türleri için Hızlı Notlar

### SaaS / yazılım hizmeti
- Veri konumu (TR'de mi, yurt dışında mı) — KVKK m.9 etkili
- SLA + ceza tutarı
- Veri taşınabilirliği ve sözleşme sonu çıkış
- Açık kaynak bileşen beyanı

### Distribütörlük / acentelik
- Münhasırlık + bölge
- Hedef cirolar + cezai şart
- TTK m.102 vd. acentelik bağımsızlığı emredici hükümleri
- Tazminat hakkı (denkleştirme bedeli — TTK m.122) — feshe rağmen istenebilir

### Lisans (fikri hak)
- FSEK m.52 ayrı ayrı sayım
- Süre, alan, münhasırlık
- Türev eser oluşturma hakkı
- Alt lisans

### Kira (konut/çatılı işyeri)
- TBK m.299-356 emredici — sözleşmede aleyhe sapma hükümsüz
- Uzatma rejimi
- Tahliye sebepleri sınırlı

### Tüketici sözleşmesi
- TKHK 6502 emredici hükümler
- Mesafeli satışlar — cayma hakkı
- Genel işlem koşulları (TBK m.20-25) — sürpriz şart, dengesizlik denetimi

## Notlar

- Mevzuat ve içtihat her kullanımda yeniden doğrulanır.
- Müvekkile sunulan rapor önce müvekkilin teknik / ticari ekibiyle de paylaşılmalı (ticari etkiyi anlayabilmek için).
- Karmaşık sözleşmelerde inceleme tek seferlik değil; karşı tarafın redline'ına göre yeniden değerlendirilir.


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

