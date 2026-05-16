---
name: soguk-baslangic-mulakat
description: Plugin'in ilk kullanımında çalıştırılan kurulum mülakatı. Büronun pratik profilini, uzmanlık alanlarını, müvekkil tipini, saldırganlık tonunu, onay matrisini, standart pozisyonlarını, ihtisas mahkemesi tercihlerini ve hukuk-rag/yargi_mcp/mevzuat_mcp entegrasyon ayarlarını sorar. Çıktı: CLAUDE.md (veya buro.local.md) profil dosyası — diğer tüm skill'ler bu profili okur. Skill çıktısı doldurulmadan diğer skill'ler "generic" çıktı üretir.
---

# /turk-hukuk-legal:soguk-baslangic-mulakat — Soğuk Başlangıç Mülakatı

> **Bu skill, plugin'in tüm diğer skill'lerinin temel taşıdır.** Profil doldurulmadan diğer skill'ler kişiselleştirilmemiş, generic çıktı verir. İlk kullanımda 15-25 dakika ayır.

## Davet

```
/turk-hukuk-legal:soguk-baslangic-mulakat
```

İki mod var:
- **Tam mülakat** (15-25 dk) — kapsamlı profil
- **Hızlı başlangıç** (2 dk) — sadece kritik 4-5 soru; sonra her skill çağırınca profil derinleşir

## İş Akışı

### Adım 0 — Mod Seçimi

Kullanıcıya sor:
- **A**: Tam mülakat (önerilir, ilk kez kuruyorsan)
- **B**: Hızlı başlangıç (sonra zaman buldukça doldurulur)

### Adım 1 — Büro Kimliği

| Alan | Soru |
|---|---|
| Büro adı | "Büronun veya kendinin tam adı?" |
| Baro | "Hangi baroya kayıtlısın?" (varsa) |
| Sicil no | "Baro sicil numaran?" (varsa) |
| Tebligat KEP | "KEP adresin var mı? (TTK m.18/3 zorunluluğu için)" |
| UETS adresi | "Elektronik Tebligat Sistemi adresin?" (varsa) |
| Vergi/T.C. No | "Müvekkil dosyalarında kullandığın kimlik numarası tipi?" |
| Mahlas | "Sanat veya ticari mahlasınla mı çalışıyorsun? (örn. müzik telif davalarında)" |
| Marka vekili sicili | "TPMK marka/patent vekili sicilinde kayıtlı mısın?" (varsa) |

### Adım 2 — Pratiğin Tarafı

İki kapsamlı seçenek:

**A. Asıl taraf olarak çalışıyorum** (kendi davalarımı, kendi sözleşmelerimi yürütüyorum)
**B. Üçüncü kişi adına çalışıyorum** (büro müvekkilleri var)

A ise tek profil, B ise müvekkil tipi başlığı eklenir.

### Adım 3 — Uzmanlık Alanları (çoklu seçim)

```
İhtisas alanların — birden fazla seçebilirsin:
[ ] Fikri haklar — telif (FSEK)
[ ] Fikri haklar — sınai mülkiyet (SMK: marka, patent, tasarım, coğrafi işaret)
[ ] Müzik telif & sanatçı hakları (FSEK + meslek birlikleri)
[ ] Yazılım & teknoloji hukuku (FSEK m.2/1 + lisans + OSS)
[ ] Ticari sözleşmeler (TBK + TTK)
[ ] Tüketici hukuku (TKHK)
[ ] Şirketler hukuku & M&A (TTK + SerPK)
[ ] İş ve sosyal güvenlik (İş K. 4857 + 5510 SGK)
[ ] KVKK & veri koruma (6698 + sektörel)
[ ] Borçlar hukuku & haksız fiil
[ ] Eşya & gayrimenkul
[ ] Aile & miras (TMK)
[ ] Ceza & ceza yargılaması (TCK + CMK)
[ ] İdare & vergi (İYUK + VUK)
[ ] İcra & iflas (İİK)
[ ] Rekabet hukuku (4054)
[ ] Bankacılık & finans (5411 + 6362)
[ ] Telekom & medya (5651 + 5809)
[ ] Sağlık & ilaç (3359 + 1262)
[ ] Diğer: ...
```

### Adım 4 — Müvekkil / Tarafın Tipi

**Hangi pozisyonda olursun daha sık?**

- [ ] Hak sahibi (lisans veren / eser sahibi / tescilli marka sahibi)
- [ ] Hak alan (lisans alan / işveren / yatırımcı)
- [ ] İddia muhatabı (tüketici / işçi / ihtilafa düşen)
- [ ] Asıl taraf (kendi davam)
- [ ] Arabulucu / üçüncü kişi
- [ ] Karma — her pozisyonda

