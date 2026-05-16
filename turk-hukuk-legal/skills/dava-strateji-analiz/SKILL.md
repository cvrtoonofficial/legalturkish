---
name: dava-strateji-analiz
description: Bir davanın bizim lehimize çevrilmesi için 5 adımlı Sherlock yöntemi. ÖNCE müvekkille diyalog kurar, davayı tam anlamadan ilerlemez. Sonra (1) bu tip davada hâkimin lehe karar verdiği durumları yargi_mcp ile tarar; (2) karşı tarafın hangi durumlarda kötü niyetli veya usuli hatalı bulunduğunu çıkarır; (3) bizim olgularımızı bu lehe durumlarla eşleştirir; (4) hâkimin ve davalı tarafın öne sürebileceği karşı argümanları önceden tespit eder; (5) Sherlock / şeytanın avukatı tonuyla, hukuki dayanağı sağlam, mahkemeye sunulacak güçlü argümantasyon üretir. Müzik telif, trafik kazası, idari vergi, sınır ötesi sözleşme fesih davaları için optimize.
version: 0.4.0
last_legal_review: 2026-05-16
required_mcps:
  - mevzuat_mcp
  - yargi_mcp
  - hukuk-rag
optional_mcps:
  - literatur-mcp
  - yoktez-mcp
  - markapatent-mcp
applicable_laws:
  - 6100
  - 5846
  - 6769
  - 6698
  - 6098
  - 6102
  - 2918
  - 213
  - 2577
---

# /turk-hukuk-legal:dava-strateji-analiz — Sherlock Strateji Analizi

> Bu skill, plugin'in **kalbidir**. Bir davayı müvekkilin lehine çevirmek için, sıradan bir hukuki analiz değil; **detektif düşüncesi + şeytanın avukatı + hukuk profesörü** üçlüsünü birleştiren bir yöntem uygular.

> **Asla davayı tam anlamadan dilekçeye başlamaz.** İlk adım her zaman müvekkille diyalogdur; merak edilen her şey önce sorulur, sonra yazılır.

## Adım 0 — Zorunlu MCP Çağrıları

### 0.1 Profil okuma
- `~/.claude/plugins/config/turk-hukuk-legal/CLAUDE.md`
- Yoksa: `/turk-hukuk-legal:soguk-baslangic-mulakat` öncelik

### 0.2 5 MCP'nin tamamı bağlı mı kontrol et
- mevzuat-mcp (kanun metni)
- yargi-mcp (içtihat)
- hukuk-rag (büro dosyaları)
- literatur-mcp (DergiPark doktrin)
- yoktez-mcp (YÖK tezleri)
- markapatent-mcp (TPMK — FSEK/SMK davalarında)

Eksik MCP varsa kullanıcıya uyarı: "Bu skill'in tam etkili çalışması için 5 MCP'nin tamamı önerilir. Şu an {N} MCP bağlı; çıktı sınırlı kapsamda olacak."

---

## ADIM 1A — MÜVEKKİLLE DİYALOG (asla atlama)

Dilekçe / strateji üretmeye başlamadan **mutlaka** şu çerçevede sor:

### Temel sorular (her dava için)

1. **Hangi davayız?**
   - Davacı mı, davalı mı, üçüncü kişi/müdahil mi?
   - Yargı kolu: hukuk / ceza / idari / iş / fikri sınai / vergi
   - Aşama: ihtarname öncesi / dava açma / cevap / replik / istinaf / temyiz / AYM / AİHM

2. **Olayın özü 3 cümlede nedir?**
   - Ne oldu (vakıa)
   - Kim yaptı / kim sorumlu (taraflar)
   - Şu an ne aşamada (durum)

3. **Hedefimiz nedir?**
   - Tazminat (manevi/maddi/her ikisi)
   - Men / ref / tespit / hükümsüzlük / iptal
   - İhtiyati tedbir + esas
   - Uzlaşma / arabuluculuk

