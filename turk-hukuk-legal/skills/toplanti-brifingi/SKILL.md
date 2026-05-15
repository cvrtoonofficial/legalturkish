---
name: toplanti-brifingi
description: Hukuki içerikli toplantılar için yapılandırılmış brifing hazırlar — sözleşme müzakereleri, duruşma öncesi, yönetim kurulu, uyum incelemesi, denetim, kurum görüşmesi. Bağlam araştırması, anahtar belge listesi, eylem kalemi takip çerçevesi.
---

# /turk-hukuk-legal:toplanti-brifingi — Toplantı Brifingi

## Davet

```
/turk-hukuk-legal:toplanti-brifingi [toplantı türü]
```

Toplantı türleri:
- `muzakere` — sözleşme müzakeresi
- `durusma-oncesi` — duruşma hazırlığı
- `yk` — yönetim kurulu / icra kurulu
- `uyum` — uyum / denetim toplantısı
- `kurum-gorusmesi` — düzenleyici kurum görüşmesi
- `musvekkil` — müvekkille strateji görüşmesi
- `genel` — özel tip

## İş Akışı

### Adım 1 — Toplantı Bağlamını Topla

| Bilgi | Soru |
|---|---|
| Toplantı tarihi & yeri | Fiziksel mi online mı? |
| Katılımcılar | Kim katılıyor, hangi sıfatla? |
| Karşı taraf temsili | Avukat kim, kıdemi? |
| Toplantı tipi | Bağlayıcı karar mı, müzakere mi, bilgi alma mı? |
| Belge önceden paylaşıldı mı | Hangi belgeler hazır olmalı? |
| Süre kısıtlaması | Acil karar gerektiren konu var mı? |
| Çıkar çatışması | Tarafsızlık veya gizlilik koruma gereği |

### Adım 2 — İlgili Belgeleri Topla

Connected sistemlerden tara:
- Sözleşme dosyası — son imzalı versiyon, müzakere notları, geçmiş revizyonlar
- Yazışmalar — son 6 ay e-posta, KEP, ihtarname
- Önceki toplantı tutanakları
- İlgili mahkeme dosyaları (varsa)
- Mevzuat ve içtihat — `mevzuat_mcp` + `yargi_mcp`
- Sektörel düzenleyici kurum kararları

### Adım 3 — Toplantı Tipine Göre Brifing Yapısı

#### A. Sözleşme Müzakeresi

```markdown
## Müzakere Brifingi

**Sözleşme:** [...]
**Karşı taraf:** [...]
**Tarih:** [...]

### Bizim pozisyonumuz
- Birincil hedef: ...
- İkincil hedef: ...
- Geri çekilme noktası: ...

### Karşı tarafın pozisyonu (anlaşılan)
- ...

### Açık maddeler
| Madde | Bizim teklif | Karşı teklif | Geri çekilme | Strateji |
|---|---|---|---|---|

### Kırmızı çizgiler
- Kabul edemeyeceğimiz maddeler (TBK m.115 emredici, FSEK m.16-19 manevi haklar, vb.)

### Sıralama önerisi
1. Önce çözüme yakın konular (güven ortamı için)
2. Sonra orta zorluk
3. En son, en zor konu

### Sunulacak doküman paketi
- ...

### Karar yetkileri
- Bu toplantıda kim karar verebilir?
- Eskalasyon noktası: ...

### Sonraki adımlar (toplantı sonrası beklenti)
- Yazılı taahhüt ihtiyacı?
- Tekrar görüşme tarihi?
```

#### B. Duruşma Öncesi Hazırlık

