---
name: dilekce-ihtarname
description: HMK (6100) uyumlu dava dilekçesi (m.119), cevap dilekçesi (m.129), replik/düplik (m.136), karşı dava (m.132), istinaf (m.342), temyiz (m.364) dilekçelerini ve TBK temerrüt ihtarnamesi, kira ihtarnamesi, iş akdi fesih ihtarnamesi gibi şekil sıkı ihtarnameleri hazırlar. Profesyonel hukukçuya yönelik bürokratik dil; mevzuat ve içtihat referansları mevzuat_mcp + yargi_mcp ile çalışma anında doğrulanır.
---

# /dava-uyusmazlik:dilekce-ihtarname — HMK Uyumlu Dilekçe ve İhtarname Yazımı

> **Mevzuat metni her kullanımda doğrulanır.** Bu skill, içerdiği HMK ve TBK madde referanslarını sadece **iskelet** olarak kullanır; gerçek metin `mevzuat_mcp.search_within_kanun(mevzuat_no="6100", keyword="...")` ile çekilir.

## Davet

```
/dava-uyusmazlik:dilekce-ihtarname [tip]
```

Tipler:
- `dava` — dava dilekçesi (HMK m.119)
- `cevap` — cevap dilekçesi (HMK m.129)
- `karsi-dava` — karşı dava (HMK m.132)
- `replik` — cevaba cevap (HMK m.136)
- `duplik` — ikinci cevap (HMK m.136)
- `istinaf` — istinaf dilekçesi (HMK m.342)
- `temyiz` — temyiz dilekçesi (HMK m.364)
- `iddaa-yenileme` — iddianın ve savunmanın genişletilmesi (m.141)
- `ihtiyati-tedbir` — HMK m.389+
- `delil-tespiti` — HMK m.400
- `bilirkisi-itiraz` — bilirkişi raporuna itiraz
- `ihtarname-temerrut` — TBK m.117 temerrüt ihtarnamesi
- `ihtarname-kira` — TBK kira ödeme/tahliye ihtarnamesi
- `ihtarname-is-akdi` — İş K. m.18-21 fesih ihtarnamesi
- `ihtarname-genel` — TBK m.131+ (cayma, fesih, vb.)

## Genel İş Akışı

### Adım 0 — Profil Kontrolü
`/dava-uyusmazlik:soguk-baslangic-mulakat` çalıştırılmış mı? Çalışmamışsa generic çıktı uyarısı ver.

### Adım 1 — Tip & Tarafları Belirle
- Dilekçe tipi (yukarıdaki listeden)
- Davacı / davalı / dava dışı taraflar
- Yetkili mahkeme — ihtisas dairesi var mı? (Fikri ve Sınai Haklar HM, İş Mahkemesi, Aile Mahkemesi, Tüketici Mahkemesi, vb.)
- Görevli mahkeme (HMK m.2-4, miktar/değer ölçütü)
- Yargı yeri (HMK m.5-19 yetki kuralları)

### Adım 2 — Vakıa Topla
- Olay anlatımı kronolojik
- Tarihler net (zamanaşımı kontrolü)
- Taraflar arası ilişki belgeleri
- Önceki yazışmalar
- Müvekkil notları

### Adım 3 — Hukuki Sebep Seçimi
Dava konusunun hangi maddi hukuk normuna dayandığı:
- TBK (sözleşme, haksız fiil, vekâletsiz iş görme, sebepsiz zenginleşme)
- TTK (ticari işlemler, şirketler, kıymetli evrak, deniz ticareti, sigorta)
- TKHK (tüketici)
- İş K. (işçi-işveren)
- FSEK / SMK (fikri-sınai)
- TMK (medeni, aile, miras, eşya)
- İYUK (idari)
- Diğer özel mevzuat

> Hukuki sebep `mevzuat_mcp` ile doğrulanmalı.

### Adım 4 — Talep Sonuç Formüle Et
HMK m.119/1-(g): "Talep sonucu" net, terditli olabilir (örn. asıl/öncelik talep + yedek talep).

Tipik talepler:
- Tespit
- Eda (ifaya zorlama, men, kaldırma, tazminat)
- İnşai (sözleşmeyi sona erdirme, hükümsüzlük tespiti)

### Adım 5 — Delil Listesi (HMK m.121)
Davanın açılışında her delil **özellikleriyle birlikte** gösterilmeli:
- Belge / senet / fatura
- Tanık (ad, adres, anlatacağı konu)
- Bilirkişi (talep gerekçesi)
- Yemin (HMK m.225-239)
- Keşif (m.288)
- Tarafların isticvabı