4. **En çok endişe ettiğim risk nedir?**
   - Karşı tarafın savunması: ...
   - Hâkimin olası tutumu: ...
   - Süre / şekil eksiği: ...

5. **Karşı tarafın profili?**
   - Bireysel / şirket / kamu kurumu / yabancı?
   - Avukat tipi (bireysel avukat / büyük büro)?
   - Önceki yazışmalardan tutum (saldırgan, uzlaşmacı, sessiz, oyalayıcı)?

6. **Elimde hangi deliller var?**
   - Belgeler (tarih sıralı)
   - Tanıklar
   - Bilirkişi raporu (talep edildi mi, geldi mi)
   - Dijital deliller (URL, ekran görüntüsü, noter tespiti)

### Konuya özel sorular

#### Müzik telif (FSEK) davalarıysa
- Eserin türü: musikî / sözlü musikî / aranjman / mix / işlenme / icra kaydı / yapım?
- Eser sahipliği nasıl ispatlanır: FSEK m.11 karinesi mi, kayıt mı, meslek birliği üyeliği mi, stüdyo master mı?
- Meslek birliği yetkisi: MESAM / MSG / MÜYAP / SETEM / MÜZİKBİR'den hangisi devrede?
- Lisans / devir sözleşmesi imzalandı mı? FSEK m.52 yazılı + ayrı sayma şartı karşılanıyor mu?
- Manevi haklar (FSEK m.14-19) ihlali var mı?
- Platform mu, kişisel kullanıcı mı? (5651 Ek m.4 sorumluluk değişir)
- Grok / başka YZ modellerinin eğitiminde kullanım iddiası var mı?

#### Trafik kazası davalarıysa
- Sürücü / yolcu / yaya / yan etki mağduru?
- Kusur durumu: bilirkişi raporu var mı, kusur oranı net mi?
- Sigorta tahkim komisyonuna başvuru yapıldı mı? (zorunlu mali sorumluluk → tahkim)
- Bedensel zarar var mı? Maluliyet raporu var mı?
- 2918 sayılı KTK + TBK m.49+ haksız fiil çerçevesi tartışmalı mı?

#### İdari vergi davalarıysa
- Tarhiyat: VUK ön tarh / takdir / re'sen / ikmâlen?
- 30 / 60 gün İYUK süresi durumu?
- Uzlaşma denenedi mi? (213 SK Ek m.1)
- Vergi mahkemesi → BAM → Danıştay aşaması?
- GİB özelgesi tarama yapıldı mı? (yargi_mcp ile)

#### Sınır ötesi sözleşme fesih (Amuse vb.)
- Sözleşmede uygulanacak hukuk + yetkili mahkeme klozu?
- Müvekkil tüketici konumunda mı (MÖHUK m.26 + AB Tüketici Hukuku)?
- Yargılama masrafının orantısız olduğuna dair somut kanıt? (AİHS m.6 etkili başvuru)
- Türk mahkemesinde yetki kabul edilebilmesi için gereken eşik?

### Müvekkilden onay almadan ilerleme

Tüm soruların **temel** olanları cevaplanmadan strateji yazılmaz. Kullanıcı "biliyorsun zaten" derse, **bildiğin yere onay iste** — yanlış varsayım stratejiyi mahveder.

---

## ADIM 1B — DAVA TİPİNİ KESİN OLARAK SINIFLANDIR

