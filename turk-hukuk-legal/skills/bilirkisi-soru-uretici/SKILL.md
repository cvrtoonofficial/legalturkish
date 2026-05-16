---
name: bilirkisi-soru-uretici
description: Bilirkişiye yöneltilecek teknik ve hukuki soruların sistematik üretimi. HMK m.266-289 çerçevesinde, davanın özel uzmanlık gerektiren noktalarını analiz eder; sorulması gereken soruları olgu, hukuk, teknik ve nedensel ilişki başlıklarına ayırır. Türk yargı pratiğinde bilirkişi raporu davanın kaderini büyük oranda belirler — bu skill bilirkişiye doğru soruların sorulmasını sağlar. Fikri ve sınai haklar, müzik telif, yazılım, mali bilirkişilik, inşaat, tıp ve teknik konular için uygundur.
version: 0.2.0
last_legal_review: 2026-05-16
required_mcps:
  - mevzuat_mcp
optional_mcps:
  - yargi_mcp
  - hukuk-rag
applicable_laws:
  - 6100
  - 5846
  - 6769
---

# /turk-hukuk-legal:bilirkisi-soru-uretici — Bilirkişi Soruları Üretici

> Türk yargı pratiğinde **bilirkişi raporu davanın kaderini belirler** — özellikle FSEK/SMK, mali, teknik, müzik telif davalarında. Doğru soruların sorulması, raporun değerini ve kanıt gücünü doğrudan etkiler. Bu skill, bilirkişi heyetine yöneltilecek soruları sistematik üretir.

## Adım 0 — Zorunlu MCP Çağrıları

### 0.1 Profil okuma
- `~/.claude/plugins/config/turk-hukuk-legal/CLAUDE.md`

### 0.2 Mevzuat çekme (`mevzuat_mcp`)
- **Kanun 6100 HMK** — m.266-289 (bilirkişi rejimi); anahtar: "bilirkişi", "uzman görüş", "rapor itirazı"
- Davanın özüne bağlı kanunlar (FSEK 5846, SMK 6769, vb.)

### 0.3 İçtihat tarama (`yargi_mcp`)
- Bilirkişi raporu eleştirilerine ilişkin yerleşik içtihat
- `yargi_mcp.search_bedesten_unified(...)` — "bilirkişi raporu yetersiz", "ek rapor"

### 0.4 `hukuk-rag` (varsa)
- Matter dosyasından **teknik nokta** ve **uzmanlık alanları**nı çıkar:
  ```
  mcp__hukuk-rag__hukuk_rag_ara(
    sorgu="teknik konu / uzmanlık / inceleme noktası",
    dava="<matter_collection>"
  )
  ```

---

## İş Akışı

### Adım 1 — Bilirkişiye Sorulan Konuyu Tanımla

#### Davanın hangi noktası uzman incelemesi gerektiriyor?

- [ ] **Eser sahipliği / orijinallik** (FSEK)
- [ ] **Marka karıştırılma ihtimali** (SMK m.6/1)
- [ ] **Patent istem analizi & tecavüz** (SMK m.85, 141)
- [ ] **Tasarım benzerliği — bilgili kullanıcı testi** (SMK m.55+)
- [ ] **Müzik / ses kayıt benzerliği** (FSEK m.5, 6, 80)
- [ ] **Yazılım kodu karşılaştırması** (FSEK m.2/1)
- [ ] **Mali zarar hesabı** (TBK m.49+, FSEK m.68, m.70)
- [ ] **İnşaat / yapı kalitesi** (TBK eser sözleşmesi)
- [ ] **Tıbbi malpraktis** (TBK + Hekim Etiği)
- [ ] **Trafik / kaza** (yeniden inşa, çarpışma analizi)
- [ ] **Belge / imza / yazı incelemesi** (CMK + grafoloji)
- [ ] **Bilişim suçu / dijital delil** (TCK + 5651)
- [ ] **Veri ihlali / KVKK teknik analiz** (KVKK m.12)
- [ ] **Diğer:** ...

### Adım 2 — Uzmanlık Alanlarını Belirle

Bilirkişi heyetinde hangi disiplinler olmalı?

| Disiplin | Tipik vaka |
|---|---|
| Hukukçu | Yorum, içtihat ışığında değerlendirme |
| Mali müşavir / SMMM | Tazminat, rayiç bedel, kar kaybı |
| Mühendis (yazılım, makine, inşaat) | Teknik karşılaştırma |
| Müzik uzmanı / müzikolog | Müzik eseri benzerliği |
| Patent vekili | Patent istem analizi |
| Marka vekili | Karıştırılma ihtimali |
| Doktor (uzman dal) | Tıbbi sorumluluk |
| Grafolog | İmza/yazı incelemesi |
| Bilişim uzmanı | Dijital delil, ACR sistemleri |

**Heyet önerisi:** Karma heyet (örn. hukukçu + mali müşavir + ilgili mühendis) genelde daha sağlam rapor üretir.

### Adım 3 — Soruları Kategorilere Ayır

