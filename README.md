# Şifre Kasası

Windows için kişisel hesap ve şifre yöneticisi. Hesap adı, kullanıcı adı, şifre
ve notlarınızı **yalnızca kendi bilgisayarınızda, şifreli olarak** saklar;
arama, rastgele şifre üretici, panoya kopyalama ve yedek alma / geri yükleme
özellikleri sunar.

- **Güvenlik:** Ana şifre PBKDF2 (600.000 iterasyon, SHA-256) ile doğrulanır;
  hesap adları, kullanıcı adları, şifreler ve notlar ana şifreden türetilen
  **AES-256** anahtarıyla şifrelenir. Ne veritabanında ne de yedek dosyasında
  düz metin bilgi bulunmaz.
- **Çevrimdışı:** Verileriniz buluta gönderilmez; kendi bilgisayarınızdaki
  SQL Server'da tutulur.

## İndirme ve kurulum

1. [Releases](https://github.com/selimdemir/sifre-kasasi/releases) sayfasına gidin.
2. En son sürümün altındaki **Assets** bölümünden iki dosyayı birlikte indirin:
   - `SifreKasasi.exe` — program
   - `SifreKasasi.exe.config` — ayar dosyası
3. İki dosyayı birlikte bir klasöre kopyalayın (ör. `C:\SifreKasasi`) ve
   `SifreKasasi.exe` dosyasını çalıştırın. Kurulum gerekmez.

> Tarayıcı / Windows "tanınmayan uygulama" uyarısı verebilir; program imzasız
> olduğu için bu uyarı normaldir.

## Gereksinimler

| Gereksinim | Açıklama |
|---|---|
| Windows 10 / 11 | .NET Framework 4.8 Windows'ta hazır kurulu, ek kurulum gerekmez |
| SQL Server | **LocalDB** (en hafif) veya **SQL Server Express** (ücretsiz) |

Veritabanı ve tablolar **ilk çalıştırmada otomatik oluşturulur**; SQL bilgisi
gerektirmez. Bağlantı ayarı gerekirse uygulama kendi ayar penceresini açar
(LocalDB: `(localdb)\MSSQLLocalDB`, Express: `.\SQLEXPRESS`).

## İlk çalıştırma

1. Uygulamayı açın, **ana şifrenizi** belirleyin.
2. Bu şifre hem girişte sorulur hem de kayıtlarınızın şifrelenme anahtarıdır.
   **Unutulursa kayıtlar kurtarılamaz — mutlaka not alın.**

## Güncelleme (yeni sürüm kurma)

1. [Releases](https://github.com/selimdemir/sifre-kasasi/releases) sayfasından
   yeni sürümün iki dosyasını indirin.
2. Uygulama kapalıyken eski `SifreKasasi.exe` ve `SifreKasasi.exe.config`
   dosyalarının üzerine yeni dosyaları kopyalayın.
3. Programı açın — kayıtlarınız aynen yerinde kalır (veriler veritabanında
   saklandığı için exe'yi değiştirmek onlara dokunmaz).

## Yedekleme

- *Dosya → Yedek Al* (`Ctrl+S`): program klasörüne tarihli `.json` yedek alır
  (içeriği şifrelidir).
- Yedeği düzenli olarak **bilgisayar dışına** (USB / harici disk) kopyalayın.
- **Format sonrası:** Windows + SQL Server kurun → programı kopyalayın →
  *Dosya → Yedeği Geri Yükle* → yedeği aldığınız andaki ana şifreyi girin.

## Sorun giderme

- **"Bağlantı kurulamadı"** → *İşlemler → Veritabanı Bağlantı Ayarları* →
  sunucu adını kontrol edin, "Bağlantıyı Test Et" ile deneyin.
- **Detaylı hata kaydı** → `%AppData%\SifreKasasi\log.txt`
- **Ana şifremi unuttum** → Tasarım gereği kurtarma yoktur; yedeğinizi ve
  şifrenizi güvenli biçimde saklamak esastır.