| Sınıflama | Atıf yapılacak mevzuat | Yargı yeri | Yargıtay daire (verify) |
|---|---|---|---|
| Müzik telif tecavüzü | FSEK 5846 m.21-25, 66-70, 77 | Fikri ve Sınai Haklar Hukuk Mahkemesi | Yargıtay 11. HD |
| Marka tecavüzü | SMK 6769 m.7, m.29, m.149 | Fikri ve Sınai Haklar Hukuk Mahkemesi | Yargıtay 11. HD |
| Patent tecavüzü | SMK m.85, m.141 | Fikri ve Sınai Haklar Hukuk Mahkemesi | Yargıtay 11. HD |
| Trafik kazası bedensel | TBK m.49+, KTK 2918 | Asliye Hukuk | 4. HD (verify) |
| Trafik kazası maddi | KTK 2918, sigorta tahkim | Tahkim → Asliye Hukuk | — |
| İdari işlem iptali | İYUK 2577 m.2/1-a | Vergi mahkemesi | Danıştay 3/4/9. D (konuya göre) |
| Tam yargı davası | İYUK m.2/1-b | İdari mahkeme | Danıştay |
| Tüketici sözleşmesi fesih (sınır ötesi) | TKHK + MÖHUK m.26 | Tüketici Mahkemesi | 13. HD (verify) |
| KVKK ihlali | KVKK 6698 m.11-14 | İdare mahkemesi (Kurul kararına) | Danıştay 10. D (verify) |

`mevzuat_mcp` ile her madde **doğrulanır**. Yargıtay daire numaraları her kullanımda `yargi_mcp` ile teyit edilir.

---

## ADIM 2 — LEHE İÇTİHAT TARAMASI (Sherlock'un kanıt toplaması)

Yargıtay, Danıştay, BAM, AYM ve sektörel kurum kararlarını **bizim taraf lehine** kararları arar:

### 2.1 Sorgular

`yargi_mcp.search_bedesten_unified` ve uygun spesifik endpoint'lerle:

#### Müzik telif örneği
- `"FSEK 68 üç kat rayiç bedel" davacı lehine`
- `"FSEK 11 eser sahipliği karinesi" davacı`
- `"FSEK 80 bağlantılı haklar" yapımcı icracı`
- `"FSEK 77 ihtiyati tedbir teminat şartı yok"`
- `"meslek birliği yetki" Yargıtay 11. HD`

#### Trafik kazası örneği
- `"trafik kazası kusur oranı bilirkişi raporu" lehe`
- `"KTK 85 sürücü kusuru" lehine`
- `"sigorta tahkim destek karar" davacı`
- `"bedensel zarar maluliyet hesabı"`

#### İdari vergi örneği
- `"VUK 30 re'sen takdir hatası iptal"`
- `"İYUK 11 üst makama başvuru süresi"`
- `"vergi iadesi davacı lehine Danıştay"`
- `"uzlaşma kabul edilmedi ek tarhiyat"`

#### AYM / AİHM
- `yargi_mcp.search_anayasa_unified("adil yargılanma hakkı ihlali")`
- AYM ihlal kararları davanın anayasal boyutu için

### 2.2 Çıktı: lehe argüman bankası

Her bir karardan çıkan **somut argüman** + esas/karar numarası kayıt edilir:

```
ARGÜMAN 1: FSEK m.68 üç kat tazminat hesabında kasıt veya ağır ihmal şartı,
karşı tarafın platform niteliğindeyse, ACR sistemi kurmamasının kendi başına
"ağır ihmal" oluşturduğu yönünde içtihat var.
→ Kaynak: Yargıtay 11. HD, E. ..., K. ..., T. ... [yargi_mcp doğrulanmış]
→ Bizim olgu uygunluğu: ⭐⭐⭐⭐⭐ — X İstanbul'da ACR yok argümanı doğrudan uyuyor.

ARGÜMAN 2: ...
```

### 2.3 Doktrin desteği

`literatur-mcp` ve `yoktez-mcp` ile akademik destek:
- DergiPark son 5 yıl konuya ilişkin makaleler
- YÖK tezlerinden ilgili lisansüstü/doktora çalışmaları
- Çoğunluk görüşü / azınlık görüşü ayrımı

Doktrin, içtihat zayıfsa **destek argüman**; içtihat güçlüyse **pekiştirme**.

---

## ADIM 3 — KARŞI TARAFIN ZAYIFLIKLARI (Şeytanın avukatı bakış açısı)

Karşı tarafın sunduğu / sunabileceği savunmaları **hipotetik olarak kabul** et, sonra her birinin nerede çatladığını bul:

