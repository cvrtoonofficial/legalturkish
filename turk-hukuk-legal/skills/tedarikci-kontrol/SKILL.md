---
name: tedarikci-kontrol
description: Bir tedarikçi veya iş ortağıyla mevcut sözleşmelerin durumunu tüm bağlı sistemlerden (CLM, bulut depolama, e-posta, CRM) tarayarak konsolide eder. Hangi belgeler var, hangileri eksik, hangi süreler doluyor, hangi yan yükümlülükler süresiz devam ediyor — kapsamlı tedarikçi hukuki dosya raporu.
argument-hint: "[tedarikçi adı]"
---

# /turk-hukuk-legal:tedarikci-kontrol — Tedarikçi Sözleşme Durum Kontrolü

## Davet

```
/turk-hukuk-legal:tedarikci-kontrol [tedarikçi adı]
```

Tedarikçi adı verilmezse, hangi tedarikçinin kontrol edilmesi istendiği sorulur.

## İş Akışı

### Adım 1 — Tedarikçiyi Belirle

Aşağıdaki varyasyonları dikkate al:

- Tam tüzel kişi adı vs. ticari unvan (örn. "Türkcell İletişim Hizmetleri A.Ş." vs. "Turkcell")
- Türkçe / İngilizce kullanım
- Kısaltmalar (örn. "TTNET" vs. "Türk Telekom")
- Ana şirket / iştirak / şube ilişkileri (TTK m.195 vd. — hâkimiyet kavramı)
- Tedarikçi grubu mu, tek tüzel kişi mi

Belirsizlik varsa kullanıcıdan netleştirme iste.

### Adım 2 — Bağlı Sistemleri Tara

#### CLM (Sözleşme Yaşam Döngüsü) — Bağlıysa
- Aktif sözleşmeler
- Süresi dolmuş sözleşmeler (son 3 yıl)
- Müzakerede / imza beklenende
- Ek protokoller (zeyilname) ve değişiklik metinleri

#### Bulut Depolama (Drive / OneDrive / Box / SharePoint) — Bağlıysa
- İmzalı sözleşmeler
- Redline süreci belgeleri
- Due diligence dosyaları

#### E-posta + KEP — Bağlıysa
- Son 6 ay sözleşme ilgili yazışma
- İhtarname / KEP tebligatları
- Müzakere thread'leri

#### CRM — Bağlıysa
- Müşteri / tedarikçi hesabı kaydı
- İlişki tipi ve durumu
- Hukuk müşaviri iletişim bilgileri

#### Sohbet (Slack / Teams) — Bağlıysa
- Son 3 ay tedarikçi adı geçen mesajlar
- İç sözleşme talebi konuşmaları

### Adım 3 — Sözleşme Durumunu Konsolide Et

Her sözleşme için:

| Alan | Detay |
|---|---|
| Sözleşme tipi | NDA, çerçeve sözleşme, hizmet, lisans, KVKK ek protokol, dağıtım, vb. |
| Durum | Aktif / Süresi dolmuş / Müzakerede / İmza beklemede |
| İmza tarihi | ... |
| Süresi | Başlangıç — bitiş |
| Otomatik yenileme | Var/Yok + ön bildirim süresi |
| Anahtar maddeler | Sorumluluk sınırı, uygulanacak hukuk, fesih kuralları |
| Ek protokoller | Sayı + tarih |

### Adım 4 — Boşluk Analizi

```
## Tedarikçi Belge Envanteri

[VAR / EKSİK] Gizlilik sözleşmesi — durum
[VAR / EKSİK] Çerçeve sözleşmesi (MSA muadili) — durum
[VAR / EKSİK] KVKK Ek Protokolü — durum
[VAR / EKSİK] İş emri / SOW(lar) — sayı
[VAR / EKSİK] SLA — durum
[VAR / EKSİK] Sigorta poliçesi suretleri — durum
[VAR / EKSİK] Vergi mukimliği belgesi (yurt dışı tedarikçi için) — durum
[VAR / EKSİK] Banka bilgisi formu — durum
[VAR / EKSİK] Marka/ticari unvan kullanım izni (varsa) — durum
```

İlişki tipine göre eksik olabilecek belgeleri işaretle. Örn: yazılım tedarikçisi varsa KVKK ek protokolü ve OSS bileşen beyanı; lojistik tedarikçisi varsa sigorta poliçesi suretleri.

### Adım 5 — Süre ve Risk Takibi

