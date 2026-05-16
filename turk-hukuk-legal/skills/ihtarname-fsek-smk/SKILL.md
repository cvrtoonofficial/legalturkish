---
name: ihtarname-fsek-smk
description: FSEK (5846) ve Sınai Mülkiyet Kanunu (6769) kapsamında tecavüz, ihlal veya hak gaspı durumunda gönderilecek noter ihtarnamesini hazırlar. Marka, patent, faydalı model, tasarım, coğrafi işaret tecavüzü; eser sahipliği ihlali; bağlantılı haklar; haksız rekabet (TTK m.54-63) ile bağlantılı durumlar dahil. Yalnızca taslak hazırlar; gönderim için baroya kayıtlı avukat onayı şarttır. Gönderim (noter, KEP, iadeli taahhütlü posta) yapılmaz.> **Mevzuat referansları çalışma anında doğrulanır.** Bu skill içinde geçen FSEK ve SMK madde numaraları iskelet niteliğindedir; her ihtarname taslağı oluşturulurken `mevzuat_mcp.search_within_kanun` ile güncel metne erişilmelidir.

## Davet

```
/fikri-sinai-haklar:ihtarname-fsek-smk
```

İhtarname konusunu (tecavüz türü) ve hak sahibinin pozisyonunu (saldıran/savunan) sorar.

## İş Akışı

### Adım 1 — Senaryo Tipini Belirle

Aşağıdaki tablodaki ihtarname tiplerinden birini seç. Yanlış tip, dava sürecinde **kanıt değeri ve süre** açısından sorun çıkarır.

| # | Senaryo | Hukuki temel | Talep tipi |
|---|---|---|---|
| 1 | Marka tecavüzü (tescilli marka) | SMK m.7, 29 (haklar ve tecavüz halleri); m.149 (talepler) | Tecavüzün durdurulması, men, ref, tazminat, hükümsüzlük |
| 2 | Patent / faydalı model tecavüzü | SMK m.85 (haklar) ve m.141 (tecavüz halleri); m.149 (talepler) | Tecavüzün önlenmesi, men, tazminat |
| 3 | Tasarım tecavüzü | SMK m.59 (tescilli tasarım hakkı), m.81 (tecavüz halleri); m.149 | Tecavüzün önlenmesi, men, tazminat |
| 4 | Coğrafi işaret ihlali | SMK m.44-45 (kullanım), m.53 (tecavüz halleri) | Men, ref |
| 5 | FSEK — Mali hak tecavüzü | FSEK m.21-25 (mali haklar), m.66-68 (tecavüzün önlenmesi, ref, tazminat — üç kat rayiç bedel) | Men + üç kat tazminat |
| 6 | FSEK — Manevi hak tecavüzü | FSEK m.14-17 (manevi haklar), m.67 (manevi haklara tecavüz) | Tecavüzün önlenmesi, manevi tazminat |
| 7 | FSEK — Bağlantılı haklar (icracı, yapımcı, yayın) | FSEK m.80 | Mali/manevi haklara tecavüze paralel |
| 8 | Yazılım telif ihlali | FSEK m.2/1 (bilgisayar programları eser), m.38 (kişisel kullanım istisnasının sınırı) | Mali hak tecavüzü |
| 9 | Haksız rekabet (markasız ürün taklidi, slogan kopyası) | TTK m.54-63 (haksız rekabet) | Men, ref, tazminat |
| 10 | Domain / alan adı uyuşmazlığı | SMK + TBK genel hükümler + İBM Marka kullanımı | Devir, men |

**Çok katmanlı senaryo:** Bazı vakalar birden fazla temele dayanır (örn. tescilli marka + haksız rekabet + FSEK ambalaj eseri). Her temeli ayrı paragrafta işle.

### Adım 2 — Mevzuat Metnini Doğrula

Her senaryo için ilgili madde metnine erişin:

```
mevzuat_mcp.search_within_kanun(
  mevzuat_no="6769",  # SMK
  keyword="marka tecavüzü"
)
mevzuat_mcp.search_within_kanun(
  mevzuat_no="5846",  # FSEK
  keyword="mali hak"
)
```

