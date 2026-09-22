# Pinova — Özellikler ve Kurulum Kılavuzu

> Bu belge, **Pinova** (tam otomatik e-pin / dijital ürün satış scripti) yazılımının özelliklerini ve kurulum adımlarını özetler.
> Canlı demo: **[pinova.epinsoft.com.tr](https://pinova.epinsoft.com.tr)** · Satın alma: **pazarlama@epinsoft.com.tr**

---

## 1. Ürün Özeti

**Pinova**, oyun e-pini, oyun kodu, hediye kartı, oyun parası ve her türlü **dijital ürünü otomatik teslimatla** satmak için tasarlanmış, hazır ve satışa uygun bir **e-pin satış yazılımıdır** (PHP).

Müşteri ödemeyi tamamladığı anda stok kodu **saniyeler içinde otomatik** olarak teslim edilir — manuel işlem gerekmez. Tek panelden yönetilen, **tek-satıcılı** (kendi mağazanız) bir dükkân modelidir.

**Kimler için:** Kendi e-pin / dijital ürün satış sitesini kurmak isteyen girişimciler, bayiler ve dijital ürün satıcıları.

**Örnek kullanım senaryoları:** Steam key, PUBG UC, Valorant VP, Minecraft, PlayStation kodları, hediye kartları, oyun parası ve benzeri anında-teslim dijital ürünler.

---

## 2. Özellikler

### 2.1 Otomatik Teslimat & Stok
| Özellik | Açıklama |
|---|---|
| Anında otomatik teslimat | Ödeme onaylandığı an stok kodu müşteriye otomatik iletilir. |
| AES şifreli stok | Stok kodları veritabanında **şifreli** saklanır; sızıntı riski azaltılır. |
| Stok yönetimi | Ürün başına stok havuzu; tükenince otomatik "stokta yok" durumu. |
| Sipariş & fatura kaydı | Her satış kayıt altında; müşteriye teslim edilen kod izlenebilir. |

### 2.2 Cüzdan & Ödeme
| Özellik | Açıklama |
|---|---|
| Bakiye (cüzdan) sistemi | Müşteriler bakiye yükleyip bakiyeden alışveriş yapabilir. |
| Çoklu ödeme geçidi | Birden fazla ödeme sağlayıcısı desteklenir (bkz. 4.6 — kendi POS'unuzu bağlarsınız). |
| Bakiye yükleme akışı | Ödeme geçidi üzerinden güvenli bakiye yükleme. |

### 2.3 Bayilik (Reseller)
| Özellik | Açıklama |
|---|---|
| Bayi fiyatlandırma | Bayilere özel indirimli fiyatlar tanımlanabilir. |
| Bayi paneli | Bayiler için ayrı yönetim/sipariş görünümü. |

### 2.4 İçerik & Pazarlama
| Özellik | Açıklama |
|---|---|
| AI blog otomasyonu | OpenAI / Gemini / Claude ile SEO odaklı blog içeriği üretimi. |
| SEO dostu | Arama motoru uyumlu URL yapısı ve içerik altyapısı. |
| Mobil uyumlu | Duyarlı (responsive) arayüz. |

### 2.5 Yönetici Paneli
| Özellik | Açıklama |
|---|---|
| Ürün / kategori yönetimi | Ürün, kategori, fiyat ve görsel yönetimi. |
| Stok yönetimi | Toplu stok ekleme; şifreli kod havuzu. |
| Sipariş & raporlar | Satış listesi, gelir raporları, müşteri kayıtları. |
| Kapsamlı yönetim | Onlarca yönetim sayfasıyla dükkânın tüm yönleri kontrol edilir. |

---

## 3. Teknik Mimari

| Katman | Teknoloji |
|---|---|
| Backend | PHP (CodeIgniter tabanlı MVC) |
| Veritabanı | MySQL / MariaDB |
| Önyüz | Duyarlı HTML/CSS/JS |
| Zamanlanmış işler | Cron (blog üretimi vb.) |
| Dağıtım | Paylaşımlı hosting / VPS; Cloudflare uyumlu |
| Önerilen PHP | 7.4+ (güncel sürüm önerilir) |

---

## 4. Kurulum ve Yapılandırma

> Aşağıdaki adımlar genel bir kurulum akışıdır. Gerçek erişim bilgileri (DB parolası, admin girişi, anahtarlar) teslim sırasında ayrıca iletilir.

### 4.1 Gereksinimler
- PHP 7.4+ (önerilen), MySQL/MariaDB
- Apache/LiteSpeed (`.htaccess` / URL yeniden yazma desteği)
- SSL sertifikası (HTTPS) — canlı ortam için önerilir

### 4.2 Dosyaların Yüklenmesi
```
# Kaynak kodu web köküne yükleyin (FTP/SFTP veya panel dosya yöneticisi)
# Örn. public_html/ ya da alan adı kök dizini
```

### 4.3 Veritabanı İçe Aktarma
```
# phpMyAdmin veya CLI ile şemayı içe aktarın
mysql -u KULLANICI -p VERITABANI < pinova.sql
```

### 4.4 Yapılandırma
- **base_url** (`config.php`): sitenizin tam adresi (örn. `https://ornek.com/`).
- **Veritabanı** (`database.php`): sunucu, kullanıcı, parola, veritabanı adı.
- **Şifreleme anahtarı** (`config.php`): `$config['encryption_key']` — güçlü, benzersiz bir değer atayın (stok kodları şifreli saklanır).

### 4.5 Cron Kurulumu
```
# AI blog üretimi vb. zamanlanmış işler (örnek — her 30 dakikada)
*/30 * * * * curl -s "https://ornek.com/cron/..." >/dev/null 2>&1
```

### 4.6 Ödeme Geçitleri (ÖNEMLİ — Satış Avantajı)
Pinova, ödeme geçitlerini **placeholder (boş credential)** olarak teslim eder. Yani:

- **Kendi ödeme sağlayıcı hesabınızı** (iyzico, Stripe, PayTR vb.) **admin panelden** bağlarsınız.
- Ödemeler doğrudan **sizin** POS/hesabınıza akar; aracı yoktur.
- Farklı ülke/sağlayıcıya kolayca uyarlanır.

> Demo ortamında ödeme geçitleri credential'sız olduğu için **demo modunda** çalışır; canlıya geçerken kendi anahtarlarınızı girersiniz.

### 4.7 İlk Kullanım
1. Admin paneline giriş yapın (giriş bilgileri teslimde iletilir).
2. Kategori ve ürünleri ekleyin.
3. Ürünlere stok (kod) yükleyin — kodlar şifreli saklanır.
4. Ödeme geçidi bilgilerinizi girin.
5. Test siparişiyle otomatik teslimatı doğrulayın.

---

## 5. Teslim Paketi

- Tam kaynak kod
- Veritabanı şeması
- Kurulum desteği
- Özellikler bu belgede özetlenmiştir; özel talepler için iletişime geçebilirsiniz.

---

## 6. İletişim

- 🌐 **Web:** [epinsoft.com.tr](https://epinsoft.com.tr)
- ✉️ **E-posta:** pazarlama@epinsoft.com.tr
- 📞 **Telefon:** +90 850 255 18 01
- ▶ **Canlı demo:** [pinova.epinsoft.com.tr](https://pinova.epinsoft.com.tr)
