# Context7'ye Proje Ekleme

Context7, geliştiricilerin doğrudan kodlama ortamında güncel dokümantasyona erişebilmesi için favori kütüphanelerinizi ve framework’lerinizi eklemenize olanak tanır.

## Hızlı Gönderim

Bir kütüphane eklemenin en kolay yolu web arayüzümüzü kullanmaktır:

[**Kütüphane Gönder →**](https://context7.com/add-library?tab=github)

Yapmanız gereken tek şey GitHub depo adresini vermek. Context7, projenizin dokümantasyonunu otomatik olarak analiz edip indeksleyecektir.

## `context7.json` ile Gelişmiş Yapılandırma

Kütüphanenizin Context7 tarafından nasıl analiz edileceği ve sunulacağı üzerinde daha fazla kontrol sahibi olmak istiyorsanız, depo kök dizinine bir `context7.json` dosyası ekleyebilirsiniz. Bu dosya, `robots.txt` benzeri çalışır ve Context7’ye projenizi nasıl ele alacağını bildirir.

### Yapılandırma Alanları

Tüm seçenekleri içeren örnek bir `context7.json` dosyası:

```json
{
  "$schema": "https://context7.com/schema/context7.json",
  "projectTitle": "Upstash Ratelimit",
  "description": "Upstash Redis tabanlı hız sınırlama kütüphanesi",
  "folders": [],
  "excludeFolders": ["src"],
  "excludeFiles": [],
  "rules": ["Veritabanı olarak Upstash Redis kullanın", "Tek bölge kurulumu kullanın"],
  "previousVersions": [
    {
      "tag": "v1.2.1",
      "title": "sürüm 1.2.1"
    }
  ]
}
```

> **💡 İpucu**: `$schema` alanını dahil etmek, VS Code gibi modern kod editörlerinde otomatik tamamlama, doğrulama ve ipuçları sağlar; yapılandırmanızı oluşturmayı ve sürdürmeyi kolaylaştırır.

#### Alan Açıklamaları

- `projectTitle` (string): Context7’de projeniz için görünen isim. Varsayılan depo adını geçersiz kılar.

- `description` (string): Kütüphanenizin ne işe yaradığını kısaca açıklayın. Kod ajanlarının projenizin amacını anlamasına yardımcı olur.

- `folders` (array): Dokümantasyon analizinde dahil edilecek klasör yolları. Boş bırakılırsa Context7, tüm depoda ilgili dökümanları arar. Regex desenleri desteklenir ve tam yol gerektirir.

- `excludeFolders` (array): Analizden hariç tutulacak klasör yolları. Kaynak kodu, derleme klasörleri veya dokümantasyon dışı içerikleri hariç tutmak için kullanılır. Regex desenleri desteklenir ve tam yol gerektirir.

- `excludeFiles` (array): Analizden hariç tutulacak dosya adları. Sadece dosya adı (yol olmadan) belirtilmelidir. Örneğin, `CHANGELOG.md`, lisans veya yalnızca kod ajanları için alakasız olabilecek dosyaları hariç tutmak için kullanılır. Regex desteklenmez.

- `rules` (array): Kütüphanenizi kullanırken kod ajanlarının uyması gereken en iyi uygulamalar veya önemli kurallar. Bunlar, ajanlara sunulan dokümantasyon bağlamında öneri olarak görünür.

- `previousVersions` (array): Kütüphanenizin Context7’de erişilebilir olmasını istediğiniz önceki sürümleri.

  - `tag`: Git etiketi veya sürüm tanımlayıcı
  - `title`: İnsan tarafından okunabilir sürüm ismi

### Varsayılan Hariç Tutmalar

Eğer `context7.json` içinde `excludeFiles` veya `excludeFolders` belirtmezseniz, Context7 şu varsayılan desenleri kullanır:

#### Varsayılan Hariç Tutulan Dosyalar

```
CHANGELOG.md, changelog.md, CHANGELOG.mdx, changelog.mdx
LICENSE.md, license.md
CODE_OF_CONDUCT.md, code_of_conduct.md
```

#### Varsayılan Hariç Tutulan Klasörler

```
*archive*, *archived*, old, docs/old, *deprecated*, *legacy*
*previous*, *outdated*, *superseded*
i18n/zh*, i18n/es*, i18n/fr*, i18n/de*, i18n/ja*, i18n/ko*
i18n/ru*, i18n/pt*, i18n/it*, i18n/ar*, i18n/hi*, i18n/tr*
i18n/nl*, i18n/pl*, i18n/sv*, i18n/vi*, i18n/th*
zh-cn, zh-tw, zh-hk, zh-mo, zh-sg
```

Bu varsayılanlar, kod ajanlarının güncel ve teknik olarak ilgili dokümantasyona erişmesini, eski veya teknik olmayan içeriklerden korunmasını sağlar.

## Kimler Yapılandırma Ekleyebilir?

- **Kütüphane yazarları**: `context7.json` dosyasını doğrudan deponuza ekleyebilirsiniz
- **Katkıda bulunanlar**: Yapılandırma eklemek veya güncellemek için pull request gönderebilirsiniz
- **Topluluk üyeleri**: Popüler kütüphanelerin daha iyi analiz edilmesi için iyileştirme önerileri sunabilirsiniz

## En İyi Uygulamalar

1. **Açıklamaları kısa tutun**: Kütüphanenizin amacını ajanlara net şekilde anlatan bir cümle yeterli
2. **Alakasız klasörleri hariç tutun**: Kaynak kodu, test veya derleme çıktıları gibi klasörleri excludeFolders ile dışlayın
3. **Faydalı kurallar ekleyin**: Kod üretirken dikkat edilmesi gereken önemli noktaları veya ipuçlarını ekleyin
4. **Sürüm geçmişini koruyun**: Eski API’lere ihtiyaç duyabilecek projeler için önceki önemli sürümleri erişilebilir tutun

## Sürüm Ekleme

Mevcut kütüphanenize yeni bir sürüm eklemek için:

1. `context7.json` **dosyasına yeni sürüm ekleyin**: `previousVersions` dizisine yeni sürümünüzü ekleyin:

   ```json
   "previousVersions": [
     {
       "tag": "v2.0.0",
       "title": "sürüm 2.0.0"
     }
   ]
   ```

   > **Not**: `tag` değeri, GitHub deponuzda var olan bir Git etiketiyle tam olarak eşleşmelidir.

2. **Kütüphanenizi yenileyin**: Context7’de kütüphane sayfanıza gidin ve yeni sürümün indekslenmesi için yenileme işlemi başlatın.

## Yardıma mı ihtiyacınız var?

Projelerinizi eklerken bir sorun yaşarsanız veya yardıma ihtiyacınız olursa, lütfen [bir sorun bildirin](https://context7.com/add-library?tab=github) veya topluluğumuza ulaşın.