#### A. Olgu Soruları (ne var, ne yok)

> Davanın **maddi vakıası**nı netleştirir; bilirkişinin gözleyebileceği nesnel gerçekler.

Örnekler:
- "Davalı platformda davacının {eser_adı} adlı eserinin {tarih1} ile {tarih2} arasında kaç farklı kullanıcı tarafından yüklendiği tespit edilsin."
- "Sözleşmede yer alan {kloz_adı} maddesi, taraflar arasında imzalanan {tarih} tarihli sözleşmede mevcut mudur, varsa metni aynen aktarılsın."
- "Bilirkişice yapılan inceleme tarihinde, davalı sitesinde {URL} adresinde yer alan içeriğin durumu tespit edilsin."

#### B. Teknik Sorular (uzmanlık gerektiren değerlendirme)

> Olayların **teknik nitelikte** bir uzmanlık değerlendirmesi gerektirdiği noktalar.

Örnekler (FSEK senaryosu):
- "Davacıya ait {eser_adı} ile davalıda kullanılan {ihlal_içeriği} arasında, eser sahipliği ölçütleri açısından (özgünlük, yaratıcılık, ifade biçimi), bilirkişinin değerlendirmesine göre **birebir benzerlik, asli unsur benzerliği veya bağımsız geliştirme** ilişkisi tespit edilebilir mi?"
- "Davacının eseri ile karşılaştırılan içerik arasında **sıradan dinleyici / bilgili kullanıcı / makine analizi** açısından karıştırılma ihtimali bulunmakta mıdır?"
- "Davalının kullandığı algoritmanın, davacının eserlerinin tespiti açısından bir **Automatic Content Recognition (ACR) sistemi** ile karşılaştırıldığında, mevcut teknolojik standartların gereksinimlerini karşılayıp karşılamadığı tespit edilsin."

Örnekler (Patent senaryosu — SMK m.85):
- "Davalı tarafından üretilen {ürün} 'un teknik özelliklerini, davacının {patent_no} numaralı patentinin bağımsız istem(ler)i ile **eleman eleman** karşılaştırarak, her bir istem unsuru için 'okunuyor / okunmuyor / eşdeğer' değerlendirmesi yapın."
- "Eşdeğerler doktrini (doctrine of equivalents) ışığında, davalı ürününün istemlerin değişiklikli ifa edilmiş hali olup olmadığı değerlendirilsin."

Örnekler (Mali senaryosu — FSEK m.68):
- "Davacıya ait {eser_listesi} için, eserlerin emsal lisans bedelleri dikkate alınarak rayiç bedel hesaplansın. Rayiç bedel hesabında: (i) eserin niteliği, (ii) kullanım kapsamı, (iii) kullanım süresi, (iv) pazar payı, (v) emsal piyasa bedelleri esas alınsın."
- "FSEK m.68 uyarınca, davalının kullanımı kasıt veya ağır kusurla gerçekleşmiş ise rayiç bedelin **üç katına kadar** tazminat hesabı yapılsın."

#### C. Hukuki Karakter Soruları (yorum gerektiren)

> Burada bilirkişinin **hukuki sonuç çıkarması istenmez** — hâkim yetkisindedir. Ama olgunun **hukuki nitelendirilmesi için ön bilgi** istenebilir.

Örnekler:
- "Davacının {eser_adı} adlı eserinin FSEK m.1/B uyarınca eser niteliği taşıyıp taşımadığı; özgünlük, ifade kalıbı, sahibinin hususiyetini taşıma kriterleri açısından değerlendirilsin."
- "Davalının ToS'undaki (Kullanım Koşulları) {madde_no} numaralı lisans klozu, FSEK m.52/2 uyarınca **mali hakların ayrı sayımı şartını karşılayıp karşılamadığı** ve genel ifade kullanılıp kullanılmadığı yönünden değerlendirilsin."

#### D. Nedensel İlişki Soruları (sebep-sonuç)

> Bir olayın diğerinin sebebi olup olmadığı; özellikle tazminat davalarında.

Örnekler:
- "Davalı platformun ACR sistemi kurmama tercihi ile davacının eserlerinin platform üzerinde yetkisiz dolaşımı arasında **doğrudan nedensel bağ** bulunmakta mıdır?"
- "Trafik kazasında, davalı sürücünün hızı ve davacının yaralanmasının ağırlığı arasındaki ilişki tespit edilsin."

#### E. Eksik İnceleme / Ek Bilgi İstemek

Bazen ana soru cevapsız kalır; ek bilgi gerek:

- "Bilirkişi heyetinin tespitlerinin {konu} açısından eksik kaldığı; ek belge / örnek / analiz gerektirdiği değerlendirilebilirse, hangi belgelerin/numune tipinin gerektiği belirtilsin."
- "İnceleme, sadece sunulan belgelere dayanılarak yapıldığından, davalının üretim tesislerinde keşif veya numune alımı yapılmasının raporun değerini artırıp artırmayacağı görüş olarak verilsin."

### Adım 4 — Soru Formatı ve Kuralları

