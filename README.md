# Kelime Bilmece 🎯

Kelime Bilmece, Android cihazlar için geliştirilmiş eğlenceli ve eğitici bir kelime tahmin oyunudır. Verilen ipuçlarından yola çıkarak doğru kelimeyi bulmaya çalışın ve kelime dağarcığınızı geliştirin!

## 🎮 Oyun Özellikleri

- **Çeşitli Kategoriler**: Farklı konularda kelime bilmeceleri
- **İpucu Sistemi**: Her seviye için yardımcı ipuçları
- **Seviye Sistemi**: Kolay seviyeden zor seviyeye kadar ilerleyen zorluk
- **Puan Sistemi**: Başarılarınızı takip edin
- **Push Bildirimler**: Günlük hatırlatmalar ve yeni içerik bildirimleri
- **Offline Oyun**: İnternet bağlantısı olmadan da oynanabilir
- **Kullanıcı Dostu Arayüz**: Modern ve sezgisel tasarım

## 🛠️ Kullanılan Teknolojiler

- **Platform**: Android (Java)
- **IDE**: Android Studio
- **Backend**: Firebase
  - Firebase Realtime Database
  - Firebase Authentication
  - Firebase Analytics
- **Push Bildirimler**: OneSignal
- **Minimum SDK**: API 21 (Android 5.0)
- **Hedef SDK**: API 33

## 🚀 Kurulum

### Önkoşullar
- Android Studio (en son sürüm)
- Java 8 veya üzeri
- Firebase projesi
- OneSignal hesabı
- Android SDK (minimum API 21)

### Adımlar

1. **Projeyi klonlayın**
   ```bash
   git clone https://github.com/EmirHanDinc/Kelime-Bilmece.git
   ```

2. **Android Studio'da açın**
   - Android Studio'yu açın
   - "Open an existing Android Studio project" seçin
   - Klonladığınız klasörü seçin

