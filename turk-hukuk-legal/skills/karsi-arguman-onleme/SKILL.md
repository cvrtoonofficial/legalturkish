---
name: karsi-arguman-onleme
description: Mahkemeye veya karşı tarafa sunulacak metni göndermeden ÖNCE, hâkimin sorabileceği şüpheler ve davalı tarafın öne sürebileceği savunmaları sistematik olarak öngörür. Her olası karşı argümana metnin içinde önleyici cevap yerleştirir. Sherlock yönteminin "10 adım önde düşünme" boyutunu uygular. dava-strateji-analiz ile entegre çalışır; ayrıca sözleşme müzakerelerinde, ihtarname yazımında ve duruşma savunma hazırlığında bağımsız çağrılabilir.
version: 0.4.0
last_legal_review: 2026-05-16
required_mcps:
  - mevzuat_mcp
  - yargi_mcp
optional_mcps:
  - hukuk-rag
  - literatur-mcp
applicable_laws:
  - 6100
  - 6098
---

# /turk-hukuk-legal:karsi-arguman-onleme — Karşı Argüman Öngörme

> "Yazdığını okuyacak olan hâkim ve davalının zihninde **gelmeden önce** olası karşı argümanları öngör, onları metinin içinde **önceden** çürüt." Sherlock'un altın kuralı.

## Adım 0 — Zorunlu MCP Çağrıları

### 0.1 Profil okuma

### 0.2 Mevzuat & İçtihat
- HMK m.119 (dava dilekçesi), m.129 (cevap dilekçesi), m.136 (replik/düplik)
- TBK m.27 (kesin hükümsüzlük) — sözleşme tartışmalarında
- TMK m.2 (hakkın kötüye kullanılması) — karşı tarafın çelişkili davranışı için

---

## İş Akışı

### Adım 1 — Girişi Al

Skill bir aşağıdakilerden biri olarak çağrılabilir:

| Tip | Girdi | Çıktı |
|---|---|---|
| Dilekçe gözden geçirme | Hazırlanan dilekçe taslağı | Eklenecek "önleyici cevap" paragrafları |
| Sözleşme müzakeresi | Müzakere pozisyonumuz | Karşı tarafın olası geri çevirmesi + cevabı |
| İhtarname öncesi | İhtarname taslağı | Karşı tarafın yanıtında ne diyeceği + cevabımız |
| Duruşma savunması | Beyan / savunma | Hâkim/karşı vekilin olası soruları + cevap |

### Adım 2 — Hâkimin Bakış Açısı

Hâkimin tipik düşünce örüntüleri:

#### Şüphe 1: "Bu talep gerçekten dayanıyor mu?"
- Tazminat tutarı abartılı mı?
- Tanık ifadeleri tarafsız mı?
- Bilirkişi raporu güvenilir mi?

**Önleyici cevap:** Talebin temellerini **kanıtlı ve oranlı** sun — emsâl tutarlara atıf, hesap detayı.

#### Şüphe 2: "Usul / şekil eksik mi?"
- Süre dolmuş mu?
- Görevli/yetkili mahkeme mi?
- Vekâletname tam mı?
- Harç yatırılmış mı?

**Önleyici cevap:** İlk paragrafta **usul kontrolünü** açıkça yap. "İşbu dava, X tarihli kararın tebliğinden itibaren 2 hafta içinde (HMK m.345) açılmıştır."

#### Şüphe 3: "Karşı tarafa savunma hakkı tam mı?"
- İhtarname gönderildi mi?
- Arabuluculuk denenedi mi (zorunluysa)?
- Karşı tarafa süre tanındı mı?

**Önleyici cevap:** Önceki yazışmaları ve arabuluculuk sürecini kronolojide net ortaya koy.

#### Şüphe 4: "Yargılama ekonomisi açısından bölünmeli mi?"
- HMK m.30 ekonomi ilkesi
- Ayrı dava açılabilir mi?

**Önleyici cevap:** Bütüncül dava avantajını vurgula — taraflar, deliller, vakıalar aynı.

#### Şüphe 5: "Talep tipi doğru mu?"
- Tespit mi eda mı inşai mi karışmış?
- HMK m.106 talep türleri net mi?

**Önleyici cevap:** Talep sonucunda her bir kalemi numaralı + spesifik ifade et.

---

### Adım 3 — Davalı Tarafın Bakış Açısı

Davalının tipik savunma örüntüleri:

#### Savunma 1: Usul itirazları (HMK m.116)
- Görev itirazı
- Yetki itirazı
- Husumet itirazı
- Derdestlik / kesin hüküm
- Zamanaşımı / hak düşürücü süre

