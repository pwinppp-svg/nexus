# NEXUS AI

Aplikasi web AI berbahasa Indonesia dengan antarmuka gelap futuristik. Fitur: chat AI, unggah file, ekstraksi teks PDF/DOCX/TXT/CSV/JSON, analisis gambar, generator gambar, dan peningkatan resolusi gambar lokal.

## Persyaratan
- Node.js 22 atau lebih baru (untuk workflow cloud)
- API key OpenAI untuk fitur AI (chat, analisis gambar, generator gambar)

## Menjalankan di laptop
1. Ekstrak ZIP ini.
2. Buka folder `nexus-ai` di Terminal / Command Prompt.
3. Jalankan `npm install`.
4. Salin `.env.example` menjadi `.env`.
5. Buka `.env`, isi `OPENAI_API_KEY=API_KEY_MILIKMU`.
6. Jalankan `npm run dev`.
7. Buka alamat `http://localhost:5173` di browser.

## Build / produksi
- `npm run build`
- `npm start`
- Buka `http://localhost:3001`

Jangan pernah mengunggah atau membagikan file `.env`. File unggahan tersimpan di `server/uploads`. Atur kebijakan penyimpanan dan autentikasi sebelum aplikasi dipublikasikan ke internet.

## Catatan
- Image Enhancer saat ini melakukan upscale 2x dan penyesuaian kontras/saturasi di browser; ini bukan rekonstruksi detail AI.
- Generator gambar memakai model `gpt-image-1` dan memerlukan akses API yang sesuai.
- Jangan gunakan aplikasi publik tanpa menambahkan login, batas penggunaan, validasi keamanan, dan kebijakan privasi.

## Membuat aplikasi Android (APK)

Proyek ini sudah disiapkan untuk dibungkus dengan Capacitor. Karena lingkungan kerja ini tidak memiliki Android SDK dan tidak dapat mengunduh toolchain Android, paket ini menyertakan GitHub Actions untuk membangun APK di runner cloud GitHub.

### Yang diperlukan
- Node.js 20+
- Android Studio versi terbaru
- Android SDK dan Android SDK Build-Tools (pasang melalui Android Studio)
- Backend NEXUS AI yang sudah online dengan HTTPS

### Cara membangun APK melalui GitHub Actions (tanpa memasang Android Studio di laptop)
1. Buat repository GitHub kosong bernama `nexus-ai` dan unggah seluruh isi folder proyek ini ke branch `main`.
2. Jika backend sudah online, buka **Settings > Secrets and variables > Actions > New repository secret**. Buat secret `NEXUS_API_URL` berisi URL backend HTTPS. Jika belum ada backend, APK tetap dapat dibangun tetapi fitur AI yang memerlukan server belum aktif.
3. Buka tab **Actions**, pilih workflow **Build NEXUS AI APK**, lalu tekan **Run workflow**. Workflow juga berjalan otomatis saat ada push ke `main` atau `master`.
4. Setelah workflow berhasil, buka hasil run dan unduh artifact **NEXUS-AI-debug-apk**.
5. Ekstrak artifact, lalu pasang `app-debug.apk` pada perangkat Android.

Workflow cloud berada di `.github/workflows/android-apk.yml`. Untuk membangun manual dengan Android Studio, jalankan `npm install`, `npm run build`, `npx cap add android`, `npx cap sync android`, lalu build APK melalui Android Studio.

### Catatan penting
- APK membutuhkan backend yang bisa diakses dari internet agar chat, analisis gambar, unggah file, dan generator gambar bekerja.
- Jangan menaruh `OPENAI_API_KEY` di kode Android atau file frontend.
- Image Enhancer lokal berjalan di perangkat, tetapi fitur AI memerlukan backend.
- Untuk distribusi ke orang lain, siapkan autentikasi, kebijakan privasi, pembatasan penggunaan, dan APK release yang ditandatangani.

## Tautan unduhan APK otomatis
Workflow sekarang juga membuat **GitHub Release** berisi `NEXUS-AI.apk`. Setelah workflow hijau, buka tab **Releases** di repository: tautan `NEXUS-AI.apk` di sana bisa dibuka langsung dari HP. Pastikan repository publik jika ingin tautan bisa diunduh tanpa login.