### 3.1 Kötü niyet işaretleri (TMK m.2)

Karşı tarafın **kötü niyetle hareket ettiği**ni gösteren tipik durumlar:

| Senaryo | Hukuki sonuç |
|---|---|
| Karşı taraf, sözleşmeye dayanırken aynı zamanda sözleşmeden doğan **kendi yükümlülüğünü** ihlal ediyor | TMK m.2 hakkın kötüye kullanımı |
| Karşı taraf, ihtarnameye süresinde cevap vermiyor ama dava açılınca "bildirim yapılmadı" iddiası | Çelişkili davranış yasağı (TMK m.2) |
| Karşı taraf, müvekkilin ekonomik gücünden faydalanarak süre uzatma talepleri | Hakkın kötüye kullanımı |
| Karşı taraf, paralel forumlarda **çelişkili iddialar** ileri sürmüş | Stoppel benzeri TMK m.2 |
| Karşı taraf, **gözlemlenebilir tedbir** almamış ama sorumluluğu reddediyor | İhmal/kasıt argümanı |

### 3.2 Usuli hatalar

Karşı tarafın HMK / İYUK / CMK kapsamında düşebileceği tipik usul kusurları:

- **Husumet itirazı zamanını kaçırma** (HMK m.116/1-a)
- **Yetki sözleşmesinin geçerli olmaması** (kesin yetki + tüketici)
- **Cevap dilekçesinin süresinde sunulmaması** (HMK m.127)
- **Vekâletname eksikliği** (özel yetkinin tam olmaması)
- **Delil sunma süresi geçmesi** (HMK m.121)
- **Belirsiz alacak davası harcının yatırılmaması**
- **Bilirkişi rapor itirazının süresinde sunulmaması** (HMK m.281)
- **İstinaf gerekçesinin yetersiz olması** (HMK m.353)
- **İYUK süre hesabında hata** (60 gün vs. 30 gün konuya göre)
- **Vergi ihtirazı kaydı tutulmamış olması**

### 3.3 Esasa ilişkin zaaflar

Karşı tarafın **kendi temellerinin** çatlayabileceği yerler:

#### Müzik telif örneği — karşı tarafın zaafları
- Lisans kanıtı yok → "Nemo plus iuris..." (kullanıcının verebileceği lisans yetersiz)
- Üçüncü kişinin yüklediği iddiası → ama platform sorumluluğu (5651 Ek m.4 + ACR yokluğu)
- "DMCA bildirimi yapılmadı" → Türk yargısında geçerli değil (MÖHUK + emredici hukuk)
- ToS'taki lisans klozu → FSEK m.52 emredici hükme aykırı, hükümsüz

#### Trafik kazası örneği — karşı tarafın zaafları
- Bilirkişi raporu yapay seçilmiş → ek rapor / yenileme talebi
- Sigorta poliçesi süresi geçmiş → poliçe geçerlilik tartışması
- Sürücünün alkollü olduğu → KTK m.95 + kusur çarpması yüksek

#### Vergi örneği — karşı tarafın (idarenin) zaafları
- Re'sen tarhiyat gerekçesizliği → VUK m.30 sebebi yetersiz
- İncelemeli yapılan tarhiyatın incelemenin sınırlarını aşması
- Mükellefe savunma hakkı verilmemesi → AY m.36 ihlali → AYM yolu

---

## ADIM 4 — EŞLEŞTİRME (Bizim olgular ↔ lehe içtihat + karşı tarafın zaafları)

Adım 2'deki argüman bankasını + Adım 3'teki karşı taraf zayıflıklarını **bizim somut olgularımızla** eşleştir:

