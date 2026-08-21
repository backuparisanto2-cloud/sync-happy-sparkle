# Tambah Merk & Serial Number pada Inventaris

Menambahkan dua field baru untuk setiap barang (kamar maupun fasilitas utama): **Merk** dan **Serial Number**.

## Database
- Tambah kolom `brand` (teks, opsional) dan `serial_number` (teks, opsional) ke tabel `room_items` dan `shared_items` lewat migrasi.

## Form input barang
- Di dialog tambah/edit barang, pada blok "Data pembelian" tambahkan isian **Merk** dan **Serial Number** (dua kolom bersebelahan), keduanya opsional.
- Nilai tersimpan saat simpan barang, dan terisi otomatis saat mengedit barang lama.

## Tampilan kartu barang
- Di kartu barang (kamar & fasilitas), tampilkan merk di baris info bersama vendor, dan serial number sebagai teks kecil (mis. `SN: ABC123`).

## Pencarian
- Kolom pencarian di halaman kamar dan fasilitas juga mencocokkan merk dan serial number.

## Laporan
- Tambah dua kolom laporan baru: **Merk** dan **Serial Number**, tersedia di pengelola kolom (Excel/PDF). Merk aktif secara default, serial number tersedia tapi nonaktif secara default agar tabel tetap ringkas.

## Catatan teknis
- Migrasi: `ALTER TABLE ... ADD COLUMN brand text, serial_number text` untuk kedua tabel (grant/RLS existing tetap berlaku).
- Perubahan kode: `src/lib/inventory.ts` (tipe + payload), `src/lib/item-payload.ts`, `src/components/ItemFormDialog.tsx`, `src/components/InventoryItemCard.tsx`, `src/routes/kamar.$nomor.tsx`, `src/routes/fasilitas.tsx`, `src/lib/report.ts`, `src/lib/report-columns.ts`.
