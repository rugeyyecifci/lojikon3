# Lojikon

Lojistik firması için geliştirilmiş, veritabanındaki kayıtları web tabanlı bir arayüz üzerinden görüntülemeyi, filtrelemeyi, aramayı ve yönetmeyi sağlayan bir ASP.NET Core MVC uygulaması.

Uygulama, firmanın MySQL veritabanındaki log ve durum kayıtlarını çeker; kullanıcıların bu kayıtlar arasında hızlıca arama yapmasını, istedikleri alanlara göre filtrelemesini ve sonuçları Excel'e aktarmasını sağlar.

## Özellikler

- **Kayıt listeleme:** Veritabanındaki kayıtlar tablo görünümünde listelenir.
- **Arama ve filtreleme:** Adres, detay, durum, seviye, tip, hata kodu gibi alanlara göre filtreleme; hangi alanların filtrede kullanılacağı onay kutularıyla seçilebilir.
- **Filtre seçenekleri yönetimi (Admin paneli):** Filtrelerde kullanılan seçenekler web arayüzünden eklenebilir, düzenlenebilir ve silinebilir.
- **Excel'e aktarma:** Filtrelenmiş sonuçlar tek tıkla `.xlsx` dosyası olarak indirilebilir.
- **Kayıt silme:** Kayıtlar onay penceresiyle tekil ya da toplu olarak silinebilir.

## Görüntülenen alanlar

| Alan | Açıklama |
|------|----------|
| ID | Kayıt numarası |
| AddressId / AddressName | Adres kimliği ve adı |
| DetailId / DetailName | Detay kimliği ve adı |
| AddressIndex | Adres sırası |
| LogTime | Kaydın zamanı |
| LogText | Kayıt metni |
| UnicID | Benzersiz kimlik |
| GState / GLevel / GType | Durum, seviye ve tip bilgileri |
| ErrorID / ErrorInfo | Hata kodu ve açıklaması |
| UpdateState | Güncelleme durumu |

## Kullanılan teknolojiler

- **.NET 8** / **ASP.NET Core MVC** (Razor görünümleri)
- **Entity Framework Core** + **Pomelo.EntityFrameworkCore.MySql**
- **MySQL**
- **ClosedXML** (Excel çıktısı)
- **Bootstrap** (arayüz)

## Sayfalar

| Adres | Açıklama |
|-------|----------|
| `/` veya `/Log` | Kayıt listesi, arama, filtreleme ve Excel'e aktarma |
| `/Admin` | Filtre seçeneklerinin listesi |
| `/Admin/Create` | Yeni filtre seçeneği ekleme |
| `/Admin/Edit/{id}` | Filtre seçeneği düzenleme |

## Kurulum ve çalıştırma

### Gereksinimler

- [.NET 8 Runtime (ASP.NET Core)](https://dotnet.microsoft.com/download/dotnet/8.0)
- MySQL sunucusu

### Veritabanı bağlantısı

`appsettings.json` dosyasındaki bağlantı cümlesini kendi veritabanı bilgilerinize göre düzenleyin:

```json
"ConnectionStrings": {
  "DefaultConnection": "server=localhost;database=plclog;user=KULLANICI;password=SIFRE;"
}
```

Uygulama ilk çalıştığında gerekli tablolar yoksa otomatik olarak oluşturulur.

### Çalıştırma

Windows'ta:

```bash
WebApplication3.exe
```

ya da herhangi bir platformda:

```bash
dotnet WebApplication3.dll
```

Ardından tarayıcıdan konsolda yazan adrese (ör. `http://localhost:5000`) gidin.

IIS üzerinde yayınlamak için klasördeki `web.config` dosyası hazırdır; klasörü bir IIS sitesine yönlendirmeniz yeterlidir.

## Proje yapısı

Bu depo, uygulamanın yayınlanmış (publish) halini içerir:

- `WebApplication3.dll` / `WebApplication3.exe` – uygulamanın kendisi
- `appsettings.json` – yapılandırma ve veritabanı bağlantısı
- `web.config` – IIS yapılandırması
- Diğer `.dll` dosyaları – uygulamanın bağımlılıkları