> **Önemli:** HMK m.119 ile dilekçeyle sunulmayan deliller, ön inceleme aşamasına kadar **iddianın değiştirilmesi yasağı** çerçevesinde sınırlı eklenebilir (m.141).

## Şablonlar

### 1. Dava Dilekçesi (HMK m.119)

```
... MAHKEMESİ'NE
                                                    [Yer]

DAVACI            : [Tam ad, T.C./Vergi no, adres, KEP]
VEKİLİ            : Av. [Ad], Baro Sicil No: ..., adres, KEP
DAVALI            : [Tam ad, ... bilinen tüm bilgiler]
KONUSU            : [Kısa konu özeti — örn. "Tazminat talebi"]
DAVANIN DEĞERİ    : ... TL (belirsiz alacak davası ise HMK m.107)
HARÇ TUTARI       : ... TL (Harçlar Kanunu üzerinden)
HUKUKÎ SEBEP      : TBK m.XX, TTK m.XX, vb.

AÇIKLAMALAR:

1. OLAY
[Vakıanın kronolojik anlatımı; her tarih ve belge ek numarasıyla]

2. HUKUKÎ DEĞERLENDİRME
[Olayın hukuki nitelendirilmesi; ilgili madde metni ve içtihat atıfları]

3. ZAMANAŞIMI
[Talep zamanaşımına uğramamıştır; gerekçesiyle]

DELİLLER:
1. ... (Ek-1)
2. Tanık: ... (HMK m.240)
3. Bilirkişi raporu talebi
4. Karşı tarafın ticari defterleri (HMK m.222)
5. Yemin hakkı saklıdır

HUKUKÎ SEBEPLER: TBK, TTK, HMK ve ilgili mevzuat

TALEP SONUCU:
Yukarıda açıklanan sebeplerle:
a) ... TL'nin dava tarihinden itibaren işleyecek yasal faizi ile birlikte davalıdan tahsiline,
b) Yargılama giderleri ve vekâlet ücretinin davalıya yükletilmesine,
karar verilmesini saygıyla arz ve talep ederim.

                                                    [Tarih]
                                                    Davacı Vekili
                                                    Av. [Ad Soyad]
EKLER:
1. Vekâletname
2. ... (delil belgeleri)
```

### 2. Cevap Dilekçesi (HMK m.129)

```
... MAHKEMESİ'NİN ... E. SAYILI DOSYASINA SUNULMAK ÜZERE
... MAHKEMESİ'NE

DOSYA NO          : 20XX/XXXX E.
CEVAP VEREN
(DAVALI)         : ...
VEKİLİ            : Av. ...
DAVACI            : ...
KONUSU            : Davaya cevaplarımızın sunulmasıdır.
TEBLİĞ TARİHİ     : ... (cevap süresinin başlangıcı; HMK m.127 — 2 hafta)

CEVAPLARIMIZ:

1. USUL İTİRAZLARI
a) Görev itirazı: [Varsa]
b) Yetki itirazı: [Varsa]
c) Derdestlik / kesin hüküm itirazı: [Varsa]
d) Husumet itirazı: [Varsa]
e) Dava şartlarına ilişkin diğer itirazlar (HMK m.114-115)

2. ESASA İLİŞKİN CEVAPLARIMIZ
[Davacının iddialarına madde madde cevap]

3. KARŞI VAKIALAR
[Davalı tarafından ileri sürülen olgular]

4. ZAMANAŞIMI / HAK DÜŞÜRÜCÜ SÜRE [varsa]
[İtirazı]

DELİLLER:
1. ...
2. Karşı taraf delillerine itirazlarımız (...)

HUKUKÎ SEBEPLER: HMK, TBK, ve ilgili mevzuat

TALEP SONUCU:
a) Öncelikle usul itirazlarımızın kabulü ile davanın USULDEN REDDİNE,
b) Aksi takdirde davanın ESASTAN REDDİNE,
c) Yargılama giderleri ve vekâlet ücretinin davacıya yükletilmesine,
karar verilmesini saygıyla arz ve talep ederim.

                                                    [Tarih]
                                                    Davalı Vekili
                                                    Av. ...
```

### 3. İstinaf Dilekçesi (HMK m.342)

