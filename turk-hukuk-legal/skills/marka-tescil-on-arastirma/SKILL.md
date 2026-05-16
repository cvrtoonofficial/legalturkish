---
name: marka-tescil-on-arastirma
description: Türk Patent ve Marka Kurumu (TPMK) nezdinde marka tescil başvurusu öncesinde Sınai Mülkiyet Kanunu (6769) m.5 mutlak ret nedenleri ve m.6 nispi ret nedenleri açısından ön araştırma yapar. Knockout (apaçık çakışma) tespiti, benzerlik analizi metodolojisi, sınıf seçimi (Nice sınıflandırması) önerisi sunar. **Sonuç hukuki görüş değildir; uzman vekil değerlendirmesi gerekir.**
version: 0.2.0
last_legal_review: 2026-05-16
required_mcps:
  - mevzuat_mcp
  - yargi_mcp
optional_mcps:
  - hukuk-rag
applicable_laws:
  - 6769
---

# /fikri-sinai-haklar:marka-tescil-on-arastirma — Marka Tescil Ön Araştırması

> **Bu skill, hukuki görüş değil ön analiz üretir.** TPMK nezdindeki resmî inceleme ve nihai tescil değerlendirmesi yalnızca yetkili Kurum birimlerince yapılır. Marka vekilliği ehliyeti olmayan kişilerin TPMK önünde işlem yapması **SMK m.160** uyarınca sınırlandırılmıştır.



---

## Adım 0 — Zorunlu MCP Çağrıları

> Bu bölüm `meta/MCP-PROTOCOL.md` çerçevesini uygular. Skill çıktısı **bu çağrılar tamamlanmadan** üretilmez.

### 0.1 Profil okuma
- Dosya: `~/.claude/plugins/config/turk-hukuk-legal/CLAUDE.md`
- Yoksa → kullanıcıya `/turk-hukuk-legal:soguk-baslangic-mulakat` çalıştırması önerilir; bu skill yine generic modda çalışır ama çıktı başında **⚠️ Profil yok** uyarısı eklenir.

### 0.2 Mevzuat çekme (`mevzuat_mcp`)
Bu skill için temel kanun numaraları:

- **Kanun 6769** — anahtar kelimeler: "mutlak ret", "nispi ret", "tanınmış marka", "karıştırılma"

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
/fikri-sinai-haklar:marka-tescil-on-arastirma "<marka önerisi>" --sinif=<nice>
```

## İş Akışı

### Adım 1 — Marka Bilgilerini Topla

- **Marka adı / işaret:** (kelime, şekil, kelime+şekil, ses, hareket, vb.)
- **Marka tipi:** (SMK m.4 — ayırt edici nitelikteki her işaret)
- **Başvuru sahibi:** (gerçek/tüzel kişi, vatandaşlık — Paris öncelik hakkı için)
- **Hedef mal/hizmet sınıfları:** Nice sınıflandırması (NCL)
- **Coğrafi kullanım:** (TR + paralel başvurular: AB EUIPO, WIPO Madrid Sistemi?)
- **Faaliyet tarihi:** Önceye dayalı kullanım iddiası için

### Adım 2 — Mutlak Ret Nedenleri Tarama (SMK m.5)

> Madde metni `mevzuat_mcp.search_within_kanun(mevzuat_no="6769", keyword="mutlak ret")` ile çekilir.

Aşağıdaki başlıkları sistematik olarak tara:

| Bent | Konu | Knockout işareti |
|---|---|---|
| m.5/1-a | Ayırt edici nitelikten yoksun | Generik kelime, tek harfli, sadece tarif edici |
| m.5/1-b | Mal/hizmetin niteliğini gösteren | "EKMEK" markasıyla 30. sınıf ekmek başvurusu |
| m.5/1-c | Mal/hizmetin cins/çeşit/vasıf | "TAZE" markası 29. sınıf gıdada |
| m.5/1-ç | Ticaret hayatında herkesçe kullanılan | "PRO", "ECO" gibi yaygın ekler tek başına |
| m.5/1-d | Halkı yanıltıcı | Coğrafi olmayan yerle ilgili işaret |
| m.5/1-e | Coğrafi işaretten oluşan | Tescilli coğrafi işaretle çakışma (SMK m.34 vd.) |
| m.5/1-f | Devlet/uluslararası amblem | T.C., Kızılay, OECD, vb. |
| m.5/1-g | Halkın dini/manevi değerleri | Kutsal sayılan isim/sembol |
| m.5/1-h | Kamu düzeni / ahlaka aykırı | Argo, hakaret içerikli işaretler |
| m.5/2 | Kullanımla ayırt edicilik kazanma | İstisna: uzun süreli yoğun kullanım kanıtı |

**Knockout testi:** Yukarıdaki bentlerden biri açıkça uyduğunda **başvuru reddedilme riski yüksek**. Yine de kullanımla ayırt edicilik (m.5/2) ve istisna durumlar var.

### Adım 3 — Nispi Ret Nedenleri (SMK m.6) — Benzerlik Analizi

Bu, ön araştırmanın **en kritik** kısmıdır. Sadece otomasyonla yapılamaz; uzman değerlendirmesi gerekir.

#### 3a. TPMK Marka Veritabanı Tarama

> **Not:** Bu skill TPMK'nın resmî veritabanına doğrudan bağlanmaz. Vekille birlikte yapılacak işlemler:
> - TPMK Marka Araştırma servisi (turkpatent.gov.tr/arastirma)
> - WIPO Madrid Monitor (uluslararası tescil için)
> - EUIPO eSearch plus (AB için)

Sorgu örüntüsü:
1. **Birebir aynı işaret + aynı sınıf** → otomatik ret riski (m.6/1)
2. **Aynı / benzer işaret + aynı / benzer sınıf** → karıştırılma ihtimali değerlendirmesi (m.6/1)
3. **Tanınmış marka kontrolü** (m.6/4, m.6/5) — başka sınıfta bile risk
4. **Önceki kullanım** (m.6/3) — tescil edilmemiş ama önceye dayalı hak sahibi

#### 3b. Karıştırılma İhtimali Faktörleri (Yargıtay 11. HD Yerleşik Kriterler)

Yargıtay 11. HD'nin yerleşik içtihatlarına göre karıştırılma ihtimali değerlendirilirken bakılan başlıca faktörler — **`yargi_mcp.search` ile somut karar örnekleri çekilebilir**:

- **İşaret benzerliği:** Görsel + sescil (fonetik) + kavramsal benzerlik (üçlü test)
- **Mal/hizmet benzerliği:** Aynı sınıfta olmak yetmez; aynı sınıftaki farklı alt gruplarda da farklılık olabilir
- **Tüketici dikkat seviyesi:** Lüks mal yüksek, tüketim malı düşük dikkat seviyesi
- **Markanın tanınmışlık derecesi:** Tanınmış marka yararına geniş koruma
- **Önceki markanın ayırt edicilik düzeyi:** Düşük ayırt edici unsurlar (jenerik kısaltma) zayıf koruma

#### 3c. Tanınmış Marka Listesi (TPMK)

- TPMK tarafından tanınmış marka tescil sistemi mevcuttur (SMK m.6/4 atfı)
- Liste TPMK'dan ücretli ya da WIPO Well-Known Marks veritabanı üzerinden incelenir
- Tanınmış markayla benzer işaret **farklı sınıfta bile** reddedilebilir

### Adım 4 — İçtihat Tara

Spesifik benzerlik çakışması için:

```
yargi_mcp.search("marka tescil ret SMK 6/1 karıştırılma ihtimali [örnek kelime]")
```

Yargıtay 11. HD ve eski 11. Ceza Dairesinin SMK içtihatları rehberdir. **Daire numaraları değişebilir; her kullanımda doğrula.**

### Adım 5 — Risk Skoru ve Tavsiye

| Renk | Anlam | Tavsiye |
|---|---|---|
| 🟢 **YEŞİL** | Mutlak ret tetikleyici yok, nispi ret çakışması bulunamadı | Marka vekiliyle başvuru hazırlama |
| 🟡 **SARI** | Belirli risk var; uzman değerlendirmesi şart | Vekille tartış, gerekirse alternatif işaret düşün |
| 🔴 **KIRMIZI** | Net knockout veya kuvvetli benzerlik | Markayı değiştirmek veya rebrand önerilir |

### Adım 6 — Sınıflandırma Önerisi (Nice — NCL)

- Hangi 45 sınıf seçilecek?
- **Ek sınıf maliyeti** her yıl güncellenir — TPMK ücret tarifesinden teyit edilmeli
- Akıllı yaklaşım: ana faaliyet + komşu sınıflar + olası genişleme
- Aşırı kapsam **kötü niyet** suçlamasına yol açabilir (m.6/9)

### Adım 7 — Çıktı Formatı

```markdown
## Marka Ön Araştırma Raporu