```
BİZİM OLGU 1: X İstanbul platformunda ACR sistemi yok (dava dilekçesi m.20).
↓
EŞLEŞTİĞİ LEHE İÇTİHAT: Yargıtay 11. HD, ...E ...K — ACR yokluğu ağır ihmal sayılır.
EŞLEŞTİĞİ KARŞI ZAYIFLIK: Karşı taraf "biz iyi niyetli platformuz" diyemez (ACR yoksa).
SONUÇ ARGÜMAN: Davalı, mevcut teknik standartların gerektirdiği denetim mekanizmasını
kurmayarak FSEK m.66/2'deki "ihtimam yükümlülüğü"nü ihlal etmiştir.

BİZİM OLGU 2: Davalı 13.02.2026 tarihli ihtarnamaya makul sürede cevap vermedi.
↓
EŞLEŞTİĞİ LEHE İÇTİHAT: TMK m.2 — çelişkili davranış yasağı; ihtarnameye
sessiz kalma + dava açılınca "bildirim yapılmadı" iddiası TMK m.2 ihlali.
EŞLEŞTİĞİ KARŞI ZAYIFLIK: Karşı tarafın "DMCA bildirimi yapılmadı" savunması
hem MÖHUK açısından geçersiz hem TMK m.2 açısından çelişkili.
SONUÇ ARGÜMAN: Davalının ihtarnameyi yanıtsız bırakıp dava açıldığında "bildirim
yapılmadı" iddiasını ileri sürmesi, hakkın kötüye kullanımı niteliğindedir.
```

Her eşleşme **somut, kanıtlı, mahkemeye sunulabilir** olmalı.

---

## ADIM 5 — HÂKİM VE DAVALI TARAFIN KARŞI ARGÜMANLARINI ÖNGÖRME

Burası kritik: **sen yazmadan önce, karşı taraf ve hâkim ne diyecek?**

### 5.1 Hâkimin olası soruları/şüpheleri

Hâkim genelde şu noktalardan rahatsız olur:

- "Davacı haklı görünüyor ama tazminat tutarı abartılı mı?"
- "Karşı tarafa savunma hakkı tam tanındı mı? (HMK m.27)"
- "Bilirkişi raporu yeterince tarafsız mı?"
- "Süre / şekil eksiği var mı?"
- "Yargılama ekonomisi açısından ayırılabilir mi (HMK m.30)?"

Her bir hâkim şüphesi için **önleyici cevap** dilekçeye girer:

```
"Müvekkil [...] taleplerini şu somut delillerle dayanır: ...
Tazminat tutarı, [bilirkişi raporu ön analizine göre / emsal davalardaki
ortalama tazminata göre] makul oranda belirlenmiş olup, abartı içermez.
Karşı tarafa [...] tarihli ihtarname ile savunma hakkı tanınmış,
arabuluculuk süreci yürütülmüştür."
```

### 5.2 Davalı tarafın olası savunmaları

Adım 3'te tespit edilen zayıflıkları davalı kendisi kapatmaya çalışabilir. Olası savunmalar + **bizim hazır cevabımız**:

```
DAVALI SAVUNMASI 1: "Pasif husumet ehliyeti yok"
→ KARŞI CEVAP: 5651 Ek m.4/3 "malî yönden tam yetkili" hükmü açık;
İstanbul BAM 16. HD ...E ...K kararı emsâl niteliğindedir.

DAVALI SAVUNMASI 2: "DMCA bildirimi yapılmadı"
→ KARŞI CEVAP: MÖHUK m.1 uyarınca yabancı federal düzenleme Türk yargı
yetkisinde uygulanmaz; Türk hukuku ihtarname yeterli bildirim sayar
(TBK m.117 + FSEK m.68 ön bildirim şart yok).

DAVALI SAVUNMASI 3: "Eser sahipliği ispatlanmadı"
→ KARŞI CEVAP: FSEK m.11 karinesi davacı lehine; EK-3 master kayıtları,
EK-4 meslek birliği üyelik belgeleri karineyi pekiştirir.

DAVALI SAVUNMASI 4: "Tüzel kişilik perdesi"
→ KARŞI CEVAP: HMK m.124/4 terditli talep ile X Corp.'un davaya dahil
edilmesi yedek talebi sunulmuştur; TMK m.2 hakkın kötüye kullanımı.
```

