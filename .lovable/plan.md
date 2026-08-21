# Ringkasan Pengeluaran di Dashboard

Menambahkan satu bagian baru "Ringkasan Pengeluaran" di halaman Ringkasan (dashboard), dihitung dari data pengeluaran yang sudah ada.

## Yang akan tampil

1. **Kartu total**
   - Total pengeluaran bulan berjalan (Agustus 2026)
   - Total tahun berjalan
   - Total keseluruhan tercatat

2. **Per bulan**
   - Daftar 12 bulan terakhir dengan total rupiah tiap bulan dan bar proporsional (gaya sama dengan blok "Kondisi Barang" yang sudah ada)
   - Bulan tanpa transaksi tetap ditampilkan dengan Rp 0 agar tren terlihat

3. **Per kategori**
   - Belanja, Service / Perbaikan, Jasa, Iuran, Lain-lain
   - Total rupiah + jumlah transaksi + persentase terhadap total periode

4. **Pemilih periode**
   - Tombol "Bulan ini / Tahun ini / Semua" yang mengubah angka pada blok per kategori
   - Blok per bulan selalu menampilkan 12 bulan terakhir

Ada tautan "Lihat semua" ke halaman Pengeluaran, dan tampilan kosong yang rapi bila belum ada data.

## Catatan teknis

- Tidak ada perubahan database. Dashboard memakai `expensesQuery` dari `src/lib/expenses.ts` lewat `useQuery`.
- Agregasi bulan/kategori dilakukan di klien dengan `useMemo` di `src/routes/index.tsx`; kunci bulan memakai `expense_date` (format `YYYY-MM`), label bulan Indonesia (`Agu 2026`).
- Nilai rupiah memakai `formatRupiah` yang sudah ada.
- Gaya kartu/bar mengikuti komponen `gold-card` dan `Stat` yang sudah dipakai di dashboard, agar konsisten.