```markdown
## Duruşma Brifingi

**Mahkeme:** [...]
**Esas no:** [...]
**Duruşma tarihi:** [...]
**Aşama:** [İlk inceleme / Tahkikat / Sözlü yargılama / Karar]

### Dava özeti
- Konu: ...
- Bizim tarafımız: ...
- Talep / itiraz: ...

### Önceki tutanaklar özeti
- Geçen duruşmada ne oldu?
- Karara bağlanan ara işlemler

### Bu duruşmada hedef
- Tutulması istenen ara karar
- Sunulacak yeni delil / dilekçe
- Tanık dinleneceği
- Bilirkişi raporuna itiraz

### Hazırlanan belgeler
- ...

### Karşı tarafın olası argümanları
- ...

### Karşı argümanlar (hazırda)
- ...

### Süre kontrolü
- [ ] Dilekçe sunma süresi
- [ ] Bilirkişi raporu itiraz süresi
- [ ] Tanık listesi süresi
- [ ] Diğer ...

### Müvekkil hazırlığı
- Müvekkil katılacak mı?
- Beyan alma riski var mı?
- Hazırlanması gereken sorular
```

#### C. Yönetim Kurulu / İcra Kurulu

```markdown
## YK Hukuk Brifingi

**Toplantı tarihi:** [...]
**Gündem konuları (hukuk ilgili):**
1. ...
2. ...

### Konu 1 — [...]
- Mevcut durum
- Hukuki risk
- Karar seçenekleri (A/B/C)
- Önerilen karar
- Yasal süre baskısı (varsa)

### Açık riskler (bilgilendirme)
- ...

### Yaklaşan yasal yükümlülükler
- ...

### Stratejik hukuki notlar
- Mevzuat değişiklikleri etkisi
- Sektörel kurum gelişmeleri
- Yargıtay içtihat değişiklikleri
```

#### D. Düzenleyici Kurum Görüşmesi

```markdown
## Kurum Görüşmesi Brifingi

**Kurum:** [BDDK / EPDK / KVKK Kurulu / Rekabet Kurumu / ...]
**Yazışma referansı:** [...]
**Toplantı tarihi:** [...]

### Konu
[Kurum yazısındaki soru/soruşturma]

### Bizim pozisyonumuz
- Olgular
- Hukuki dayanak
- Daha önce kurum ile yazışmalar

### Sunulacak belgeler
- ...

### Hassas noktalar
- Yanıt vermeden önce iç hukuk değerlendirme yapılması gerekenler
- Daha sonra yazılı süreçte teyit edilmesi gereken sözlü açıklamalar

### Avukat-müvekkil imtiyazı koruması
- Hangi belgeler imtiyaz kapsamında?
- İmtiyazlı belgenin yanlışlıkla teslimi riski (waiver)

### Sonraki adımlar
- Yazılı tutanak gelir mi?
- Süreklilik için takip planı
```

### Adım 4 — Eylem Kalemi Takibi

Toplantı sonrası bu skill ile **eylem kalemleri** kayıt altına alınabilir:

```markdown
## Toplantı Sonrası Eylem Kalemleri

| # | Eylem | Sorumlu | Son tarih | Durum |
|---|---|---|---|---|
| 1 | Karşı taraf redline cevabı bekleme | ... | ... | Açık |
| 2 | Müvekkille onay alma | ... | ... | Açık |

### Karar verilen noktalar
- ...

### Açık kalan noktalar (sonraki görüşme için)
- ...
```

## Türk Pratiği için İpuçları

- **UYAP üzerinden duruşma günlerini izle** — duruşma günü değişebilir
- **E-Tebligat ve KEP** üzerinden gelen tebligatların duruşmadan önce kontrolü
- **Hâkim tipi** — ihtisas mahkemesi (Fikri ve Sınai Haklar, İş, Tüketici, Aile) farklı dinamikte; uzmanlık eksiklerinde daha fazla açıklama gerek
- **Bilirkişi vs. uzman tanık** — bilirkişi raporu mahkemece istenir; uzman tanık tarafça çağrılır (HMK m.293)
- **Tutanak hazırlığı** — duruşma tutanağında yer alması istenilen ifadeleri önceden notla
- **Kıdemli avukatla strateji görüşmesi** — büyük toplantıdan önce yarım saatlik prep oturumu uygulamada çok değerli

## Notlar

- Toplantı tutanağı varsa yapay zekâ destekli özet çıkartılabilir ama tutanağın **resmi versiyonu mahkeme tutanağıdır**
- KEP üzerinden tebligat takibi otomatize edilebilir (mevcut MCP'lere bakılması gerek)
- Eylem kalemleri takvime ve görev yönetim sistemine taşınmalı