3. **Firebase Yapılandırması**
   - [Firebase Console](https://console.firebase.google.com/) adresine gidin
   - Yeni bir proje oluşturun
   - Android uygulaması ekleyin
   - `google-services.json` dosyasını `app/` klasörüne ekleyin

4. **OneSignal Yapılandırması**
   - [OneSignal Dashboard](https://onesignal.com/) adresine gidin
   - Yeni bir uygulama oluşturun
   - App ID'yi `build.gradle` dosyasına ekleyin

5. **Bağımlılıkları yükleyin**
   ```bash
   ./gradlew build
   ```

6. **Uygulamayı çalıştırın**
   ```bash
   ./gradlew assembleDebug
   ```

## 📂 Proje Yapısı

```
Kelime-Bilmece/
├── app/
│   ├── src/main/java/com/emr/kelimebilmece/
│   │   ├── activities/          # Aktivite sınıfları
│   │   │   ├── MainActivity.java
│   │   │   ├── GameActivity.java
│   │   │   ├── LevelActivity.java
│   │   │   └── SettingsActivity.java
│   │   ├── adapters/           # RecyclerView adaptörleri
│   │   │   └── LevelAdapter.java
│   │   ├── models/             # Veri modelleri
│   │   │   ├── Question.java
│   │   │   ├── Level.java
│   │   │   └── User.java
│   │   ├── utils/              # Yardımcı sınıflar
│   │   │   ├── DatabaseHelper.java
│   │   │   ├── PreferenceManager.java
│   │   │   └── GameLogic.java
│   │   └── fragments/          # Fragment sınıfları
│   ├── src/main/res/
│   │   ├── layout/             # XML layout dosyaları
│   │   ├── drawable/           # Görseller ve drawable'lar
│   │   ├── values/             # Strings, colors, styles
│   │   ├── menu/               # Menü dosyaları
│   │   └── xml/                # Preferences XML
│   ├── build.gradle
│   └── google-services.json
├── gradle/
├── build.gradle
└── README.md
```

## 🎯 Oyun Mekaniği

### Nasıl Oynanır?
1. **Seviye Seçimi**: Ana menüden oynamak istediğiniz seviyeyi seçin
2. **İpucu Okuma**: Verilen ipuçlarını dikkatlice okuyun
3. **Kelime Tahmin**: Boş kutulara harfleri yerleştirerek kelimeyi tahmin edin
4. **İpucu Kullanma**: Takıldığınız yerlerde ipucu butonunu kullanın
5. **Seviye Tamamlama**: Doğru kelimeyi bulduğunuzda bir sonraki seviyeye geçin

### Puan Sistemi
- **Doğru Cevap**: +10 puan
- **İpucu Kullanımı**: -2 puan
- **Zaman Bonusu**: Hızlı çözümde ek puan
- **Seri Bonus**: Ardışık doğru cevaplarda bonus puan

## 🔥 Firebase Yapılandırması

### Realtime Database Yapısı
```json
{
  "questions": {
    "level_1": {
      "question_id": {
        "question": "İpucu metni",
        "answer": "CEVAP",
        "category": "kategori",
        "difficulty": 1,
        "hints": ["İpucu 1", "İpucu 2"]
      }
    }
  },
  "users": {
    "user_id": {
      "name": "Kullanıcı Adı",
      "score": 0,
      "level": 1,
      "completedLevels": []
    }
  },
  "leaderboard": {
    "user_id": {
      "name": "Kullanıcı Adı",
      "score": 1000,
      "rank": 1
    }
  }
}
```

### Güvenlik Kuralları
```json
{
  "rules": {
    "questions": {
      ".read": true,
      ".write": false
    },
    "users": {
      "$uid": {
        ".read": "$uid === auth.uid",
        ".write": "$uid === auth.uid"
      }
    },
    "leaderboard": {
      ".read": true,
      ".write": "auth != null"
    }
  }
}
```

## 📱 OneSignal Entegrasyonu

### Bildirim Türleri
- **Günlük Hatırlatma**: "Bugün kelime bilmecesi çözmeyi unutma!"
- **Yeni Seviye**: "Yeni seviyeler eklendi, hemen oyna!"
- **Başarı Bildirimi**: "Tebrikler! Yeni bir seviye tamamladın"
- **Liderlik Tablosu**: "Liderlik tablosunda yükseldin!"

### Yapılandırma
```java
// OneSignal başlatma
OneSignal.setLogLevel(OneSignal.LOG_LEVEL.VERBOSE, OneSignal.LOG_LEVEL.NONE);
OneSignal.initWithContext(this);
OneSignal.setAppId("YOUR_ONESIGNAL_APP_ID");
```

## 🎨 Uygulama Ekran Görüntüleri

*(Ekran görüntülerini eklemek için görselleri repository'ye yükleyin ve buraya referans verin)*

```markdown
### Ana Menü
![Ana Menü](screenshots/main_menu.png)

### Oyun Ekranı
![Oyun Ekranı](screenshots/game_screen.png)

### Seviye Seçimi
![Seviye Seçimi](screenshots/level_selection.png)

### Ayarlar
![Ayarlar](screenshots/settings.png)
```

## 🏆 Özellikler

### Mevcut Özellikler
- ✅ Kelime tahmin oyunu
- ✅ Seviye sistemi
- ✅ İpucu sistemi
- ✅ Puan takibi
- ✅ Push bildirimleri
- ✅ Offline oyun desteği
- ✅ Kullanıcı profilleri

### Gelecek Güncellemeler
- 🔄 Çok oyunculu mod
- 🔄 Günlük görevler
- 🔄 Sosyal medya paylaşımı
- 🔄 Tema seçenekleri
- 🔄 Ses efektleri
- 🔄 Kategori filtreleme

## 📊 Performans

- **APK Boyutu**: ~15 MB
- **RAM Kullanımı**: ~50 MB
- **Minimum Sistem Gereksinimleri**: Android 5.0+
- **Önerilen RAM**: 2 GB+

## 🛡️ Güvenlik

- **Veri Şifreleme**: Kullanıcı verileri şifrelenir
- **Firebase Security Rules**: Güvenli veri erişimi
- **ProGuard**: Kod gizleme ve optimizasyon
- **SSL Pinning**: Güvenli ağ bağlantıları

## 🧪 Test

### Unit Testler
```bash
./gradlew test
```

### Instrumentation Testler
```bash
./gradlew connectedAndroidTest
```

### Test Kapsamı
- Model sınıfları test edildi
- Oyun mantığı test edildi
- Database işlemleri test edildi

## 📈 Analytics

Firebase Analytics ile takip edilen metrikler:
- Günlük aktif kullanıcılar
- Seviye tamamlama oranları
- Ortalama oyun süresi
- En çok oynanan kategoriler
- Kullanıcı tutma oranları

## 👨‍💻 Geliştirici

**Emir Han Dinç**
- GitHub: [@EmirHanDinc](https://github.com/EmirHanDinc)
- LinkedIn: [Emir Han Dinç](https://linkedin.com/in/emirhandinc)

## 🤝 Katkıda Bulunma

1. Bu repository'yi fork edin
2. Feature branch oluşturun (`git checkout -b feature/YeniOzellik`)
3. Değişikliklerinizi commit edin (`git commit -m 'Yeni özellik eklendi'`)
4. Branch'inizi push edin (`git push origin feature/YeniOzellik`)
5. Pull Request oluşturun

### Katkı Kuralları
- Kod standartlarına uyun
- Test yazın
- Commit mesajlarını açıklayıcı yazın
- Documentation güncelleyin

## 📞 İletişim

- **Issues**: [Sorun bildirmek için](https://github.com/EmirHanDinc/Kelime-Bilmece/issues)
- **Discussions**: [Tartışmalar için](https://github.com/EmirHanDinc/Kelime-Bilmece/discussions)
- **Email**: emirhandinc@example.com

## ⭐ Destek

Eğer bu proje işinize yaradıysa, lütfen bir ⭐ vererek destekleyiniz!

## 📝 Changelog

### v1.0.0 (2023-01-15)
- İlk sürüm yayınlandı
- Temel oyun mekaniği eklendi
- Firebase entegrasyonu tamamlandı
- OneSignal push bildirimleri eklendi

### v1.1.0 (2023-02-20)
- Yeni seviyeler eklendi
- Performans iyileştirmeleri
- Bug düzeltmeleri

---

**Kelime Bilmece** - Eğlenceli kelime tahmin oyunu! 🎯📱