### 5.3 Önleyici dilekçe yapısı

Her muhtemel savunmaya bir paragraf, dilekçenin "Karşı Tarafın Muhtemel Savunmalarına İleri Cevaplar" bölümünde **önceden** verilir. Bu, dava dilekçesinde **Sherlock yöntemiyle** karşı tarafın hamlelerini önceden gören taraf olduğunu gösterir.

---

## ADIM 6 — SHERLOCK / ŞEYTANIN AVUKATI ÜSLUBUYLA METİN ÜRETME

Şimdi yazım zamanı. Üslup:

### 6.1 Ton özellikleri

- **Bürokratik ama keskin**: "Müvekkilim, davalının ihtarnameyi yanıtsız bıraktıktan sonra dava açıldığında 'bildirim yapılmadı' iddiasını ileri sürmesinin **çelişkili davranış yasağına aykırılığını** vurgulamayı zaruri görmektedir."
- **Detektif/avukat tonunda gözlem**: "Davalının ToS'unda yer alan 'dünya çapında, geri dönülemez, telifsiz lisans' ifadesi, **kendi başına FSEK m.52 emredici hükmüne aykırı olup**, davacının davaya konu eserleri bakımından zaten **etkisizdir** — zira davacı bu sözleşmenin tarafı değildir."
- **Olguların mantıksal zinciri**: "Karşı tarafın iddiası kabul edildiği takdirde, mantıksal sonuç olarak {X} doğacaktır. Ne var ki {X} hem mevzuata hem yerleşik içtihada **doğrudan aykırı** olduğundan, karşı iddianın kendisi kabul edilemez."
- **Karşı tarafın çelişkilerini ortaya koyma**: "Davalı bir yandan {A} iddiasını ileri sürerken, diğer yandan {B} iddiasını da öne sürmekte; bu iki iddianın **bir arada doğruluğu mantıken mümkün değildir**."

### 6.2 İçtihat alıntı standardı

```
"Nitekim Yargıtay [11. Hukuk Dairesi]nin [tarih] tarih ve [E. .../...] sayılı
kararında da benimsendiği üzere: '[ilgili gerekçe pasajı]' Bu içtihat, mevcut
uyuşmazlığın koşullarıyla {A, B, C bakımından} birebir örtüşmektedir."
```

İçtihat metni `yargi_mcp.get_bedesten_document_markdown` ile alınır — özetlenmez, **doğrudan alıntı**.

### 6.3 Mevzuat alıntı standardı

```
"5846 sayılı FSEK m.X/Y açık hükmü gereğince: '[ilgili madde metni]'.
Bu hüküm, somut olayda {nasıl uygulanır}."
```

Madde metni `mevzuat_mcp.search_within_kanun` ile alınır.

### 6.4 Doktrin alıntı standardı

```
"Doktrinde [yazar adı]'nın da işaret ettiği üzere ([eser/makale adı], [yıl]):
'[ifadenin özü]'. Bu görüş yerleşik bir kabul olup..."
```

Doktrin `literatur-mcp` veya `yoktez-mcp` ile çekilir.

### 6.5 Dilekçenin standart yapısı (Sherlock toniyle)