#### İyi soru kriterleri

- ✅ **Net** — tek bir konuya odaklı
- ✅ **Yönlendirici değil** — cevabı içermez
- ✅ **Ölçülebilir** — somut bir tespit veya sayı bekler
- ✅ **HMK m.281'e uygun** — bilirkişinin uzmanlık alanı içinde
- ✅ **İçtihat referanslı** — gerektiğinde Yargıtay 11. HD vb. kararlara atfen

#### Sık hatalar

- ❌ "Davacı haklı mıdır?" (hukuki sonuç sorusu — hâkim takdiri)
- ❌ "Ne kadar tazminat verilmelidir?" (bilirkişi hesap yapar, takdir hâkimde)
- ❌ Çok geniş soru ("Bütün dosyayı incele")
- ❌ Cevabı yönlendiren soru ("Davalının kötü niyetli olduğu doğru mudur?")
- ❌ Bilirkişinin uzmanlık alanı dışı soru (örn. mühendise hukuki yorum)

### Adım 5 — Soru Setini Düzenle

Soruları üç gruba ayır:

#### Grup 1 — İlk rapor için zorunlu sorular (5-10 soru)
- Davanın can damarı; raporda mutlaka cevap istenmeli
- Olgu + temel teknik sorular

#### Grup 2 — Detay / destekleyici sorular (5-15 soru)
- Ana sorulara destek; rapor zenginleşsin
- Yan teknik + nedensel ilişki

#### Grup 3 — Şartlı / yedek sorular (3-7 soru)
- Eğer ilk rapor belirsiz çıkarsa, **ek rapor talebi** için
- "Eğer rapor X yönünde ise Y de değerlendirilsin"

### Adım 6 — Rapor İtirazına Hazırlık

Skill, rapor geldiğinde yapılacak itirazların **çekirdek mantığını** önceden hazırlar:

- "Eğer rapor şu noktayı atlarsa: HMK m.281 ek rapor istenir"
- "Eğer rapor metodu eksikse: bilirkişi heyetinin teknik dayanaklarının yetersizliği itirazı"
- "Eğer rapor yanılgılı bir hukuki nitelendirme yapmışsa: hukuki nitelendirmenin hâkim yetkisinde olduğu hatırlatılır"

---

## Standart Çıktı Formatı (Hukuki Memo)

```markdown
# Bilirkişi Soruları — {matter_adi}

**Konu:** {özet}
**Bilirkişi heyeti önerisi:** {disiplin1, disiplin2, ...}
**Dosya:** {esas no}
**Skill versiyonu:** 0.2.0

## I. Davanın Bilirkişi İhtiyacı
[Hangi noktaların uzman incelemesi gerektirdiği]

## II. Önerilen Bilirkişi Heyeti
[Disiplin bazlı uzmanlık önerileri]

## III. Soru Seti

### Grup 1 — Zorunlu Sorular (ilk rapor için)
1. ...
2. ...
3. ...

### Grup 2 — Detay Sorular
1. ...

### Grup 3 — Şartlı / Yedek Sorular
1. Eğer rapor X yönünde ise: ...

## IV. Rapor İtirazına Hazırlık
- Hangi nokta eksik kalırsa ek rapor istenir
- Olası yanılgıların erken işaretlenmesi
- HMK m.281 ek rapor talebi formülasyonu

## V. Süreler
- Rapor itirazı için süre: 2 hafta (HMK m.281 — mevzuat_mcp ile doğrulandı)
- Ek rapor talebi: rapor tebliğinden itibaren makul süre

## Ekler
A. Doğrulanmış Mevzuat (HMK m.266-289)
B. İçtihat Referansları (yargi_mcp — bilirkişi raporu yetersizlik içtihatı)
C. Matter Dosya Referansları (hukuk-rag)
D. MCP Çağrı Logu
E. Eskalasyon Kontrolü
F. Versiyon & Doğrulama
```

## Eskalasyon Tetikleyicileri

1. Davada **çoklu uzmanlık** gerektiren ve heyet bileşimi belirsizse → kıdemli görüş
2. Karşı tarafın bilirkişi raporuyla çelişen **alternatif uzman görüşü** (HMK m.293 uzman tanık) gerekiyor
3. **Yabancı dil bilirkişi** veya **yurt dışı uzman** gerek (özellikle patent davalarında)
4. **Hâkimin re'sen bilirkişi seçimi** yerine **tarafların önerdiği bilirkişi** istemi (HMK m.267)
5. **Bilirkişi heyetinin yetersizliği** açıksa: bilirkişi yenileme talebi (HMK m.281)

## Notlar

- Soru seti **sözlü yargılama aşamasında değiştirilebilir**; ihtiyaca göre güncellenir.
- Bilirkişi raporu **mahkemeyi bağlamaz** (HMK m.282) — hâkim takdir yetkisini kullanır; ama pratikte raporlar belirleyicidir.
- Türk pratiğinde **bilirkişi raporunun kalitesi davanın kaderini büyük oranda belirler** — bu yüzden iyi soru sormak kritiktir.