İstinaf yoluna başvuru, ilk derece mahkemesinin kararı taraflara tebliğden itibaren **2 hafta** içinde yapılır (HMK m.345 — `mevzuat_mcp` ile doğrula).

```
... BÖLGE ADLİYE MAHKEMESİ İLGİLİ HUKUK DAİRESİNE
GÖNDERİLMEK ÜZERE
... MAHKEMESİ'NE

DOSYA NO          : 20XX/XXXX E. — 20XX/XXXX K.
İSTİNAF EDEN     : ...
VEKİLİ            : Av. ...
KARŞI TARAF       : ...
KARAR TARİHİ      : ...
TEBLİĞ TARİHİ     : ... (istinaf süresinin başlangıcı)

İSTİNAF NEDENLERİ:

1. USULE AYKIRILIKLAR (HMK m.353/1-a kapsamında)
[Davanın esasına etkili usul hataları — örn. duruşma günü tebliğsizliği, görev/yetki hatası, delillere yanlış değer verme]

2. ESASA AYKIRILIKLAR (HMK m.353/1-b kapsamında)
[Maddî hukuk uygulanmasındaki hata — yanlış madde, eksik araştırma, yanlış yorumlama, bilirkişi raporuna aykırı karar]

3. EKSİK İNCELEME / ARAŞTIRMA
[Mahkemenin sormadığı veya almadığı deliller]

TALEP SONUCU:
a) ... Mahkemesinin 20XX/XXXX E., 20XX/XXXX K. sayılı kararının BOZULMASINA / KALDIRILMASINA,
b) Davanın esastan kabulüne (veya yeniden görülmek üzere mahkemesine gönderilmesine),
c) Yargılama giderleri ve vekâlet ücreti yönünden ...
karar verilmesini saygıyla arz ve talep ederim.

                                                    [Tarih]
                                                    İstinaf Eden Vekili
                                                    Av. ...
```

### 4. Temerrüt İhtarnamesi (TBK m.117)

```
İHTARNAME

İHTAR EDEN     : ... (alacaklı)
VEKİLİ          : Av. ...
MUHATAP         : ... (borçlu)

KONU            : ... TL alacağın TBK m.117 uyarınca temerrüde düşürülerek ödenmesinin ihtaren talebi.

İHTAR METNİ:

1. ALACAĞIN DAYANAĞI
[Sözleşme tarih ve içeriği; fatura, sevk irsaliyesi; teslim/ifa tarihi]

2. MUACCELLİYET
... tarihinde muaccel hale gelen ... TL tutarındaki alacak, tarafınızca ödenmemiştir.

3. TALEP
İşbu ihtarnamenin tarafınıza tebliğinden itibaren 7 (yedi) gün içinde:
a) Anapara ... TL,
b) Temerrüt faizi (TBK m.120 — yıllık ticari işlerde avans faiz oranı, diğer hallerde yasal faiz),
c) Vekâlet ücreti ve masraflar
toplamı .... TL'nin tarafımıza ödenmesini ihtar ederiz.

4. SONUÇ
Süresi içinde ödeme yapılmaması halinde aleyhinize:
- İcra takibi başlatılacak,
- Tüm yasal yollara müracaat edilecek,
- Doğacak tüm masraf, vekâlet ücreti ve faizler tarafınıza yükletilecektir.

Saygılarımızla.

                                                    [Tarih]
                                                    Vekili
                                                    Av. ...
```

### 5. Kira İhtarnamesi (TBK kira hükümleri)

```
İHTARNAME

KİRAYA VEREN   : ...
VEKİLİ          : Av. ...
KİRACI          : ...

KONU            : ... aylarına ait toplam ... TL kira bedelinin ödenmesi ile ödenmemesi halinde sözleşmenin feshi ve tahliye talebi.

[TBK kira hükümleri — m.315 ve devamı kira bedelinin ödenmemesi temerrüdü için ihtarda bulunma şartı düzenler. Madde metni `mevzuat_mcp.search_within_kanun(mevzuat_no="6098", keyword="kira temerrüt")` ile doğrulanmalıdır. Konut/çatılı işyeri kirası için ek koruma hükümleri vardır.]

[Şablon yapısı temerrüt ihtarnamesiyle benzer; ek olarak fesih ve tahliye ihtarı]
```

### 6. İş Akdi Fesih İhtarnamesi (İş K. 4857 m.18-19)