**Marka:** [...]
**Tip:** [Kelime / Şekil / Karma / ...]
**Hedef sınıflar:** [Nice X, Y, Z]
**Coğrafi kapsam:** [TR / TR + AB / Madrid sistemi]

---

### Mutlak ret tarama (SMK m.5)
- m.5/1-a (ayırt edicilik): [DEĞERLENDİRME]
- m.5/1-b (tarif edicilik): [DEĞERLENDİRME]
- ...

### Nispi ret tarama (SMK m.6)
- TPMK veritabanı: [TARAMA SONUCU — vekille tekrar edilmeli]
- Birebir / yakın işaret bulundu mu: [Evet/Hayır + örnek tescil numaraları]
- Tanınmış marka çakışması: [Var/Yok + açıklama]

### İçtihat referansları
- [yargi_mcp'den çekilen karar özetleri]

### Risk skoru: [🟢 / 🟡 / 🔴]

### Sonraki adımlar
1. Marka vekiliyle resmi araştırma (turkpatent.gov.tr/arastirma)
2. [Gerekirse] alternatif işaret değerlendirme
3. Başvuru tarihinin belirlenmesi (öncelik için)
4. Madrid başvurusu / EUIPO eş zamanlılığı
```

## Sık Karşılaşılan Hatalar

1. **TPMK Marka Bülteni'ne bakmamak** — başvuru sonrası 2 ay içinde itiraz süresi var (SMK m.18/3 — doğrulanacak)
2. **Önceye dayalı kullanım hakkını göz ardı etmek** — m.6/3 tescilsiz ama önceye dayalı kullananı korur
3. **Tanınmış marka geniş koruma** — farklı sınıfta da risk
4. **Kötü niyetli tescil** — m.6/9, m.25/1-c — özellikle ünlü yabancı markaları "yedek" alma çabaları
5. **Domain ve marka ayrı sistemler** — domain almak marka hakkı yaratmaz

## Yetki Sınırı

Bu skill **marka vekili veya marka konusunda uzman avukat denetimi olmadan** başvuru sürecini yürütmek için kullanılamaz. TPMK önünde resmî temsil yetkisi **marka vekili siciline kayıtlı** vekillerle sınırlıdır.

## Disclaimer

Çıktı **hukuki görüş değildir**. Mevzuat ve içtihat referansları her kullanımda `mevzuat_mcp` ve `yargi_mcp` ile yeniden doğrulanmalıdır. **TPMK resmî tescil incelemesi** ile bu skill'in ön araştırması farklı şeylerdir.


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

