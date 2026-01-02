# Telegram Grup Yönetim Sistemi - Kullanım Kılavuzu

> **Kapsamlı kullanım kılavuzu, hata çözümleri ve en iyi pratikler**

## 📋 İçindekiler

1. [Kurulum ve İlk Ayarlar](#kurulum-ve-ilk-ayarlar)
2. [Hesap Yönetimi](#hesap-yönetimi)
3. [Grup İşlemleri](#grup-işlemleri)
4. [Üye Toplama (Scraper)](#üye-toplama-scraper)
5. [Üye Taşıma (Migration)](#üye-taşıma-migration)
6. [Toplu Mesaj Gönderme](#toplu-mesaj-gönderme)
7. [Paketler ve Limitler](#paketler-ve-limitler)
8. [Hata Çözümleri](#hata-çözümleri)
9. [İpuçları ve En İyi Pratikler](#ipuçları-ve-en-iyi-pratikler)
10. [SSS](#sss)

---

## 🚀 Kurulum ve İlk Ayarlar

### Sistem Gereksinimleri
- Python 3.8 veya üzeri
- Windows, Linux veya macOS
- Kararlı internet bağlantısı

### Kurulum Adımları

```bash
# 1. Repoyu klonlayın
git clone https://github.com/yourusername/telegram-manager.git
cd telegram-manager

# 2. Gerekli paketleri yükleyin
pip install -r requirements.txt

# 3. Uygulamayı başlatın
python app.py
```

### İlk Giriş

1. Tarayıcınızda `http://localhost:5000` adresine gidin
2. "Kayıt Ol" butonuna tıklayın
3. E-posta ve şifre ile hesap oluşturun
4. Giriş yapın

> ⚠️ **ÖNEMLİ:** İlk kayıt olan kullanıcı otomatik olarak **Admin** rolü alır.

---

## 👤 Hesap Yönetimi

### Telegram Hesabı Ekleme

#### Adım 1: API Bilgilerini Alın

1. [my.telegram.org](https://my.telegram.org) adresine gidin
2. Telegram hesabınızla giriş yapın
3. "API Development Tools" bölümüne tıklayın
4. Yeni bir uygulama oluşturun:
   - **App title:** İstediğiniz bir isim (örn: "MyApp")
   - **Short name:** Kısa bir isim (örn: "myapp")
   - **Platform:** Diğer platformlardan birini seçin
5. **API_ID** ve **API_HASH** değerlerini kaydedin

#### Adım 2: Hesabı Sisteme Ekleyin

1. Sol menüden **"Hesaplar"** sayfasına gidin
2. **"Hesap Ekle"** butonuna tıklayın
3. Formu doldurun:
   ```
   Telefon Numarası: +905551234567 (ülke kodu ile)
   API ID: 12345678
   API Hash: abcdef1234567890abcdef1234567890
   ```
4. **"Ekle"** butonuna tıklayın
5. Telegram'dan gelen doğrulama kodunu girin
6. İki faktörlü doğrulama varsa, şifrenizi girin

#### Olası Hatalar ve Çözümleri

**Hata:** "Invalid phone number"
- **Çözüm:** Telefon numarasını mutlaka `+` işareti ve ülke kodu ile girin. Örnek: `+905551234567`

**Hata:** "API_ID_INVALID"
- **Çözüm:** API ID'nin doğru olduğundan emin olun. Sayısal bir değer olmalı (örn: 12345678)

**Hata:** "SESSION_PASSWORD_NEEDED"
- **Çözüm:** Hesabınızda iki faktörlü doğrulama açık. Açılan pencereye şifrenizi girin.

**Hata:** "PHONE_CODE_INVALID"
- **Çözüm:** Telegram'dan gelen kodu yanlış girdiniz. Tekrar deneyin veya yeni kod isteyin.

---

## 📁 Grup İşlemleri

### Grupları Senkronize Etme

1. **"Gruplar"** sayfasına gidin
2. Üst kısımda hesap seçin
3. **"Grupları Senkronize Et"** butonuna tıklayın
4. Sistem otomatik olarak hesabınızdaki tüm grupları çeker

> 💡 **İpucu:** Düzenli olarak senkronizasyon yaparak grup listesini güncel tutun.

### Grup Listesi Oluşturma

Belirli grupları kolayca yönetmek için listeler oluşturabilirsiniz:

1. **"Grup Listeleri"** sayfasına gidin
2. **"Yeni Liste"** butonuna tıklayın
3. Liste adı verin (örn: "Aktif Gruplarım")
4. Gruba tıklayarak listeye ekleyin
5. **"Kaydet"** butonuna tıklayın

---

## 🔍 Üye Toplama (Scraper)

> ⚠️ **PAKET GEREKSİNİMİ:** Bu özellik sadece **Pro** ve **Enterprise** paketlerde mevcuttur.

### Grup Üyelerini Toplama

#### Adım 1: Scraper Sayfasına Gidin

1. Sol menüden **"Üye Toplama"** (Scraper) sayfasına gidin
2. Bir hesap seçin

#### Adım 2: Kaynak Grubu Belirleyin

Kaynak grubu 3 şekilde belirtebilirsiniz:

**1. Grup ID ile:**
```
-1001234567890
```

**2. Kullanıcı adı ile:**
```
@pythontr
```

**3. Davet linki ile:**
```
https://t.me/joinchat/xxxxx
```

#### Adım 3: Filtreleri Ayarlayın

- **Sadece Mesaj Gönderenler:** ✅ (Aktif üyeleri toplamak için önerilir)
- **Maksimum Üye Sayısı:** 500 (varsayılan)

#### Adım 4: Liste Oluşturun

1. **"Yeni Liste"** seçeneğini işaretleyin
2. Liste adı verin (örn: "Python TR Üyeleri")
3. **"Toplamayı Başlat"** butonuna tıklayın

### İşlem Takibi

1. Scraping başladığında **"Görevler"** sayfasına yönlendirilirsiniz
2. İşlem ilerlemesini gerçek zamanlı olarak görürsünüz
3. Tamamlandığında **"Üye Listeleri"** sayfasından listeyi görebilirsiniz

### Scraper Hataları ve Çözümleri

#### ❌ "ChatAdminRequiredError"
**Açıklama:** Üyeleri görüntülemek için admin yetkisi gerekiyor.

**Çözüm:**
- Gruptan admin yetkisi alın VEYA
- Genel üye listesi açık olan başka bir grup deneyin

#### ❌ "ChannelPrivateError"
**Açıklama:** Grup özel ve üye değilsiniz.

**Çözüm:**
- Önce gruba katılın
- Ardından scraping işlemini başlatın

#### ❌ "FloodWaitError"
**Açıklama:** Telegram hız sınırı uyguladı.

**Çözüm:**
- Sistem otomatik olarak bekler ve devam eder
- Sabırlı olun, işlem tamamlanacaktır

---

## 🚚 Üye Taşıma (Migration)

> ⚠️ **PAKET GEREKSİNİMİ:** Çoklu hesap özelliği için **Pro** veya **Enterprise** paketi gereklidir.

### Temel Üye Taşıma

#### Adım 1: Taşıma Sayfasına Gidin

1. **"Toplu İşlemler"** sayfasına gidin
2. **"Üye Taşıma"** sekmesine tıklayın

#### Adım 2: Kaynak Belirleyin

**Manuel ID:**
```
Kaynak Grup ID: -1001234567890
```

**VEYA Üye Listesi:**
- Daha önce oluşturduğunuz üye listesini seçin
- Bu yöntem daha hızlı ve güvenilirdir ✅

#### Adım 3: Hedef Grubu Belirleyin

**Tek Grup:**
```
Hedef Grup ID: -1009876543210
```

**VEYA Grup Listesi:**
- Birden fazla gruba aynı üyeleri eklemek için grup listesi seçin

#### Adım 4: Ayarları Yapın

**Flood (Hız Limiti) Ayarı:**
- **Skip (Atla):** ✅ Önerilen - Hız limitine takılan üyeleri atlar
- **Wait (Bekle):** Hız limiti bitene kadar bekler (çok yavaş)

**Çoklu Hesap (Pro+ için):**
- ✅ Aktif edin
- Kullanılacak ek hesapları seçin
- Böylece hız limitleri yayılır ve işlem hızlanır

#### Adım 5: Başlatın

1. **"Başlat"** butonuna tıklayın
2. **"Görevler"** sayfasından ilerlemeyi takip edin

### Migration Hataları ve Çözümleri

#### ❌ "The key is not registered in the system"
```
[20:17:56] Eklenemedi (6544340400): The key is not registered in the system
```

**Açıklama:** Kullanıcı ID'si geçersiz veya sistem tarafından tanınmıyor.

**Çözüm:**
- Bu hata tek kullanıcı bazlıdır, normal işleme devam eder
- Sorunu olan kullanıcı atlanır
- Endişelenmeyin, diğer kullanıcılar başarıyla eklenir

**Neden Olur:**
- Kullanıcı hesabını silmiş olabilir
- ID veritabanında eski/geçersiz olabilir
- Telegram kullanıcı bilgisini güncellememiş olabilir

#### ❌ "PeerFloodError" (En Yaygın Hata)
```
[13:31:14] ⚠️ Bu grup/kişi için kalıcı hız limiti (PeerFlood). Atlanıyor.
[13:31:14] Eklenemedi (2138291341): PeerFloodError
```

**Açıklama:** Telegram, hesabınızın çok fazla üye ekleme isteği gönderdiğini tespit etti ve geçici/kalıcı bir engel koydu.

**ÖZEL ÇÖZÜMLER:**

**1. Kısa Süreli Flood (Birkaç saat):**
- **Çözüm:** Birkaç saat bekleyin (genellikle 2-6 saat)
- Başka bir hesap kullanın
- Daha yavaş tempo ayarlayın

**2. Uzun Süreli Flood (24-48 saat):**
- **Çözüm:** 1-2 gün bekleyin
- Bu sürede hesabı normal kullanıcı gibi kullanın (mesaj atın, gruplara katılın)
- Eski hesaplar daha az flood yer (yeni hesap kullanmayın)

**3. Kalıcı Flood (PeerFlood):**
- **Çözüm:** 
  - Bu hesapla o gruba artık üye ekleyemezsiniz
  - Başka bir grup deneyin
  - Farklı bir hesap kullanın
  - Hesabı 1-2 hafta "aktif kullanıcı" gibi kullanın

**ÖNLEME YÖNTEMLERİ:**
- ✅ Çoklu hesap kullanın (yük dağılır)
- ✅ Günlük maksimum 50 üye ekleyin (hesap başına)
- ✅ İşlemler arası 30-60 saniye bekleyin
- ✅ Yeni hesaplar kullanmayın (minimum 1 ay eski)
- ✅ "Skip" modunu kullanın (flood olan kullanıcıyı atlar)

**Flood Seviyeleri:**
- 🟢 **10-20 üye/gün:** Güvenli
- 🟡 **30-50 üye/gün:** Orta risk
- 🔴 **50+ üye/gün:** Yüksek risk (flood garantisi)

#### ❌ "Could not find the input entity"
```
[13:13:21] Hata: Could not find the input entity for PeerChannel(channel_id=2688900567). 
Please read https://docs.telethon.dev/en/stable/concepts/entities.html
```

**Açıklama:** Telegram, verilen ID'ye ait grup/kanalı bulamamış.

**NEDEN OLUR:**
1. Grup ID'si yanlış yazılmış
2. Hesap o gruba hiç katılmamış
3. Grup silinmiş veya özel olmuş
4. Session cache'i eski

**ÇÖZÜM ADIMLARI:**

**1. ID'yi Doğrulayın:**
```
Yanlış:  2688900567
Doğru:   -1002688900567
```
> Kanal/Grup ID'leri `-100` ile başlamalı!

**2. Gruba Katılın:**
- Önce hesapla gruba manuel olarak katılın
- Ardından ID'yi tekrar deneyin

**3. Session'ı Yenileyin:**
- Hesapları senkronize edin
- "Grupları Senkronize Et" butonunu kullanın

**4. Davet Linki Kullanın:**
- ID yerine davet linki kullanmayı deneyin:
  ```
  https://t.me/joinchat/xxxxx
  ```

#### ❌ "UserPrivacyRestrictedError"
```
[15:45:12] Eklenemedi (123456789): UserPrivacyRestrictedError
```

**Açıklama:** Kullanıcının gizlilik ayarları, gruplara eklenmesini engelliyor.

**Çözüm:**
- Bu kullanıcı atlanır, normal bir durumdur
- Kullanıcının ayarlarını değiştiremezsiniz
- İşleme devam edin, diğer kullanıcılar eklenecektir

**Oran:** Genellikle kullanıcıların %5-10'u bu hatayı verir.

#### ❌ "UserNotMutualContactError"
```
Eklenemedi: UserNotMutualContactError
```

**Açıklama:** Kullanıcıyı eklemek için karşılıklı iletişim gerekiyor.

**Çözüm:**
- Atlanır, normal bir durumdur
- Telegram'ın spam önleme politikası
- Endişelenmeyin

#### ❌ "ChatWriteForbiddenError"
```
Hata: ChatWriteForbiddenError
```

**Açıklama:** Hedef grupta üye ekleme yetkisi yok.

**Çözüm:**
- Grupta admin olduğunuzdan emin olun
- "Add members" yetkisinin açık olduğunu kontrol edin
- Grup ayarlarından "Herkes üye ekleyebilir" seçeneğini kontrol edin

---

## 📨 Toplu Mesaj Gönderme

### Gruplara Mesaj Gönderme

#### Adım 1: Mesaj Sayfasına Gidin

1. **"Toplu İşlemler"** > **"Mesaj Gönderme"**
2. Hesap seçin

#### Adım 2: Hedef Belirleyin

**Tek Grup:**
```
Grup ID: -1001234567890
```

**VEYA Grup Listesi:**
- Önceden oluşturduğunuz grup listesini seçin
- Aynı mesajı birden fazla gruba gönderir

#### Adım 3: Mesajınızı Yazın

```
🎉 Yeni kampanyamız başladı!

%50 indirim için: https://example.com

✨ Son gün: 31 Aralık
```

> 💡 **İpucu:** Emoji kullanarak mesajlarınızı daha çekici hale getirin!

#### Adım 4: Gönder

1. **"Gönder"** butonuna tıklayın
2. İlerlemeyi **"Görevler"** sayfasından takip edin

### Mesaj Gönderme Hataları

#### ❌ "ChatWriteForbiddenError"
**Çözüm:** Grupta mesaj gönderme yetkiniz yok. Admin olun veya izin alın.

#### ❌ "SlowModeWaitError"
**Çözüm:** Grup yavaş moda sahip. Sistem otomatik olarak bekler ve gönderir.

---

## 💎 Paketler ve Limitler

### Paket Karşılaştırması

| Özellik | Free | Pro | Enterprise |
|---------|------|-----|------------|
| **Maksimum Hesap** | 1 | 10 | 50 |
| **Scraper** | ❌ | ✅ | ✅ |
| **Çoklu Hesap** | ❌ | ✅ | ✅ |
| **İstatistikler** | ❌ | ✅ | ✅ |
| **Grup Listeleri** | ✅ | ✅ | ✅ |
| **Üye Listeleri** | ❌ | ✅ | ✅ |
| **Destek** | ❌ | ✅ | ✅ Öncelikli |

### Paket Yükseltme

1. **"Paketler"** sayfasına gidin
2. İstediğiniz paketi seçin
3. **"Satın Al"** butonuna tıklayın
4. Telegram üzerinden `@mrfurkanbey` ile iletişime geçin
5. Ödeme sonrası paketiniz aktif edilir

---

## 🛠️ Hata Çözümleri

### Genel Hatalar

#### "Database is locked"
**Çözüm:**
```bash
# Uygulamayı kapatın
# Database dosyasını kontrol edin
sqlite3 instance/telegram_manager.db "PRAGMA integrity_check;"
```

#### "Session expired"
**Çözüm:**
- Hesaplar sayfasından hesabı silin
- Tekrar ekleyin ve doğrulama kodunu girin

#### "Connection timeout"
**Çözüm:**
- İnternet bağlantınızı kontrol edin
- VPN kullanıyorsanız kapatın/değiştirin
- Firewall ayarlarını kontrol edin

### Performans Sorunları

#### "İşlem çok yavaş"
**Çözüm:**
- Çoklu hesap kullanın (Pro paket)
- Daha az üye ekleyin (küçük gruplar)
- Database'i optimize edin:
  ```bash
  python optimize_db.py
  ```

#### "Bellek hatası"
**Çözüm:**
- Çok büyük listeleri parçalayın
- Aynı anda tek işlem yapın
- Logları temizleyin

---

## 💡 İpuçları ve En İyi Pratikler

### Üye Ekleme İpuçları

✅ **YAPILMASI GEREKENLER:**
- Eski hesaplar kullanın (1+ ay)
- Günde maksimum 50 üye ekleyin
- Çoklu hesap kullanın
- "Skip" modunu tercih edin
- Normal gruplarda aktif olun
- İşlemler arası bekleyin (30-60 sn)

❌ **YAPILMAMASI GEREKENLER:**
- Yeni hesap ile toplu ekleme yapmayın
- Günde 100+ üye eklemeyin
- Aynı hesapla sürekli ekleme yapmayın
- Botlarla spam yapmayın
- Telegram kurallarını ihlal etmeyin

### Scraper İpuçları

✅ **Verimli Scraping:**
- Filtre kullanın (sadece aktif üyeler)
- Küçük gruplardan başlayın
- Düzenli aralıklarla toplayın
- Listelerinizi organize edin

### Güvenlik İpuçları

🔒 **Hesap Güvenliği:**
- 2FA (iki faktörlü doğrulama) açın
- Güçlü şifreler kullanın
- API bilgilerini kimseyle paylaşmayın
- Session dosyalarını güvende tutun

---

## ❓ SSS

### Sıkça Sorulan Sorular

**S: Bir günde kaç üye ekleyebilirim?**
**C:** Güvenli limit 50 üye/gün/hesap. Çoklu hesap ile bu sayı katlanır.

**S: PeerFlood ne kadar sürer?**
**C:** 2 saatten 2 haftaya kadar değişir. Ortalama 24-48 saat.

**S: Ücretsiz pakette çoklu hesap kullanabilir miyim?**
**C:** Hayır, çoklu hesap özelliği Pro ve Enterprise paketlere özeldir.

**S: Scraper ile kaç üye toplayabilirim?**
**C:** Teknik limit yok, ancak grup büyüklüğüne bağlı. Önerilen: 500-1000 üye/grup.

**S: Flood yedim, ne yapmalıyım?**
**C:** 
1. Bekleyin (24-48 saat)
2. Başka hesap kullanın
3. Günlük limiti düşürün
4. Çoklu hesap kullanmaya başlayın

**S: API bilgilerimi nasıl alırım?**
**C:** [my.telegram.org](https://my.telegram.org) > API Development Tools

**S: Hesabım ban yer mi?**
**C:** Telegram kurallarına uyduğunuz sürece hayır. Aşırı spam yapmayın, günlük limitlere uyun.

**S: Mesajları zamanlayabilir miyim?**
**C:** Şu anda hayır, ancak gelecek güncellemelerde eklenecek.

---

## 📞 Destek

### Yardım Alma

**Teknik Destek:**
- Telegram: `@mrfurkanbey`
- GitHub Issues: [github.com/yourusername/repo/issues](https://github.com)

**Topluluk:**
- Telegram Grubu: Yakında açılacak

### Sorun Bildirme

Bir hata bulduğunuzda lütfen şu bilgileri verin:
1. Hata mesajının tam metni
2. Hangi işlemi yaptığınız (scraping, migration, vb.)
3. Kullandığınız paket (Free, Pro, Enterprise)
4. Ekran görüntüsü (varsa)

---

## 📄 Lisans

Bu proje MIT lisansı altında lisanslanmıştır.

---

## 🔄 Güncelleme Geçmişi

### v1.0.0 (Ocak 2026)
- ✅ İlk sürüm
- ✅ Temel özellikler
- ✅ Scraper modülü
- ✅ Migration sistemi
- ✅ Çoklu hesap desteği
- ✅ Paket sistemi

---

**Son Güncelleme:** 03 Ocak 2026

**Geliştirici:** @mrfurkanbey

**GitHub:** [github.com/yourusername/telegram-manager](https://github.com)