**Önemli:** Mevzuatta değişiklik olabilir. Çekilen metni avukata göster, doğrulamadan ihtarnameye koyma. Eğer `mevzuat_mcp` erişilemezse, taslakta madde numarası yerine `[FSEK m.XX — avukat tarafından doğrulanacak]` ifadesi kullan.

### Adım 3 — İçtihat Tara (Opsiyonel ama Şiddetle Önerilir)

```
yargi_mcp.search("FSEK 68 üç kat rayiç bedel Yargıtay 11. Hukuk Dairesi")
yargi_mcp.search("SMK 149 marka tecavüzü tazminat hesabı")
```

İhtarnamede içtihada doğrudan atıf zorunlu değildir, ancak **tazminat hesap yöntemi** ve **rayiç bedel** konularında karşı tarafa pazarlık zemini hazırlar.

### Adım 4 — Hak Sahipliği Doğrulamasını İste

Müvekkilden aşağıdakileri talep et — bunlar olmadan ihtarname **zayıf** kalır:

- **Marka:** TPMK tescil belgesi + tescil tarihi + sınıf(lar) + yenileme durumu
- **Patent/faydalı model/tasarım:** Tescil belgesi + ilan tarihi + koruma süresinin durumu
- **FSEK eseri:** Yaratım tarihi (öncelik için), kayıt (gerekirse — FSEK m.13 bandrol vb.), eser örneği, hak sahipliği zincirinin belgesi (devir sözleşmeleri)
- **Bağlantılı haklar:** Yapım/yayın tarihi, icra kaydı
- **Haksız rekabet:** Önceye dayalı kullanım kanıtı, pazardaki yeri, ticari iz

### Adım 5 — Tecavüz Eyleminin Delilini Topla

| Tecavüz tipi | Delil önerileri |
|---|---|
| Online ürün satışı | Sayfanın URL'i, **noter aracılığıyla web sayfası tespiti** (Noterlik K. m.60), arşiv linkleri (archive.org) |
| Fiziksel ürün | Numune satın alımı + fatura (alıcı kimliği gizli olabilir), bilirkişi tespiti |
| Yayın | Kayıt + tarih damgası, ekran kayıtları, kanal/platform bilgisi |
| Marka kullanımı (sosyal medya) | Profil URL, gönderi URL, takipçi sayısı |
| Yazılım | Kaynak kod karşılaştırması, dökümantasyon benzerliği |

**Not:** Mahkemeye gidilecekse `delil tespiti (HMK m.400)` veya `ihtiyati tedbir (HMK m.389+ ve SMK m.159, FSEK m.77)` daha güçlü bir delil yöntemidir. İhtarname öncesi delil tespiti yapılmışsa belirt.

### Adım 6 — Saldırganlık Tonunu Belirle

`CLAUDE.md` profilindeki ton tercihine göre:

- **Standart (aggressive):** 14 gün süre, doğrudan men + tazminat talebi, dava ihtarı, mahkeme masrafları yansıtma.
- **Ölçülü (measured):** 30 gün süre, men + uzlaşma daveti, talep edilen düzeltme/kaldırma listesi.
- **Muhafazakâr (conservative):** Görüşme talebi, müzakere kapısı açık, dava ihtarı en sona.

Karşı taraf **iyi niyetli** bir lisans pazarlığında ise muhafazakâr ton uzlaşma şansını korur; **kötü niyetli kopyacı** ise standart ton tercih edilir.

### Adım 7 — İhtarname Yapısı (Noter Onaylı)