### Adım 5 — Saldırganlık Tonu (Assertion Posture)

Bu, **ihtarname-fsek-smk**, **dilekce-ihtarname**, **icerik-kaldirma-bildirim**, **tecavuz-triyaj** skill'lerinin **default davranışını** değiştirir.

```
Saldırganlık tonu tercihin?
- [ ] STANDART — doğrudan dava ihtarı, kısa süre, tüm yasal yollar saklı
- [ ] ÖLÇÜLÜ — uyarı + makul süre + müzakere kapısı açık
- [ ] MUHAFAZAKÂR — görüşme talebi, uzlaşma daveti önce, dava en sona
- [ ] DEĞİŞKEN — vaka bazlı sor
```

### Adım 6 — Onay Matrisi

| İşlem tipi | Karar verici |
|---|---|
| Müvekkile gönderilecek görüş yazısı | ... |
| Karşı tarafa gönderilecek ihtarname | ... |
| Mahkemeye sunulacak dilekçe | ... |
| Noter onay gerektiren işlem | ... |
| Acil ihtiyati tedbir / ihtiyati haciz talebi | ... |
| 100.000 TL altı sözleşme imzası | ... |
| 100.000 TL – 1.000.000 TL sözleşme | ... |
| 1.000.000 TL üstü sözleşme | ... |
| Aleyhe çıkmış BAM kararına temyiz başvurusu | ... |
| AYM bireysel başvuru | ... |
| AİHM başvurusu | ... |

### Adım 7 — Yetkili Mahkeme Tercihleri

| Konu | Tercih edilen yer |
|---|---|
| Fikri ve sınai haklar hukuk mahkemesi | (örn. İstanbul Anadolu / Avrupa, Ankara, İzmir) |
| İş mahkemesi | ... |
| Tüketici mahkemesi | ... |
| Asliye ticaret | ... |
| Asliye hukuk | ... |
| Aile mahkemesi | ... |
| İdare mahkemesi | ... |
| Sulh ceza hâkimliği (5651 m.9 başvurularda) | ... |
| BAM dairesi tercihi (varsa) | (örn. İstanbul BAM 16. HD — FSEK/SMK ihtisas) |

### Adım 8 — Standart Pozisyonlar (Sözleşme & NDA)

#### Sorumluluk sınırlaması (TBK m.115 emredici sınır göz önüne)
- Tercih: ... (örn. 12 aylık fatura tutarı)
- Kabul: ... (örn. 6-24 ay aralık)
- Yükselt: ... (örn. sınırsız sorumluluk, dolaylı zarar dahil)

#### Tazminat & sorumluluk
- Karşılıklı tazminat: standart / değil
- Tek taraflı tazminat: kabul edilebilir / yükselt

#### Fikri haklar (FSEK m.48-52)
- Mali hakların ayrı sayımı: zorunlu
- Manevi haklar: devredilemez; sadece kullanım yetkisi
- İleride yapılacak eserler: 3 yıl üst sınır (FSEK m.51)

#### Veri koruma
- KVKK ek protokolü: kişisel veri içeren tüm sözleşmelerde zorunlu
- Veri ihlali bildirimi: 72 saat (KVKK m.12 + Kurul kararları)

#### Süre & fesih
- Tercih: 1 yıllık, 30 gün ön bildirimle bedelsiz fesih
- Otomatik yenileme: yükselt

#### Uygulanacak hukuk & uyuşmazlık çözümü
- Tercih: Türk hukuku
- Mahkeme tercihi: ...
- Tahkim: ISTAC / ICC kabul; başka: değerlendir

#### NDA standart pozisyonları
- Tip: karşılıklı tercih edilir
- Süre: 2-3 yıl (ticari sırlar için 5+)
- Rekabet etmeme / çalışan ayartmama: NDA içinde kabul edilmez

### Adım 9 — MCP & Veritabanı Bağlantıları

#### `hukuk-rag` koleksiyon eşleştirme

`hukuk-rag` üzerinde kayıtlı koleksiyonlarını çağır:

```
mcp__hukuk-rag__hukuk_rag_koleksiyonlar()
```

Her koleksiyon için sor:
- Hangi davaya ait?
- Aktif mi, arşivde mi?
- Default koleksiyon olarak hangisi kullanılsın?

#### `yargi_mcp` tercih edilen daireler

