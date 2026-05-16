---
name: dergipark-doktrin-arastirma
description: literatur-mcp (DergiPark) ve yoktez-mcp (YÖK Ulusal Tez Merkezi) üzerinden belirli bir hukuki konuda Türk akademik literatürünü tarar. Çoğunluk görüşü vs. azınlık görüşü ayrımı, son 5 yılın en çok atıf alan makaleleri, monografik tezler. Davadaki argümanlar için doktrin desteği bulur — özellikle yeni veya tartışmalı konularda kritik. FSEK + YZ eseri, sınır ötesi tüketici, sanal aldatma, Grok eğitim verisi gibi yerleşik içtihatı zayıf konular için zorunlu.
version: 0.4.0
last_legal_review: 2026-05-16
required_mcps:
  - literatur-mcp
  - yoktez-mcp
optional_mcps:
  - mevzuat_mcp
  - yargi_mcp
applicable_laws: []
---

# /turk-hukuk-legal:dergipark-doktrin-arastirma — Akademik Doktrin Taraması

> Yerleşik içtihatı zayıf olduğu yerlerde **doktrin görüşü** mahkemeye sunulabilir destek argümandır. Akademik makaleler ve tezler, hâkimin **yeni / tartışmalı** konularda karar verirken referans aldığı kaynaklardır.

## Adım 0 — Zorunlu MCP Çağrıları

### 0.1 MCP'lerin bağlı olduğunu doğrula
- `literatur-mcp` (DergiPark) bağlı mı
- `yoktez-mcp` (YÖK) bağlı mı
- İkisi de yoksa skill çalışmaz, kullanıcıya uyarı

### 0.2 Profil okuma — Türk akademik literatür tercihi olan dergi/yazar var mı?

---

## İş Akışı

### Adım 1 — Araştırma Konusunu Daraltın

```
Sor:
1. Konu nedir (kısa cümle)?
2. Hangi dava bağlamında? (matter_id)
3. Hangi argümanı destekleyecek doktrin? (lehe / aleyhe / her ikisi)
4. Son N yılın taranması? (default: 5 yıl)
5. Tip: sadece makale / sadece tez / her ikisi?
```

### Adım 2 — DergiPark Taraması

`literatur-mcp` ile:
```
literatur_mcp.search(
  query="<konu>",
  filters={
    year: ">=2021",
    field: "law" (varsa),
    language: "tr"
  }
)
```

Çıkan makaleleri **alaka sırası** + **atıf sayısı** + **dergi prestiji** kriterleriyle sırala.

### Adım 3 — YÖK Tez Taraması

`yoktez-mcp` ile lisansüstü + doktora tezleri:
```
yoktez_mcp.search(query="<konu>", level=["yuksek_lisans", "doktora"])
```

Tezler **monografik** olduğu için bir konunun en sistematik analizini sunar.

### Adım 4 — Görüş Sınıflandırması

Çıkan kaynakları **3 gruba** ayır:

| Grup | Ne içerir | Davada nasıl kullanılır |
|---|---|---|
| **Çoğunluk görüşü** | Doktrinde yerleşmiş kabul | Lehe argüman ana destek |
| **Azınlık görüşü** | Karşı görüş — sayıca az | Karşı tarafın olası argümanı; önceden yanıt |
| **Tartışmalı / yeni** | Henüz yerleşmemiş | Davayı bu konuda yeni içtihat yaratma fırsatı |

### Adım 5 — Görüşler Arası Tartışma Sentezi

Her görüş için:
- Yazar(lar) + eserin künyesi
- Görüşün özü
- Hangi argüman üzerine dayanıyor
- Karşı görüşün eleştirisine cevap (varsa)

### Adım 6 — Mahkemeye Sunum Formatı

Doktrinin mahkemeye sunumunda atıf standartı:

```
"Konuya ilişkin doktrinde [yazar adı]'nın da işaret ettiği üzere
([eser/makale adı], [dergi adı], [cilt/sayı], [yıl], [sayfa]):
'[ifadenin özü]' Bu görüş yerleşik bir kabul olup, somut olayda
{nasıl uygulanır}."
```

> Doktrin atıfı **mahkemeyi bağlamaz** ama özellikle yeni konularda hâkim için yol göstericidir. Yargıtay 11. HD bazı kararlarında "doktrindeki yerleşik görüşler doğrultusunda" formülasyonunu kullanır (`yargi_mcp` ile doğrula).

---

## Konuya Özgü Doktrin Soruları

### Müzik telif (FSEK)
- Eser sahipliği karinesi (FSEK m.11) — sınırları
- Mali hakların ayrı sayımı (m.52) — clickwrap'le imzalanan sözleşmelerin yaklaşımı
- Bağlantılı haklar (m.80) — yapımcı + icracı çakışması
- ACR sistemi yokluğunun platform sorumluluğuna etkisi
- AI eğitim verisi olarak kullanım — yeni alan, doktrin gelişiyor
- Meslek birliği yetki dağılımı (m.42 vd.)

### Trafik kazası
- Maluliyet hesabında PMF tarifesi vs. aktif tarife
- Manevi tazminat üst sınırı
- Sigorta tahkim ile mahkeme arasındaki yargı yolu

### Vergi
- Re'sen tarhiyatın gerekçe yükümlülüğü
- Özelgeye dayanma + sorumluluk
- İnceleme süresi (VUK Ek m.7) hak düşürücü mü düzenleyici mi

### Sınır ötesi tüketici
- MÖHUK m.26 tüketici tanımı genişliği
- Yabancı tahkim klozu + Türk emredici hukuk
- AİHS m.6 etkili başvuru hakkı + masraflar

---

## Standart Çıktı Formatı

```markdown
# Doktrin Taraması — {konu}

**Taranan dönem:** {yıl}-{yıl}
**Kaynaklar:** DergiPark + YÖK Tez (toplam {N} eser)
**Skill versiyonu:** 0.4.0

## I. Çoğunluk Görüşü
[Eser künyeleri + görüş özetleri]

## II. Azınlık Görüşü
[Eser künyeleri + görüş özetleri]

## III. Tartışmalı / Yeni Görüşler
[Henüz yerleşmemiş — fırsat olabilir]

## IV. Mahkemeye Sunulabilir Atıf Listesi
[Standart akademik atıf formatında]

## V. Yargıtay'ın Doktrinle İlişkisi (varsa)
[Yargıtay'ın bu doktrin görüşlerini benimsediği veya reddettiği kararlar — yargi_mcp ile]

## Ekler
A. DergiPark eserlerinin tam künyeleri
B. YÖK tezlerinin künyeleri
C. MCP Çağrı Logu
```

## Notlar

- **Doktrin** mahkemeyi bağlamaz, **destek argüman**dır.
- Yargıtay 11. HD ve diğer dairelerin son içtihatları, doktrindeki görüşleri kabul edip etmediğini gösterir — `yargi_mcp` ile çapraz kontrol.
- Yeni alanlarda (YZ, dijital telif) doktrin **içtihatten önce** gelişir — bu skill bu boşluğu doldurur.
- Tezler genelde **daha derin** ama erişimi zor; yoktez-mcp tam metin sağlar.