| Risk | Sözleşme | Detay | Aksiyon |
|---|---|---|---|
| Süre yakın doluyor | ... | Bitiş: ..., otomatik yenileme: ... | Yenileme görüşmesi |
| Önceden ihbar süresi | ... | İhbar süresi: ... gün | Karar ver, ihbar gönder |
| Süresiz yan yükümlülük | ... | Gizlilik, garanti, fikri haklar | Kayıt al, süreklilik takibi |
| Yenileme bildirimi yapılmamış | ... | İhbar tarihi geçmiş | Acil değerlendirme |
| KVKK ek protokol eksik | ... | Veri işleme öngörülüyor | Acil sözleşme |
| Vekâleten imza yetkisi tarihli | ... | Vekâletname süresi: ... | Yeni vekâletname al |

### Adım 6 — Rapor

```markdown
## Tedarikçi Sözleşme Durumu: [Tedarikçi]

**Arama tarihi:** [...]
**Taranan sistemler:** [...]
**Bağlı olmayan sistemler:** [varsa]

### İlişki özeti
- Tedarikçi: [tam tüzel kişi adı]
- İlişki türü: [tedarikçi / iş ortağı / müşteri / ...]
- Müvekkil sözleşme yöneticisi: [...]
- Tedarikçi tarafı muhatap: [...]

### Sözleşme özeti

#### [Sözleşme tipi 1] — [Durum]
- İmza tarihi: ...
- Bitiş: ... (otomatik yenileme: var/yok, ihbar süresi: ...)
- Sorumluluk sınırı: ...
- Uygulanacak hukuk: ...
- Yetki: ...
- Anahtar maddeler: [özet]
- İmzalı suret yeri: [...]

[devam...]

### Boşluk analizi
[Var olan vs. olması gereken]

### Yaklaşan eylemler
- ... gün içinde dolacak: [...]
- Acil eksik: [...]
- Ek protokol gereken konular: [...]

### Süresiz devam eden yan yükümlülükler
- Gizlilik (kapsam: ..., süre: süresiz / X yıl)
- Tazminat (sözleşme sonrası da geçerli kalemler)
- Fikri haklar lisansı / atfı
- Geri ödenmeyen avanslar veya teminat

### Notlar
[E-posta / sohbet aramalarından çıkan bağlam]
```

### Adım 7 — Bağlı Olmayan Kaynakları Yönet

Sistem bağlanmamışsa:

- **CLM bağlı değil:** CLM yok bilgilendirmesi; manuel kontrol önerisi; diğer kaynaklardan bulunanları raporla.
- **CRM bağlı değil:** İlişki bağlamı atla, boşluğu işaretle.
- **E-posta bağlı değil:** E-posta aranmadı bildirimi; "tedarikçi_adı sözleşme" araması önerisi.
- **Bulut depolama bağlı değil:** Belge depolama aranmadı bildirimi.
- **KEP bağlı değil:** Resmî tebligat geçmişi aranmadı; varsa müvekkilden talep et.

Her durumda **hangi kaynakların kontrol edildiği**, **hangilerinin kontrol edilemediği** raporda netleşmeli.

## Türk Hukuku Notları

**TTK m.18/3 KEP yükümlülüğü:** İhtarname, fesih bildirimi, temerrüt ihtarı gibi resmi yazışmaların KEP üzerinden yapılması gerekir (sermaye şirketleri arasında). KEP kayıt geçmişi tedarikçi dosyasının ayrılmaz parçasıdır.

**E-fatura ve e-arşiv:** Ödeme akışı belgeleri tedarikçi dosyasında olmayabilir ama vergi kayıtlarıyla bağlantı tutulmalı.

**Vergi stopajı:** Yurt dışı tedarikçilerde stopaj sorumluluğu (KVK m.30, GVK m.94) ve çifte vergilendirmeyi önleme anlaşması mukimlik belgesi gerekir.

**Vekâletname süresi:** Tedarikçi tarafında imza yetkisi vekâletnameyle ise vekâletnamenin geçerlilik süresi periyodik kontrol edilmeli.

## Notlar

- Hiçbir sistemde sözleşme bulunmazsa, müvekkilden başka depolama lokasyonu sor.
- Tedarikçi grubu için, kullanıcının spesifik tüzel kişi mi grup geneli mi istediğini sor.
- Süresi dolmuş ama yan yükümlülükleri devam eden sözleşmeleri özellikle işaretle.
- 90 gün içinde dolacak sözleşmeler **vurgulu** raporlanmalı.
