# Türk Hukuku Legal Plugin

Anthropic'in `knowledge-work-plugins/legal` plugin'inin Türk hukukuna **yeniden yazılmış** versiyonu. Mimari ve iş akışı modelini koruyup içeriği Türk mevzuatına göre sıfırdan kurar (TBK, TTK, HMK, KVKK, FSEK, SMK, İYUK, İş K., TKHK). Üzerine **fikri ve sınai haklar paketi** eklenmiştir — Anthropic'in temel `legal` plugin'inde olmayan ama Türk pratiğinde merkezi olan bir alan.

## Skill Listesi

### Çekirdek hukuk

| Skill | Komut | Konu |
|---|---|---|
| Sözleşme inceleme | `/turk-hukuk-legal:sozlesme-inceleme` | Müzakere kılavuzuna göre madde madde inceleme — TBK/TTK eksenli |
| Gizlilik sözleşmesi triyajı | `/turk-hukuk-legal:gizlilik-sozlesmesi-triyaj` | Yeşil/Sarı/Kırmızı sınıflandırma — TBK m.26-27 + TTK m.54-63 süzgeci |
| Uyum kontrolü | `/turk-hukuk-legal:uyum-kontrol` | KVKK + sektörel (BDDK, EPDK, KVKK Kurul Kararları, vb.) |
| Hukuki yazışma | `/turk-hukuk-legal:hukuki-yazisma` | KVKK ilgili kişi başvurusu yanıtı, ihtarname yanıtı, KEP bildirimi şablonları |
| Risk değerlendirme | `/turk-hukuk-legal:risk-degerlendirme` | Önem × olasılık matrisi + eskalasyon kuralları |
| Toplantı brifingi | `/turk-hukuk-legal:toplanti-brifingi` | Müzakere, duruşma, yönetim kurulu, denetim toplantıları için ön çalışma |
| Tedarikçi kontrol | `/turk-hukuk-legal:tedarikci-kontrol` | Sözleşme envanteri, eksik belgeler, yenileme tarihleri |
| Brifing | `/turk-hukuk-legal:brifing` | Günlük / konu / olay brifingi |
| KEP & e-imza akışı | `/turk-hukuk-legal:imza-akisi` | İmzaya hazır belge öncesi kontrol listesi, KEP/ıslak imza/e-imza tercihi |

### Fikri ve sınai haklar paketi

| Skill | Komut |
|---|---|
| Marka tescil ön araştırması | `/turk-hukuk-legal:marka-tescil-on-arastirma` |
| FSEK & SMK ihtarnamesi | `/turk-hukuk-legal:ihtarname-fsek-smk` |
| İçerik kaldırma bildirimi | `/turk-hukuk-legal:icerik-kaldirma-bildirim` |
| Tecavüz triyajı | `/turk-hukuk-legal:tecavuz-triyaj` |
| Fikri haklar klozu inceleme | `/turk-hukuk-legal:fikri-haklar-klozu-inceleme` |
| Patent serbestlik analizi | `/turk-hukuk-legal:patent-serbestlik-analizi` |
| Açık kaynak uyumu | `/turk-hukuk-legal:acik-kaynak-uyum` |
| Portföy takibi | `/turk-hukuk-legal:portfoy-takip` |
| HMK uyumlu dilekçe & ihtarname | `/turk-hukuk-legal:dilekce-ihtarname` |

## Konfigürasyon

Yerel ayarlarını `buro.local.md` dosyasına yaz (Cowork'te paylaşılan klasör; Claude Code'da `.claude/`):

```markdown
# Büro Kılavuzu

## Sözleşme inceleme standart pozisyonları

### Sorumluluk sınırlaması (TBK m.115 vd. — emredici hükümler hariç)
- Tercih: 12 aylık fatura tutarı toplamı
- Kabul edilebilir: 6–24 ay
- Yükselt: sınırsız sorumluluk, dolaylı zararların dahil edilmesi

### Tazminat & sorumluluk
- Karşılıklı tazminat klozu standart
- Tek taraflı tazminat → yükselt

### Fikri haklar
- Mali hakların ayrı ayrı sayımı zorunlu (FSEK m.52)
- Manevi haklar devredilemez; sadece kullanım yetkisi (FSEK m.16-19)

### Veri koruma
- KVKK ek protokolü zorunlu (kişisel veri içeren her işleme için)
- KEP ile veri ihlali bildirimi 72 saat içinde

### Süre & fesih
- 1 yıllık dönem, 30 gün ön bildirimle bedelsiz fesih hakkı standart
- Otomatik yenileme → yükselt

### Uygulanacak hukuk
- Tercih: Türk hukuku
- Tahkim: ISTAC, MTK, ICC kabul edilir; başka yargı yerleri → yükselt

## Yetki onay matrisi
- 100.000 TL altı: yönetici
- 100.000 TL – 1.000.000 TL: hukuk müşaviri
- 1.000.000 TL üstü: Yönetim Kurulu

## KVKK
- VERBİS kaydı güncel: [evet/hayır]
- DPIA tetikleyiciler: özel nitelikli veri, biyometrik, çocuk verisi, yüksek hacim
- İlgili kişi başvurusu yanıt süresi: 30 gün (KVKK m.13)

## İhtisas alanları
- [ ] Fikri ve sınai haklar
- [ ] Ticari sözleşmeler
- [ ] KVKK
- [ ] İş hukuku
- [ ] vb.
```

## MCP Bağımlılıkları

| MCP | Görev |
|---|---|
| `mevzuat_mcp` | Kanun, KHK, CBK, yönetmelik, tebliğ |
| `yargi_mcp` | Yargıtay, Danıştay, AYM, BAM, KVKK, Rekabet, Sayıştay kararları |
| `hukuk-rag` | Büroya özel dava dosyaları üzerinde semantik arama |
| KEP gönderim MCP (varsa) | Resmi tebligat |
| Bulut depolama | Sözleşme arşivi |
| Takvim | Duruşma & süre takibi |

## Kurulum

```bash
# Claude Code
/plugin marketplace add <yol>
/plugin install turk-hukuk-legal@<marketplace>

# Veya Cowork
# Customize → Browse plugins → Upload custom plugin file (bu dizini zip'le)
```

## Önemli Uyarılar

Plugin çıktıları taslaktır. Mevzuat ve içtihat referansları her kullanımda `mevzuat_mcp` ve `yargi_mcp` üzerinden güncel metne göre doğrulanmalıdır. Süreler, hak düşürücü ve zamanaşımı süreleri için her zaman mevzuatın güncel metnine başvurulmalıdır.

## Lisans

Apache 2.0. Üst proje: [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins) — Apache 2.0, Anthropic.