```
İHTARNAME / SAVUNMA TALEBİ

İŞVEREN         : ...
İŞÇİ            : ...

KONU            : 4857 sayılı İş Kanunu m.19 uyarınca savunma talebi / fesih bildirimi.

[İş K. m.18: geçerli sebep; m.19: yazılı bildirim ve savunma alma şartları. İşten çıkarmadan önce savunma alınmaması fesih sebebini sakatlayıcıdır.]

[İçerik yargılaması Yargıtay 9. ve 22. HD'nin yerleşik içtihatlarıyla şekillenir — `yargi_mcp.search("iş akdi fesih savunma yazılı bildirim m.19")`. Daire numaraları her kullanımda doğrulanmalıdır.]
```

## Kritik Noktalar

### Süreler
HMK ve özel mevzuat süreleri **hak düşürücü** veya **zamanaşımı** niteliğindedir. Her dilekçenin başında ilgili süre kontrol edilmeli:

| Dilekçe | Süre | Mevzuat |
|---|---|---|
| Cevap dilekçesi | 2 hafta | HMK m.127 |
| Replik | 2 hafta (HMK m.136 sürelerini doğrula) | HMK m.136 |
| İstinaf | 2 hafta (tebliğden) | HMK m.345 (doğrulanacak) |
| Temyiz | 2 hafta (tebliğden) — istinafın kesinleşmesinden değil | HMK m.366 |
| İhtiyati tedbir karşı dava | HMK m.397 — 2 hafta tedbir kararından sonra | |
| Bilirkişi raporuna itiraz | Raporun tebliğinden 2 hafta | HMK m.281 |

> **Süre tablosu her kullanımda `mevzuat_mcp` ile doğrulanmalıdır.**

### İddianın & Savunmanın Genişletilmesi Yasağı
HMK m.141: Ön inceleme aşamasından sonra **karşı tarafın açık muvafakati** olmaksızın iddia ve savunma genişletilemez. Replik ve düplikte yeni iddia ileri sürmek bu yasakla sınırlıdır.

### Belirsiz Alacak Davası (HMK m.107)
Alacak miktarı tam belirlenemiyorsa belirsiz alacak davası açılır. Sonra harca esas tutar artırılabilir.

### Tedbir & Delil Tespiti
- **İhtiyati tedbir (HMK m.389+):** Acil ihtilaflarda esas davadan önce de istenebilir; teminat şartı ve 2 haftalık dava açma süresi (m.397)
- **Delil tespiti (HMK m.400):** Belirli bir delilin **sonradan kaybolma riskine karşı** tespiti; dava açılmadan da istenebilir

### Sık Hatalar
1. **Yetki itirazı zamanı** — HMK m.116/1-a: cevap süresinde + kesin yetki dışında. Sonraki aşamada ileri sürülemez.
2. **Yenileme dilekçesi süresi** — HMK m.150 dosyanın işlemden kaldırılması ve yenileme
3. **Vekâlet ücreti** — AAÜT (Avukatlık Asgari Ücret Tarifesi) bağlayıcı asgaridir, üzerinde sözleşme yapılabilir
4. **Harç eksikliği** — yatırılmayan harç davanın açılmamış sayılması sonucunu doğurur; ön inceleme aşamasında tamamlatılır

## Çıktı

```markdown
## Dilekçe Taslağı — [Tip]

**Mahkeme:** [...]
**Dosya no:** [...]
**Süre durumu:** [Süresinde / Riskli — N gün kaldı]
**Hukuki sebep:** [...]

---

[Dilekçe gövdesi — yukarıdaki şablonlardan ilgili olan]

---

### Süre kontrol listesi
- [ ] Cevap süresi (HMK m.127)
- [ ] Delil sunum süresi (m.121)
- [ ] Vekâletname
- [ ] Harç hesabı

### Mevzuat doğrulaması
- HMK m.X: [mevzuat_mcp ile doğrulanma durumu]
- TBK m.X: [...]

### İçtihat referansları (varsa)
- [yargi_mcp sonuçları]

### Ekler kontrol listesi
- [ ] Vekâletname
- [ ] Delil ekleri
- [ ] Onaylı suretler

### Sonraki adım
1. Avukat denetimi (zorunlu)
2. UYAP'a yükleme
3. Süre takvimi güncelle
```

## Disclaimer

Bu skill **hukuki görüş değildir**. HMK, TBK ve özel mevzuat dinamiktir; her kullanımda mevzuat ve içtihat doğrulanmalıdır. Süreler hak düşürücü ya da zamanaşımı olup gözden kaçırılması müvekkilin hak kaybına yol açar.
