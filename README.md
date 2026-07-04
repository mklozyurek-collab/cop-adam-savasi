# Çöp Adam Savaşı — Android Uygulaması

Bu klasör, oyunun APK'sını üretmeye hazır eksiksiz bir Android projesidir. Oyunun kendisi `app/src/main/assets/index.html` içindedir; uygulama onu tam ekran bir WebView içinde açar (titreşim izni ve ses dahil).

APK'yı elde etmenin üç yolu var. **1. yol en kolayıdır ve bilgisayarına hiçbir şey kurmanı gerektirmez.**

---

## Yol 1 — GitHub ile otomatik APK (önerilen, kurulum gerektirmez)

GitHub, projeyi kendi sunucularında derleyip APK'yı sana hazır verir.

1. [github.com](https://github.com) hesabınla giriş yap (yoksa ücretsiz aç).
2. Sağ üstten **+ → New repository** de, ad olarak `cop-adam-savasi` yaz, **Public** seç, **Create repository** butonuna bas.
3. Bu klasördeki dosyaları yükle. İki seçenek:
   - **Bilgisayarında git varsa** (en sağlıklısı), bu klasörün içinde:
     ```
     git init
     git add .
     git commit -m "ilk surum"
     git branch -M main
     git remote add origin https://github.com/KULLANICI_ADIN/cop-adam-savasi.git
     git push -u origin main
     ```
   - **Git yoksa, tarayıcıdan:** Repo sayfasında **uploading an existing file** bağlantısına tıkla, bu klasördeki her şeyi (`.github` klasörü HARİÇ — tarayıcı gizli klasörleri çoğu zaman atlar) sürükleyip bırak ve **Commit changes** de. Sonra **Add file → Create new file** de, dosya adı olarak şunu birebir yaz: `.github/workflows/apk-olustur.yml` ve bu projedeki aynı isimli dosyanın içeriğini kopyala-yapıştır, kaydet.
4. Repo sayfasında üstteki **Actions** sekmesine git. "APK Oluştur" akışı kendiliğinden çalışmaya başlar (1. çalıştırmada onay isteyebilir, **Enable/Run workflow** de).
5. Yeşil tik çıkınca çalıştırmaya tıkla; sayfanın altındaki **Artifacts** bölümünden **cop-adam-savasi-apk** dosyasını indir. İçinden çıkan `app-debug.apk` dosyasını telefonuna at.
6. Telefonda APK'ya dokun; "bilinmeyen kaynaklara izin ver" uyarısını onayla ve kur. Hepsi bu!

> Oyunu her güncellediğinde `app/src/main/assets/index.html` dosyasını değiştirip tekrar push'la — yeni APK otomatik derlenir.

## Yol 2 — Android Studio ile (bilgisayarında derlemek istersen)

1. [Android Studio](https://developer.android.com/studio)'yu kur.
2. **Open** ile bu klasörü aç, Gradle senkronizasyonunun bitmesini bekle.
3. Menüden **Build → Build App Bundle(s) / APK(s) → Build APK(s)** seç.
4. Çıkan bildirimdeki **locate** bağlantısı seni `app/build/outputs/apk/debug/app-debug.apk` dosyasına götürür.

## Yol 3 — APK'sız kurulum: PWA (2 dakikada telefonda)

`docs/` klasörü, oyunun "uygulama gibi kurulabilen" web sürümüdür (tam ekran, çevrimdışı çalışır).

1. Yol 1'deki gibi repo oluşturup dosyaları yükledikten sonra: **Settings → Pages → Branch: main, Folder: /docs → Save**.
2. Birkaç dakika sonra `https://KULLANICI_ADIN.github.io/cop-adam-savasi/` adresi yayında olur.
3. Bu adresi telefonda Chrome ile aç → menüden **Ana ekrana ekle**. Oyun, simgesiyle birlikte uygulama gibi kurulur.
4. Bonus: Aynı adresi [pwabuilder.com](https://www.pwabuilder.com)'a yapıştırırsan sana imzalı bir APK/AAB paketi de üretir (Play Store'a yüklemek istersen bu yol işine yarar).

---

## Sık sorulanlar

- **APK imzalı mı?** Yol 1 ve 2 "debug" imzalı APK üretir: telefona kurulum için yeterlidir, ama Google Play'e yüklenemez. Play için Yol 3'teki PWABuilder çıktısı veya Android Studio'da **Build → Generate Signed App Bundle** kullan.
- **Uygulama adı / paket adı nereden değişir?** Ad: `app/src/main/res/values/strings.xml`. Paket: `app/build.gradle` içindeki `applicationId`.
- **Simge nereden değişir?** `app/src/main/res/mipmap-*/ic_launcher.png` dosyaları.

İyi eğlenceler! 🎮
