# ATS Uyumlu CV

CV bilgileri [cv.yaml](cv.yaml) formunda. Formu doldur, sonra derle:

```
python build.py
```

Çıktılar `cikti/` klasörüne yazılır:

| Dosya | Ne için |
|---|---|
| `cv_tolgahan_keles.pdf` | Başvurularda kullanılacak ana dosya |
| `cv_tolgahan_keles.docx` | "Word yükleyin" diyen portallar için (Kariyer.net, Workday vb.) |
| `cv_tolgahan_keles_ats_metin.txt` | ATS'nin PDF'ten okuyacağı düz metin. Kontrol için buna bak |
| `cv_tolgahan_keles.html` | Ara dosya (PDF bundan üretilir) |

Gereksinimler: Python 3, Chrome veya Edge (PDF için) ve `pip install -r requirements.txt`.

## Form yapısı

```yaml
genel_bilgiler:
  ad_soyad: ...
  unvan: ...
  fotograf: vesikalık.jpg      # silersen fotoğrafsız CV
  sehir: / telefon: / email: / github: / linkedin: / web:

ozet: >
  Çok satırlı metin...

is_deneyimi:                   # her "- " yeni bir iş
  - pozisyon: ...
    kurum: ...
    baslangic: 09/2025
    bitis: Devam Ediyor
    maddeler:
      - ...

egitim:       [derece, bolum, okul, baslangic, bitis, ortalama, maddeler]
yayinlar:     [baslik, yazarlar, yayin_yeri, yil, link, kod]
projeler:     [isim, baslangic, bitis, linkler (liste), maddeler]
beceriler:    Kategori Adı: [a, b, c]
diller_ve_sinavlar: [ad, sonuc]
sertifikalar: [ad, kurum, yil]
referanslar:  [ad, unvan, kurum, email, telefon]
```

- Bölümler CV'de bu sırayla çıkar. Boş bırakılan ya da silinen alan/bölüm görünmez.
- `#` ile başlayan satırlar yorumdur. Bir şeyi geçici gizlemek için başına `#` koy.
- Girinti boşlukla yapılır (TAB değil). Değerin içinde `: ` varsa çift tırnağa al.
- Zorunlu bir alan eksikse ya da girinti bozuksa `build.py` hangi kayıt/satır olduğunu söyler.
- Maddelerde `**kalın**` çalışır. `github.com/...`, `https://...` ve e-postalar otomatik tıklanabilir olur.
  ATS görünen metni okuduğu için adresleri açık yazmak en iyisi.
- Görünümü değiştirmek istersen `style.css` (PDF) dosyasını düzenle.

## ATS için uyulan kurallar

- Tek sütun, tablo / metin kutusu / ikon yok. Fotoğraf metin akışının dışında, ATS metnini etkilemiyor
- Standart bölüm başlıkları (İş Deneyimi, Eğitim, Beceriler...)
- Tarihler tek formatta: `AA/YYYY – AA/YYYY`
- Seçilebilir gerçek metin, standart yazı tipi (Calibri), ligatür kapalı (Türkçe karakterler bozulmadan okunur)
- DOCX'te bölümler gerçek Word başlık stilleriyle (Heading 1/2) işaretli
