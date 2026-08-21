# Import Repository: joyful-sync-pulse

## Goal
Mengimpor seluruh repository GitHub `backuparisanto2-cloud/joyful-sync-pulse` ke dalam project Lovable ini.

## Technical Context
Project ini berjalan di stack TanStack Start v1 dengan Tailwind CSS v4. Repository sumber perlu diperiksa terlebih dahulu agar dapat dipetakan ke struktur project saat ini (`src/routes`, `src/components`, `src/styles.css`, dll.).

## Plan Steps

1. **Verifikasi dan inspeksi repository**
   - Clone repository ke direktori sementara `/tmp/joyful-sync-pulse`.
   - Periksa struktur folder, file konfigurasi (`package.json`, `vite.config.*`, `tsconfig.json`), framework yang digunakan, dan daftar dependency.
   - Identifikasi route/halaman, komponen, styling, aset, serta integrasi eksternal (auth, database, API, storage).

2. **Mapping dan persiapan migrasi**
   - Bandingkan stack sumber dengan TanStack Start v1.
   - Buat daftar file yang dapat langsung disalin dan file yang perlu ditulis ulang/disesuaikan.
   - Catat dependency yang perlu ditambahkan atau diganti dengan alternatif yang kompatibel dengan edge runtime.

3. **Salin dan sesuaikan kode**
   - Pindahkan halaman/route ke `src/routes/` mengikuti konvensi TanStack Start.
   - Pindahkan komponen, hooks, utilities, dan styles ke lokasi yang sesuai.
   - Sesuaikan import path dan konfigurasi styling agar sesuai dengan `src/styles.css` dan tema project ini.
   - Tangani aset (gambar, font, file statis) dengan cara yang benar untuk cross-project.

4. **Konfigurasi dependency dan environment**
   - Install dependency yang diperlukan melalui `bun add`.
   - Tambahkan secret/environment variable jika repository sumber membutuhkannya.

5. **Build dan verifikasi**
   - Jalankan build untuk memastikan tidak ada error kompilasi.
   - Periksa route utama dan halaman kunci melalui preview browser.
   - Perbaiki error yang muncul.

## Expected Outcome
Project ini berisi replika fungsional dari repository `joyful-sync-pulse` yang berjalan di TanStack Start v1, dengan build berhasil dan preview dapat dibuka.
