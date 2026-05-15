---
name: brifing
description: Günlük, konu odaklı veya olay temelli hukuki brifing üretir. Sabah brifingi e-posta, takvim, sözleşme yenileme ve süre yaklaşmalarını bir araya getirir; konu brifingi spesifik hukuki sorunu derinleştirir; olay brifingi acil bir durum (veri ihlali, dava açılması, kurum yazısı, medya olayı) için hızlı bağlam toplar.
---

# /turk-hukuk-legal:brifing — Hukuki Brifing

## Davet

```
/turk-hukuk-legal:brifing gunluk
/turk-hukuk-legal:brifing konu [sorgu]
/turk-hukuk-legal:brifing olay
```

## Modlar

### Mod 1 — Günlük Brifing

Her sabah çalıştırılır (scheduled agent olarak da kurulabilir). İçindekiler:

- Dün gelen e-postaların hukuki ilgili olanları (sözleşme, ihtarname, KEP tebligatı, kurum yazısı)
- Bugün ve yarın takvim olayları (duruşma, müzakere, görüşme)
- Bu hafta yaklaşan süreler (cevap dilekçesi, KVKK m.13 yanıt, ihtarname yanıt, KEP yanıt)
- Otomatik yenileme süreleri dolanlar (90 gün, 30 gün, 7 gün uyarı eşikleri)
- Resmî Gazete'de yayınlanan ilgili mevzuat değişiklikleri
- Sektörel kurum kararları (KVKK, BDDK, Rekabet, vb.)
- Yargıtay/Danıştay/AYM yeni içtihat (büro ilgi alanlarında)

**Çıktı yapısı:**

```markdown
## Günlük Brifing — [Tarih]

### Hemen aksiyon gerektiren
- ...

### Bugün
- 10:00 — [Duruşma / Toplantı]
- 14:00 — [Müvekkil görüşmesi]

### Yarın hazırlık
- [duruşma / toplantı]

### Bu hafta süre dolanlar
- ... — [tip] — [son tarih]

### Sözleşme yenileme uyarıları
- [tedarikçi/sözleşme] — [tarih]

### Önemli e-postalar (özet)
- [konu] — [gönderen] — [özet]

### Mevzuat & içtihat
- Resmî Gazete: [yeni yayın özet]
- Sektörel: [karar özet]
- İçtihat: [karar özet]

### Yarın hazırlanması gereken
- ...
```

### Mod 2 — Konu Brifingi

Spesifik bir hukuki soruyu derinleştirir. Tipik kullanım: yeni bir konu/dosya açıldığında veya müvekkil zor bir soru sorduğunda.

İş akışı:
1. Sorgu metnini al
2. Mevzuat tara — `mevzuat_mcp` ile ilgili kanun, KHK, CBK, yönetmelik
3. İçtihat tara — `yargi_mcp` ile yüksek mahkeme + BAM kararları
4. Büro RAG'ı tara — `hukuk-rag` ile büro dosyalarında benzer vakıa
5. Doktrini özetle (varsa)
6. Görüş özeti çıkar

**Çıktı yapısı:**

```markdown
## Konu Brifingi: [Soru]

### Hukuki çerçeve
- Maddi hukuk: ...
- Usul: ...
- Süreler: ...

### Mevzuat
- TBK / TTK / FSEK / KVKK / vb. m.X — [içerik özet, mevzuat_mcp ile doğrulandı]
- ...

### Yargıtay/Danıştay/AYM içtihatı
- [Karar atıfı + özet] — yargi_mcp
- [Karar atıfı + özet]

### Bizim büromuzda geçmiş benzer dosyalar
- [hukuk-rag çıktısı]

### Doktrin (varsa)
- ...

### Görüş özeti
[2-3 paragraf — soruya cevap]

### Açık konular / belirsizlikler
- ...

### Önerilen sonraki adımlar
1. ...
2. ...
```

### Mod 3 — Olay Brifingi

Acil durum (veri ihlali, dava açılması, kurum yazısı, medya olayı, müvekkil krizi). Hız önemli — kısa ama somut.

**Çıktı yapısı:**

```markdown
## Olay Brifingi — [Olay]

### Ne biliyoruz
- [Kesin olgu] (kaynak: ...)
- [Kesin olgu] (kaynak: ...)

### Ne bilmiyoruz
- ...

### Yasal saatler (en kritik)
| Süre | Yükümlülük | Son tarih |
|---|---|---|
| 72 saat | KVKK Kurulu'na veri ihlali bildirimi | ... |
| 14 gün | Mahkeme yazısına yanıt | ... |
| ... | ... | ... |

### Acil koordinasyon gereken kişi/birim
- ...
- ...

### Olası senaryolar
- [En iyi] ...
- [Beklenen] ...
- [En kötü] ...

### Hemen yapılacaklar (24 saat içinde)
1. ...
2. ...

### Sonra yapılacaklar (1 hafta içinde)
1. ...
2. ...

### Ekipte rol dağılımı önerisi
- ...
```

## Türk Pratiği için Notlar

**Süre disiplini:** Türk yargılama sisteminde **hak düşürücü süreler** ve **zamanaşımı süreleri** kritiktir. Brifing'te süreler açık şekilde gösterilmeli; takvime atılmalı.

**KEP zorunluluğu:** Sermaye şirketleri arası yazışmalarda KEP zorunlu (TTK m.18/3). KEP geleli kayıtların izlenmesi günlük brifing parçasıdır.

**UYAP entegrasyonu:** Dava süreçleri UYAP üzerinden takip edilir. UYAP MCP'si yoksa avukat tarafı günlük UYAP kontrolü ihmal edilmemeli.

**Otomatik yenileme:** Türk hukukunda otomatik yenilenen sözleşmelerin **ihbar süresi** geçirilirse fesih reddedilir. Bu süreler **takvim öncelikli**.

**Resmî Gazete:** Mevzuat takibi için RG günlük taranmalı; sektörel kurum kararları RG'de ayrıca yayınlanır.

## Scheduled Agent Olarak Kurulum

Günlük brifing zamanlanmış görev olarak her sabah 07:00'de çalıştırılabilir:

```
mcp__scheduled-tasks__create_scheduled_task(
  cronExpression: "0 7 * * 1-5",  # iş günleri sabah 7
  prompt: "/turk-hukuk-legal:brifing gunluk"
)
```

## Notlar

- Konu brifingi tek seferlik bir görev; günlük brifingi periyodik bir alışkanlık.
- Olay brifingi krize göre uyarlanır; hız > detay.
- Her brifing, müvekkille paylaşılırken **gizlilik/imtiyaz** çerçevesi düşünülmeli.
