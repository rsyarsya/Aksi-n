# UC-02 - Mencari atau Memfilter Kegiatan

## Informasi Use Case

| Elemen | Keterangan |
|---|---|
| Aktor utama | Mahasiswa |
| Tujuan | Mempersempit daftar kegiatan menggunakan kata kunci, kategori, dan/atau tanggal. |
| Pemicu | Mahasiswa menggunakan kontrol pencarian atau filter pada halaman daftar kegiatan. |
| Prasyarat | Halaman daftar kegiatan telah terbuka dan pilihan kategori tersedia dari sistem. |
| Pascakondisi sukses | Sistem menampilkan kegiatan yang sesuai dengan kriteria aktif atau keadaan hasil kosong. |
| Pascakondisi gagal | Data kegiatan tidak berubah dan parameter tetap tersedia untuk diperbaiki atau dicoba kembali. |

## Linear Sequence Form - Alur Utama

| No. | Tindakan Mahasiswa | Respons Sistem |
|---:|---|---|
| 1 | Mahasiswa memasukkan kata kunci jika diperlukan. | Sistem menerima kata kunci pencarian. |
| 2 | Mahasiswa memilih kategori jika diperlukan. | Sistem menerima kategori yang dipilih. |
| 3 | Mahasiswa memilih tanggal awal dan/atau tanggal akhir jika diperlukan. | Sistem menerima parameter tanggal. |
| 4 | Mahasiswa memilih **Terapkan**. | Sistem memvalidasi seluruh parameter pencarian dan filter. |
| 5 | - | Sistem membatasi pencarian pada kegiatan yang terpublikasi dan tidak dibatalkan. |
| 6 | - | Sistem mencocokkan kata kunci dengan judul serta menerapkan kategori dan tanggal yang terisi menggunakan logika **AND**. |
| 7 | - | Sistem menampilkan daftar hasil beserta kriteria aktif. |
| 8 | Mahasiswa meninjau hasil. | Sistem mempertahankan hasil dan parameter aktif pada layar. |

## Alur Alternatif

### A1 - Hanya sebagian parameter diisi

1. Sistem menerapkan parameter yang terisi saja.
2. Alur berlanjut ke langkah 5 pada alur utama.

### A2 - Hasil kosong

1. Setelah langkah 6, sistem tidak menemukan kegiatan yang sesuai.
2. Sistem menampilkan pesan **"Tidak ada kegiatan yang sesuai"**.
3. Sistem menyediakan tindakan **Ubah filter** dan **Reset**.
4. **Ubah filter** mengembalikan fokus ke kontrol pencarian dan filter.
5. **Reset** menghapus parameter dan menjalankan kembali UC-01.

### A3 - Mahasiswa melakukan reset

1. Mahasiswa memilih **Reset**.
2. Sistem menghapus kata kunci, kategori, dan tanggal aktif.
3. Sistem memuat kembali daftar awal melalui UC-01.

## Alur Kegagalan

### E1 - Rentang tanggal tidak valid

1. Setelah langkah 4, sistem mendeteksi tanggal awal melewati tanggal akhir.
2. Sistem menolak filter dan menampilkan penjelasan kesalahan.
3. Mahasiswa memperbaiki rentang tanggal.
4. Alur kembali ke langkah 4.

### E2 - Pencarian gagal diproses

1. Sistem gagal memproses pencarian atau filter.
2. Sistem mempertahankan parameter yang telah diisi.
3. Sistem menampilkan pesan kegagalan dan tindakan **Coba lagi**.
4. Jika **Coba lagi** dipilih, alur kembali ke langkah 4.

## Aturan Bisnis dan Asumsi

1. Kata kunci dicocokkan terhadap judul kegiatan.
2. Parameter yang diisi bersamaan menggunakan logika **AND**.
3. Tanggal awal tidak boleh melewati tanggal akhir.
4. Pencarian hanya dilakukan terhadap kegiatan terpublikasi dan tidak dibatalkan.
5. Proses ini bersifat baca-saja.

## Kriteria Penerimaan

- Pencarian serta filter kategori dan tanggal menghasilkan data yang sesuai.
- Sistem menampilkan pesan hasil kosong ketika tidak ada kegiatan yang cocok.
- Mahasiswa dapat menghapus parameter menggunakan **Reset**.