```
[BÜRO ANTETİ]

KONU: [Markanın/Eserin/Patentin] adına yapılan tecavüzün ihtaren önlenmesi talebidir.

MUHATAP:
Ad/Unvan: ...
Adres (KEP varsa öncelikli): ...
Vergi/T.C. No: ... (biliniyorsa)

İHTAR EDEN:
... (hak sahibinin tam bilgileri)
Vekili: Av. ...

İHTAR METNİ:

1. HAK SAHİPLİĞİ
Müvekkilim, [TPMK nezdinde 20XX/XXXXX numara ile tescilli "..." markasının / 5846 sayılı FSEK kapsamında "..." adlı eserin / vb.] hak sahibidir. [Belge ekleri 1, 2.]

2. TECAVÜZ EYLEMİ
... tarihinde, ... adresinde / ... URL'sinde tarafınızca [tecavüz eyleminin tarif edilmesi]. Bu eylem, [SMK m.29/2-X, m.149 / FSEK m.21, m.66] uyarınca müvekkilin hakkına tecavüz teşkil etmektedir.

3. TALEPLERİMİZ
İşbu ihtarnamenin tarafınıza tebliğinden itibaren [14 / 30] gün içinde:

a) Tecavüz eyleminin DERHAL DURDURULMASINI,
b) Mevcut [ürünlerin / içeriğin / kopyaların] piyasadan çekilmesini, sosyal medya hesaplarından kaldırılmasını,
c) [SMK m.149/d veya FSEK m.68 uyarınca] tazminat olarak ... TL'nin ödenmesini (FSEK 68 hâli için: rayiç bedelin üç katı talep edilmektedir),
d) İlerideki tecavüzlerden kaçınılacağına dair yazılı taahhüt verilmesini

TALEP VE İHTAR EDERİZ.

4. SONUÇ
Süresi içinde taleplere uyulmaması halinde:
- SMK m.149 / FSEK m.66 vd. uyarınca tecavüzün önlenmesi, durdurulması ve giderilmesi davası,
- SMK m.159 / FSEK m.77 uyarınca ihtiyati tedbir,
- SMK m.150 / FSEK m.68 uyarınca tazminat davası,
- TCK m.155 (güveni kötüye kullanma) ve FSEK m.71-72 (cezai sorumluluk) yönünden suç duyurusu

dahil olmak üzere yasal yollara müracaat hakkımız saklıdır.

Vekâleten,
Av. [Ad Soyad]
Baro Sicil No: ...
Tarih: ...
```

### Adım 8 — Eskalasyon Kontrolü

Aşağıdaki durumlar varsa **şablon ihtarname KULLANMA**, ilk derece uzman avukat denetimi şart:

- **Marka açısından:** Tanınmış marka iddiası (SMK m.6/4, m.6/5; özel koruma), kötü niyetli tescil iddiası (m.6/9), önceki kullanım hakkı çakışması (m.6/3)
- **Patent açısından:** Hükümsüzlük itirazıyla iç içe geçen tecavüz (paralel ihtilaf riski), zorunlu lisans iddiası (SMK m.129–137)
- **FSEK açısından:** İşlenme eseri iddiası (FSEK m.6), eser sahipliği uyuşmazlığı (m.8, m.10), meslek birliği yetkisi içeren konu (FSEK m.42 vd.)
- **Genel:** Karşı taraf bir kamu kurumu / üniversite / radyo-TV yayıncısı; sınır ötesi tecavüz (uluslararası özel hukuk devreye girer); şüpheli ceza boyutu (TCK 158/h, 244, vb. — bilişim suçları)

Eskalasyon işaretlenirse Claude **taslak ihtarnameyi üretmez**, yerine `## ESKALASYON UYARISI` raporu üretir.

### Adım 9 — Gönderim Yöntemini Öner

| Yöntem | Avantaj | Dezavantaj | Önerilen |
|---|---|---|---|
| **Noter ihtarnamesi** (Noterlik K. m.91) | Resmî tebliğ, kanıt değeri yüksek, içtihat şart koşmaz ama mahkeme genelde bekler | Maliyetli, 1-2 hafta tebliğ süresi | Klasik IP davalarında |
| **KEP** | Hızlı, ucuz; 6102 TTK m.18/3 ve 6100 HMK uyarınca geçerli tebliğ | Karşı tarafın KEP'i olmalı | Şirketler arası (zorunlu KEP'liler) |
| **İadeli taahhütlü posta** | Ucuz | Tebliğ ispat zayıf, mahkeme yeterli görmeyebilir | İhtiyaten, ana yola ek olarak |
| **E-posta + KEP kombosu** | Hızlı + ispat | Sadece e-posta yetersiz | Süre hassasiyeti yüksekse |

### Adım 10 — Çıktı