**Önleyici cevap:** Görevli/yetkili mahkeme açıkça gerekçelendirilmiş; husumet doğrudan davalıya yöneltilmiş gerekçesi açıklanmış.

#### Savunma 2: Esasa ilişkin reddiyeler
- "Olayların böyle gerçekleşmediği"
- "Müvekkilin haklı olmadığı"
- "Karşı kusur"
- "İrade fesadı"

**Önleyici cevap:** Her olgu için **belge atfı**; karşı kusur iddiasının çürütülmesi için tanık + somut delil.

#### Savunma 3: Mevzuat yorumu farklılıkları
- "X madde başka türlü yorumlanmalı"
- "İlgili içtihat aksine"

**Önleyici cevap:** En güçlü içtihatların önceden alıntılanması; çelişen yorumun zayıflığı gerekçelendirilir.

#### Savunma 4: Kötü niyet karşı saldırı
- "Davacı kötü niyetli" (haksız aldatma)
- "Davacı zarar görmedi"
- "Hak kaybı (sessiz kalma)"

**Önleyici cevap:** Müvekkilin iyi niyetini gösteren olgular (ihtarname, müzakere girişimi, makul süre bekleme).

---

### Adım 4 — Metni Güçlendir

Hazırlanan metni şu yapıyla genişlet:

```
[Ana argüman]

Bu argümanı destekleyen olgular ve hukuki dayanaklar yukarıda
detaylı sunulmuş olmakla birlikte; davalı tarafça aşağıdaki muhtemel
savunmaların ileri sürülebileceği öngörüsüyle, bu hususlara önceden
ileri cevaplarımız aşağıda sunulmaktadır.

KARŞI TARAFIN MUHTEMEL SAVUNMASI 1: "..."
İLERİ CEVABIMIZ: ...
[Hukuki dayanak + içtihat]

KARŞI TARAFIN MUHTEMEL SAVUNMASI 2: "..."
İLERİ CEVABIMIZ: ...
```

Bu yapı, davacının **Sherlock öngörüsünü** mahkemeye gösterir; karşı vekilin sunabileceği saldırıları **prosedürün başında** sıfırlar.

---

### Adım 5 — Sözleşme Müzakeresi Versiyonu

Sözleşme görüşmesinde, taraftarımızın talebini söylemeden önce **karşı tarafın geri çevirme** olasılığını ele al:

```
"Şu maddenin {X} olarak değiştirilmesini öneriyoruz, çünkü {gerekçe1}.

Karşı tarafın 'biz bunu standart pozisyon kabul etmiyoruz' demesi
beklenir. Buna karşı şu kontra argüman hazır: '{rakip karşılaştırma /
emsal sözleşme / mevzuata uyum}'.

Karşı taraf 'bu kadar değişiklik kabul edemeyiz' derse şu hibrit
yapıyı öner: ..."
```

---

## Standart Çıktı Formatı

```markdown
# Karşı Argüman Öngörme — {konu}

## Girdi
[Hazırlanan metin / pozisyon]

## I. Hâkim Şüpheleri
1. ...
2. ...

## II. Davalının Olası Savunmaları
| Savunma | İleri cevabımız | Metne nereye eklensin |
|---|---|---|

## III. Üçüncü Kişilerin (varsa) Müdahale Argümanları
[Müdahil olabilecek tarafların itirazları]

## IV. Güçlendirilmiş Metin
[Önleyici cevaplar yerleştirilmiş tam metin]

## V. Audit Trail
[Hangi içtihat hangi savunmaya cevap verir; yargi_mcp atıfları]
```

## Eskalasyon Tetikleyicileri

1. Karşı tarafın savunmasının **henüz öngörülemeyen** bir yön içerebileceği şüphesi (yeni / tartışmalı alan) → doktrin tarama (dergipark-doktrin-arastirma)
2. **Birden fazla davalı** + çelişkili savunmalar → kıdemli görüş
3. **Anayasal boyut** öngörülüyorsa → AYM hazırlığı

## Notlar

- "10 adım önde düşünme" maliyetli olabilir — tüm savunmaları öngörmek zaman alır, ama **kazanma şansını ciddi yükseltir**.
- Aşırı önleyici cevap **mahkeme tarafından "savunmayı tahmin etmek"** olarak algılanmamalı; metin **dengeli** kalmalı.
- `dava-strateji-analiz` skill'inin Adım 5'i ile entegre — beraber çalışır.
