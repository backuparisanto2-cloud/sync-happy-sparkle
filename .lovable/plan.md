# Halaman Pengeluaran

Halaman baru `/pengeluaran` untuk mencatat semua pengeluaran kost, lengkap dengan kategori, dokumen bukti, dan pengisian otomatis dengan AI.

## Kategori

Lima kategori: **Belanja**, **Service/Perbaikan**, **Jasa**, **Iuran**, **Lain-lain**.

Semua kategori punya field dasar yang sama:
- Nama pengeluaran
- Tanggal
- Nominal (Rupiah)
- Nomor invoice / kuitansi
- Keterangan
- Peruntukan di (lokasi kost)
- Nama vendor
- Lampiran (foto / scan / PDF)

Kategori **Iuran** menambah dua field: nama iuran dan kontak iuran.

## Lokasi kost

Daftar lokasi tersendiri yang bisa dikelola sendiri. Di form, lokasi dipilih dari daftar; kalau belum ada, bisa langsung diketik dan ditambahkan saat itu juga (pola yang sama seperti "kondisi" pada inventaris).

## Upload & konversi file

- Gambar (JPG/PNG/HEIC/dll) dikonversi ke WebP, otomatis dikecilkan sampai maksimal 300KB per file — memakai util kompresi yang sudah ada.
- PDF: setiap halaman dirender jadi gambar lalu dikonversi ke WebP maks 300KB, sehingga semua bukti tersimpan seragam sebagai gambar dan ringan.
- File disimpan di bucket privat `inventory-photos` (folder `pengeluaran/`) dan ditampilkan lewat signed URL, sama seperti foto inventaris.

## Baca dokumen dengan AI

Saat mengunggah bukti, ada tombol **"Isi form dengan AI"**. Gambar hasil konversi dikirim ke AI untuk membaca nota/invoice, lalu hasilnya (nama, tanggal, nominal, nomor invoice, vendor, keterangan) diisikan ke form sebagai saran — pengguna tetap bisa mengoreksi sebelum menyimpan. Kalau AI gagal atau kredit habis, muncul pesan jelas dan form tetap bisa diisi manual.

## Tampilan halaman

- Menu baru "Pengeluaran" di navigasi.
- Ringkasan total pengeluaran (keseluruhan + per kategori) untuk periode terpilih.
- Filter: kategori, rentang tanggal, lokasi, dan pencarian teks (nama, vendor, invoice, keterangan).
- Daftar kartu pengeluaran dengan thumbnail bukti; klik untuk lihat besar, edit, atau hapus.

## Detail teknis

- Migrasi database: tabel `expense_locations` (nama, urutan) dan `expenses` (kategori enum-text, nama, tanggal, nominal numeric, no_invoice, keterangan, lokasi, vendor, nama_iuran, kontak_iuran, attachments jsonb, timestamps + trigger `set_updated_at`). GRANT + RLS akses publik mengikuti pola tabel inventaris yang sudah ada.
- `src/lib/expenses.ts`: tipe, query, dan mutasi (mengikuti gaya `src/lib/inventory.ts`).
- `src/lib/pdf-to-webp.ts`: render halaman PDF ke canvas (pdfjs-dist) lalu reuse `compressToWebp`.
- `PhotoUploader` diperluas agar menerima PDF, atau komponen `AttachmentUploader` baru berbasis komponen tersebut.
- AI lewat Lovable AI Gateway dari `createServerFn` (`src/lib/expense-ai.functions.ts`), model vision Gemini, output JSON terstruktur; penanganan error 402/429 sesuai kontrak gateway.
- Rute baru `src/routes/pengeluaran.tsx` dengan `head()` sendiri (title/description/OG).