```markdown
## İhtarname Taslağı — [Tecavüz Tipi]

**Gönderim yöntemi:** [Noter / KEP / vb.]
**Tebligat adresi doğrulandı mı?** [Evet / Hayır]
**Hak sahipliği belgeleri ekli mi?** [Liste]
**Delil ekleri:** [Liste]
version: 0.2.0
last_legal_review: 2026-05-16
required_mcps:
  - mevzuat_mcp
  - yargi_mcp
optional_mcps:
  - hukuk-rag
applicable_laws:
  - 5846
  - 6769
  - 6098
  - 1136
---

[İhtarname metni — yukarıdaki şablona göre]

---

### Eskalasyon kontrolü
[Tetikleyici tespit edilmedi / Şu tetikleyiciler tespit edildi: ...]

### Mevzuat doğrulaması
- [FSEK m.XX] mevzuat_mcp ile [doğrulandı / doğrulanmadı — manuel teyit gerek]
- [SMK m.XX] mevzuat_mcp ile [doğrulandı / doğrulanmadı]

### İçtihat referansları (yargi_mcp)
- ...
- ...

### Sonraki adımlar
1. Avukat denetimi
2. Müvekkil onayı
3. Noter / KEP sevki
4. [Eğer ön delil tespiti gerekiyorsa] HMK m.400 başvurusu
5. Süre takvimine ekle: cevap için son tarih, ihtiyati tedbir başvurusu için son tarih
```

## Süre Disiplini (Kritik)

Aşağıdaki süreler ihtarname taslağıyla birlikte takvime girmeli:

- **İhtarnameye cevap için verilen süre** (genelde 14 / 30 gün)
- **Hak düşürücü süreler:**
  - SMK m.157: marka hükümsüzlük davasında 5 yıl sessiz kalma (bu davacının değil, hak düşürücüdür)
  - FSEK m.66 — tecavüzün önlenmesi davası için zamanaşımı (TBK m.72 — haksız fiil zamanaşımına atıf, 2/10 yıl)
- **İhtiyati tedbir kararı sonrası dava açma süresi:** HMK m.397 (2 hafta)

> **Her sayısal süre `mevzuat_mcp` ile yeniden doğrulanmalıdır.**

## Sık Hatalar

1. **Yetersiz hak sahipliği belgesi** — TPMK tescil belgesinin yenileme tarihini kontrol etmemek
2. **FSEK 68 üç kat tazminat** — Bunu sadece **kasıtlı veya ağır ihmalli** tecavüzde talep etmek (yargısal değerlendirme; Yargıtay 11. HD kararlarıyla)
3. **Hükümsüzlük davası ile birleşmiş tecavüz** — İhtarname öncesi karşı tarafın hükümsüzlük açma ihtimalini değerlendirmemek; **paralel dava riski**
4. **Yetkili mahkeme** — Fikri ve sınai haklar **hukuk** mahkemeleri yoktur her ilçede; ihtisas mahkemeleri sınırlı (Ankara, İstanbul, İzmir vd.). Yetkili mahkemeyi `mevzuat_mcp` + ilgili HSK kararıyla teyit et.
5. **Manevi tazminat** — FSEK m.67 manevi haklara tecavüzde manevi tazminat ayrı kalem; karıştırılmamalı

## Şablon Yönetimi

Büro standart şablonlarını `CLAUDE.md` veya ayrı `templates/` klasöründe sakla. Şablon her kullanıldığında:
1. Mevzuat numaralarını `mevzuat_mcp` ile doğrula
2. Karşı taraf tipine göre tonu uyarla
3. Müvekkil onay kutusunu çıktıya ekle

## Kaynak ve İlgili Skill'ler

- `/fikri-sinai-haklar:tecavuz-triyaj` — ihtarname göndermeye değer mi?
- `/fikri-sinai-haklar:icerik-kaldirma-bildirim` — online ihlal için 5651 + FSEK uyar-kaldır
- `/dava-uyusmazlik:dilekce-ihtarname` — ihtarname genel şablonlar (FSEK/SMK dışı)

## Disclaimer

Bu skill çıktısı **hukuki görüş değildir**. Avukat denetiminden geçmemiş ihtarname tebliğ edilmez. Mevzuat numaraları ve içtihat referansları her kullanımda yeniden doğrulanmalıdır.


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