| Konu | Tercih edilen daire |
|---|---|
| FSEK/SMK | Yargıtay 11. HD (eski; daire yapısı doğrulanmalı `yargi_mcp.search`) |
| İş hukuku | Yargıtay 9. HD (22. HD kapatıldı) |
| Ticari işler | Yargıtay 11. HD veya 13. HD |
| Tüketici | Yargıtay 13. HD |
| Borçlar | Yargıtay 3. HD veya 4. HD |
| İcra | Yargıtay 12. HD |
| KVKK | KVKK Kurulu kararları (`search_kvkk_decisions`) |
| Rekabet | Rekabet Kurumu (`search_rekabet_kurumu_decisions`) |
| Anayasal şikâyetler | AYM (`search_anayasa_unified`) |

#### `mevzuat_mcp` favori kanun referansları

Skill'lerin sıklıkla taradığı kanun numaraları:
- 5846 (FSEK)
- 6769 (SMK)
- 6098 (TBK)
- 6102 (TTK)
- 6100 (HMK)
- 6698 (KVKK)
- 5651 (İnternet)
- 4857 (İş K.)
- 6502 (TKHK)
- 2577 (İYUK)
- 5237 (TCK)
- 5271 (CMK)
- 2004 (İİK)
- 4721 (TMK)
- 4054 (Rekabet)
- 1136 (Avukatlık)
- 6325 (Arabuluculuk)

### Adım 10 — Tohum Belgeler (Önerilir)

Mümkünse şu örnekleri yükle (bürünün stilini öğrenmek için):
- 1 adet imzalanmış sözleşme örneği
- 1 adet daha önce gönderilmiş ihtarname
- 1 adet dava dilekçesi (kazandığın veya kaybettiğin)
- Büro standart antet/imza bloğu

Bu belgelere `hukuk-rag` üzerinden referans verilecek.

### Adım 11 — Profil Dosyasını Yaz

Toplanan tüm bilgi `~/.claude/plugins/config/turk-hukuk-legal/CLAUDE.md` dosyasına yazılır.

Eğer kullanıcı ayrı tutmak istiyorsa, alternatif yol:
- Claude Code: çalışma dizinindeki `.claude/CLAUDE.md`
- Cowork: paylaşılan klasördeki `buro.local.md`

#### Profil dosyasının yapısı

`meta/CLAUDE-TEMPLATE.md` dosyasına bakın (bu repodaki şablon).

### Adım 12 — Doğrulama

Profil yazıldıktan sonra **kısa bir doğrulama testi** yap:

> "Profili kaydettim. Şimdi bir test sorusu: müvekkiline bir ihtarname taslağı hazırlamamı söylersen, varsayılan saldırganlık tonunu **{ton}**, varsayılan onay matrisini **{karar verici}** olarak kullanacağım. Doğru mu?"

Kullanıcı onaylarsa kurulum tamam. Onaylamazsa ilgili adıma geri dön.

## Output

```markdown
## Soğuk Başlangıç Mülakatı Tamamlandı ✓

**Profil dosyası:** `~/.claude/plugins/config/turk-hukuk-legal/CLAUDE.md`

### Özet
- Büro: ...
- Uzmanlık: ...
- Pratik tarafı: ...
- Saldırganlık tonu: ...
- Yetkili mahkeme tercihleri: ...
- `hukuk-rag` default koleksiyonu: ...

### Bağlı MCP'ler
- mevzuat_mcp: ✓
- yargi_mcp: ✓
- hukuk-rag: ✓ ({n} koleksiyon)

### Sonraki adımlar
1. Bir gerçek senaryo seç: `/turk-hukuk-legal:<skill>`
2. Profil eksik kalan alanlar zamanla doldurulacak.
3. Profili güncellemek için bu mülakatı tekrar çalıştır veya doğrudan dosyayı düzenle.

### Hızlı testler
- Sözleşme inceleme: `/turk-hukuk-legal:sozlesme-inceleme`
- KVKK uyumu: `/turk-hukuk-legal:uyum-kontrol`
- HMK dilekçe: `/turk-hukuk-legal:dilekce-ihtarname`
- Fikri haklar tecavüz triyajı: `/turk-hukuk-legal:tecavuz-triyaj`
```

## Notlar

- Profil canlı bir dosyadır; deneyim arttıkça güncellenmelidir.
- Hassas bilgi (müvekkil isimleri, dosya numaraları, finansal veriler) **profilde tutulmaz** — onlar her vaka için ayrı paylaşılır.
- Plugin sürümü değiştiğinde profil migrasyon gerekebilir; `meta/CHANGELOG.md`'ye bakın.