```
İSTANBUL ... MAHKEMESİ'NE

DAVACI:        [tam bilgi]
VEKİLİ:        [varsa]
DAVALI:        [tam bilgi]
KONU:          [özetli ama keskin]
DAVA DEĞERİ:   [HMK m.107 belirsiz alacak ise belirt]
HARÇ:          [yatırılan tutar]
HUKUKÎ SEBEP:  [ana mevzuat listesi]

AÇIKLAMALARIMIZ:

I. OLAYLAR
[Kronolojik, somut, belge atıflı — chronology-builder skill çıktısı buraya gelir]

II. HUKUKÎ DEĞERLENDİRME

II.A. UYGULANACAK HUKUK
[İlgili mevzuat hükümleri — tam metin alıntılı]

II.B. LEHE İÇTİHAT
[Adım 2'den çıkan argümanlar — somut karar atıflı]

II.C. DOKTRİN
[Literatür desteği — varsa]

III. KARŞI TARAFIN MUHTEMEL SAVUNMALARINA İLERİ CEVAPLAR
[Adım 5'ten çıkan önleyici cevaplar — her birine 1 paragraf]

IV. DAVALININ KÖTÜ NİYET / USULİ HATA NOKTALARI
[Adım 3'ten çıkan zayıflıklar — TMK m.2 + HMK usul hataları]

V. İHTİYATÎ TEDBİR TALEBİ [varsa]
[Periculum in mora + fumus boni iuris açıkça]

VI. DELİLLER
[Liste — HMK m.121]

VII. HUKUKÎ SEBEPLER
[Tam liste]

VIII. NETİCE-İ TALEP
[Numaralı + spesifik talepler]

[Tarih, vekil/asıl taraf imza]
EK belge listesi
```

---

## ADIM 7 — ÇIKTI: AUDIT TRAIL + İKİ FORMAT

### 7.1 Çıktı formatları

- **Markdown** (default — okunabilir)
- **DOCX** — `docx-uretici` skill'i ile profesyonel Word çıktısı

### 7.2 Audit trail (her kararın izi)

```markdown
## Audit Trail

### Lehe içtihat (yargi_mcp)
| Karar | Tarih | Argüman | Bizim olguya uyum |
|---|---|---|---|

### Karşı zayıflıklar (TMK m.2 + usul)
| Zayıflık | Hukuki dayanak | Eylemde nasıl ortaya çıktı |
|---|---|---|

### Önleyici cevaplar (Adım 5)
| Olası savunma | Hazır karşı cevap |
|---|---|

### Doktrin (literatur-mcp + yoktez-mcp)
| Yazar/Tez | Eser | Görüş |
|---|---|---|

### MCP Çağrı Logu
| Çağrı | Sonuç sayısı |
|---|---|
```

---

## Standart Çıktı Formatı (Hukuki Memo)

Bu skill'in çıktısı **iki katmanlı** olur:

1. **Strateji Memo** (iç çalışma — sen kullanırsın)
2. **Dilekçe Taslağı** (mahkemeye gidecek metin)

```markdown
# Dava Strateji Analizi — {dava_adi}

## İç Strateji Memo
[5 adımlık analiz — Adım 2-5 detaylı]

## Mahkemeye Gidecek Dilekçe
[Adım 6 üslubuyla yazılmış tam metin]

## Audit Trail
[Yukarıdaki tablolar]

## Sonraki Adımlar
- [ ] Dilekçeyi avukat denetimine almak (varsa)
- [ ] Müvekkilin son onayı
- [ ] UYAP üzerinden gönderim
- [ ] Takvim güncellemesi (siure-hesap-motoru ile)
```

## Eskalasyon Tetikleyicileri

1. Ceza yargılaması boyutu var (TCK kapsamı) — kıdemli ceza uzmanlığı gerekir
2. AYM / AİHM yolu açık
3. Sınır ötesi (MÖHUK + yabancı yargı kararı tenfizi)
4. Çoklu taraf (HMK m.59 zorunlu / ihtiyari dava arkadaşlığı)
5. Aleyhe çıkma riski yüksek + ciddi bedel

## Notlar

- **Davayı tam anlamadan yazma**. Adım 1A asla atlanmaz.
- **Sherlock üslubu** = soğuk, kanıtlı, kestirme. Hâkimin önündeki yargıç değil, **kanıt sunan dedektif** gibi yaz.
- **Karşı tarafı küçümseme**, çelişkilerini ortaya koy — saldırgan dilden uzak dur.
- Her argüman **somut belgeyle** dayandırılır — yorum yok.
- "Yargıtay 11. HD" gibi daire numaraları **her kullanımda `yargi_mcp` ile teyit edilir**.
