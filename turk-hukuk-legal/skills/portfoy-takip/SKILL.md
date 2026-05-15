---
name: portfoy-takip
description: Marka, patent, faydalı model, tasarım tescil portföyünüzü yenileme, yıllık ücret, kullanım beyanı ve hak sahipliği değişikliği açısından takip eder. TPMK ücret tarifesi ve sürelerine göre yaklaşan deadline'ları çıkartır. (Mevzuat ve ücret tarifeleri her yıl güncellenir — TPMK güncel sayfasından teyit edilmelidir.)
---

# /fikri-sinai-haklar:portfoy-takip — Sınai Mülkiyet Portföy Takibi

## Koruma Süreleri (SMK 6769 — `mevzuat_mcp` ile doğrulanacak)

| Hak | Süre | Yenileme |
|---|---|---|
| Marka | 10 yıl | 10 yıllık periyotlarla sınırsız |
| Patent | 20 yıl | Yıllık ücretler — ödenmezse düşer |
| Faydalı model | 10 yıl | Yenilenemez |
| Tasarım | 5 yıl | 5'er yıllık 4 yenileme — toplam 25 yıl |
| Coğrafi işaret | Süresiz | Kullanım denetimi |

## Takip Kalemleri

1. **Yenileme tarihi** — koruma süresinin son tarihi, **6 ay önceden** uyarı
2. **Yıllık ücret (patent)** — TPMK ücret tarifesine göre yıllık yenilenir
3. **Kullanım zorunluluğu** — SMK m.9 (marka kullanımı 5 yıl içinde gerçekleştirilmezse iptal edilebilir)
4. **Devir / lisans bildirimleri** — TPMK siciline işlenmesi gereken işlemler
5. **Uluslararası tescil yenilemeleri** — WIPO Madrid (marka), PCT (patent)
6. **Karşı işlemler** — başkasının itirazları, hükümsüzlük davaları, Yargıtay temyiz süreleri

## İş Akışı

1. Mevcut portföy verisini al (TPMK sicil çıktısı, vekil tablosu)
2. Veritabanına işle (csv / büro CRM / dosya sistemi)
3. Yaklaşan süreleri sırala (6 ay, 3 ay, 1 ay, 1 hafta)
4. Aksiyonu öner (yenileme talimatı, ücret yatırma, kullanım kanıtı topla)
5. Müvekkile özetle raporla

## Zamanlanmış Ajan (Önerilir)

Bu skill bir **scheduled agent** olarak haftalık çalıştırılabilir:
- Pazartesi sabahı bütün portföyü tara
- Önümüzdeki 90 gün içinde dolacak haklar listesi
- Slack / e-posta'ya gönder

## Çıktı

```markdown
## Portföy Durum Raporu — [Tarih]

### 90 gün içinde dolacak haklar
| Hak | Numara | Sahibi | Son tarih | Aksiyon |
|---|---|---|---|---|

### Kullanım kanıtı gereken markalar (SMK m.9)
- ...

### Sicile işlenmesi geciken devir/lisans
- ...

### Bütçe etkisi
- TPMK yenileme ücretleri: ...
- Vekil ücretleri: ...
- Toplam: ...
```
