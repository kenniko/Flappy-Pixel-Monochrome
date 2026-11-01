# 🐦 Flappy Monochrome

Game **Flappy Bird** bergaya pixel art dengan tema **monokrom bernuansa horor**, dibungkus sebagai aplikasi Android menggunakan [Capacitor](https://capacitorjs.com/). Seluruh visual (burung, pipa, hujan, petir, bintang, gunung) digambar langsung di `<canvas>`, dan musik latar serta efek suara disintesis lewat Web Audio API, jadi tidak ada file gambar atau audio tambahan.

![Platform](https://img.shields.io/badge/platform-Android%207.0%2B-3DDC84?logo=android&logoColor=white)
![Capacitor](https://img.shields.io/badge/Capacitor-wrapper-119EFF?logo=capacitor&logoColor=white)
![Versi](https://img.shields.io/badge/versi-1.0-lightgrey)
![Tema](https://img.shields.io/badge/tema-monochrome-000000)

<!-- Ganti dengan screenshot asli, misalnya simpan di folder docs/ -->
<!--
<p align="center">
  <img src="docs/screenshot-start.png" width="240" alt="Layar awal">
  <img src="docs/screenshot-gameplay.png" width="240" alt="Gameplay">
  <img src="docs/screenshot-gameover.png" width="240" alt="Game over">
</p>
-->
## 🎮 Cara Bermain

| Platform | Kontrol |
| --- | --- |
| Android / layar sentuh | Ketuk layar |
| Desktop / browser | Tekan `Spasi` atau `↑` (atau klik canvas) |

1. Tekan **MULAI MAIN**.
2. Ketuk untuk membuat burung mengepak dan terbang naik. Jika tidak mengetuk, burung jatuh karena gravitasi.
3. Lewati celah di antara pipa untuk menambah **skor**.
4. Menabrak pipa atau tanah berarti *game over*. Coba kalahkan **rekor** Anda!

## 📲 Instalasi (APK)

1. Unduh `flappymonochrome.apk` dari halaman [Releases](../../releases).
2. Di ponsel Android, izinkan **instal dari sumber tidak dikenal** untuk aplikasi yang Anda gunakan untuk membuka file APK.
3. Buka file APK dan ikuti petunjuk instalasi.

**Persyaratan:** Android 7.0 (API 24) atau lebih baru.

> ⚠️ **Perlu koneksi internet.** Halaman game memuat Tailwind CSS (CDN) dan font *Press Start 2P* (Google Fonts) dari internet. Tanpa koneksi, tampilan menu bisa tidak sesuai dan font pixel tidak muncul. Lihat bagian [Rencana Pengembangan](#-rencana-pengembangan) untuk cara membuatnya sepenuhnya offline.

## 📦 Informasi Aplikasi

| | |
| --- | --- |
| Nama aplikasi | Flappy Monochrome |
| Application ID | `com.game.flappymonochrome` |
| Versi | 1.0 (versionCode 1) |
| Min SDK | 24 (Android 7.0) |
| Target SDK | 36 |
| Izin | `INTERNET` |
| Framework | Capacitor (`webDir`: `www`) |

## 🛠️ Teknologi

- **HTML5 Canvas** dan JavaScript murni untuk game loop, fisika, dan rendering
- **Web Audio API** untuk BGM dan SFX sintetis
- **Tailwind CSS** (via CDN) dan **Press Start 2P** untuk tampilan UI
- **Capacitor** untuk membungkus web app menjadi aplikasi Android
- **AndroidX SplashScreen** (`Theme.SplashScreen`) untuk splash screen

## 🧱 Build dari Source

> Bagian ini mengasumsikan struktur proyek Capacitor standar, dengan aset web di folder `www/` dan proyek Android di `android/`. Sesuaikan jika struktur repo Anda berbeda.

**Prasyarat:** [Node.js](https://nodejs.org/) (LTS), [Android Studio](https://developer.android.com/studio), dan JDK sesuai kebutuhan Android Gradle Plugin yang dipakai.

```bash
# 1. Clone repo
git clone https://github.com/<username>/<nama-repo>.git
cd <nama-repo>

# 2. Pasang dependensi
npm install

# 3. Sinkronkan aset web ke proyek Android
npx cap sync android

# 4. Buka di Android Studio
npx cap open android
```

Dari Android Studio, pilih **Build ▸ Build APK(s)**, atau lewat terminal:

```bash
cd android
./gradlew assembleDebug      # hasil: app/build/outputs/apk/debug/
./gradlew assembleRelease    # perlu konfigurasi signing
```

### Menjalankan di browser (tanpa Android)

Cukup buka `www/index.html`, atau jalankan server statis agar lebih nyaman:

```bash
npx serve www
```

## 🎨 Patch Splash Screen dan Ikon Monokrom

Aset splash monokrom tersedia sebagai patch resource Android (`pixelflap-splash-patch-monochrome.zip`). Cara memasangnya:

1. Ekstrak zip, lalu salin isi folder `res/` ke `android/app/src/main/res/` dan timpa file yang sama.
2. Isinya:
   - `drawable/splash.png` dan `drawable-{land,port}-*/splash.png` — gambar splash untuk berbagai kepadatan layar dan orientasi
   - `drawable/splash_icon.png` — ikon animasi splash (768×768, transparan)
   - `values/splash_colors.xml` — warna latar splash (`splash_bg` = `#969696`)
   - `values/styles.xml` — tema `AppTheme.NoActionBarLaunch` (basis `Theme.SplashScreen`)
3. Pastikan dependensi `androidx.core:core-splashscreen` tersedia dan `AndroidManifest.xml` memakai `AppTheme.NoActionBarLaunch` sebagai tema peluncuran.
4. Jalankan `npx cap sync android`, lalu build ulang.

## 🗺️ Rencana Pengembangan

- [ ] Jadikan game sepenuhnya offline: simpan Tailwind dan font secara lokal, lalu hapus izin `INTERNET` jika sudah tidak diperlukan
- [ ] Ikon *themed* monokrom untuk Android 13+ (layer `<monochrome>` pada adaptive icon)
- [ ] Papan peringkat online
- [ ] Pilihan karakter dan latar
- [ ] Rilis build *release* yang sudah ditandatangani

## 🤝 Kontribusi

Kontribusi, laporan bug, dan ide fitur sangat disambut:

1. *Fork* repo ini
2. Buat branch fitur: `git checkout -b fitur/nama-fitur`
3. *Commit* perubahan: `git commit -m "Tambah fitur ..."`
4. *Push* ke branch: `git push origin fitur/nama-fitur`
5. Buka **Pull Request**

## 🙏 Kredit

- Font [Press Start 2P](https://fonts.google.com/specimen/Press+Start+2P) oleh CodeMan38
- [Capacitor](https://capacitorjs.com/) oleh Ionic
- Terinspirasi dari *Flappy Bird*
