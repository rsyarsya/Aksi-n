# UC-03 - Melihat Detail Kegiatan

## Informasi Use Case

| Elemen | Keterangan |
|---|---|
| Aktor utama | Mahasiswa |
| Tujuan | Mendapatkan informasi lengkap mengenai kegiatan sebelum menentukan tindakan berikutnya. |
| Pemicu | Mahasiswa memilih kartu kegiatan dari daftar atau hasil pencarian/filter. |
| Prasyarat | Kegiatan memiliki identitas valid dan sebelumnya muncul pada daftar yang dapat diakses mahasiswa. |
| Pascakondisi sukses | Detail kegiatan ditampilkan tanpa mengubah data. |
| Pascakondisi gagal | Sistem menjelaskan bahwa kegiatan tidak tersedia atau gagal dimuat serta menyediakan jalan kembali atau percobaan ulang. |

## Linear Sequence Form - Alur Utama

| No. | Tindakan Mahasiswa | Respons Sistem |
|---:|---|---|
| 1 | Mahasiswa memilih kartu kegiatan. | Sistem menerima identitas kegiatan yang dipilih. |
| 2 | - | Sistem mencari kegiatan berdasarkan identitas tersebut. |
| 3 | - | Sistem memastikan kegiatan masih ada, sudah terpublikasi, dan tidak dibatalkan. |
| 4 | - | Sistem mengambil deskripsi, jadwal, lokasi, penyelenggara, kuota, syarat, dan tenggat pendaftaran. |
| 5 | - | Sistem menghitung informasi kuota berdasarkan peserta berstatus diterima, bukan pendaftar yang masih menunggu. |
| 6 | - | Sistem menampilkan halaman detail kegiatan secara lengkap. |
| 7 | Mahasiswa membaca detail kegiatan. | Sistem mempertahankan halaman detail pada layar. |
| 8 | Mahasiswa dapat memilih **Kembali**. | Sistem mengembalikan mahasiswa ke daftar dengan konteks pencarian dan filter sebelumnya. |

## Alur Alternatif

### A1 - Kegiatan tidak lagi tersedia

1. Setelah langkah 3, sistem mendeteksi kegiatan dibatalkan atau tidak lagi terpublikasi.
2. Sistem tidak menampilkan detail sebagai kegiatan aktif.
3. Sistem menampilkan pesan bahwa kegiatan tidak lagi tersedia.
4. Sistem menyediakan tindakan **Kembali ke daftar**.

## Alur Kegagalan

### E1 - Identitas kegiatan tidak ditemukan

1. Setelah langkah 2, sistem tidak menemukan kegiatan.
2. Sistem menampilkan pesan **"Kegiatan tidak ditemukan"**.
3. Sistem menyediakan tindakan **Kembali ke daftar**.

### E2 - Pengambilan detail gagal

1. Sistem gagal mengambil data detail.
2. Sistem menampilkan pesan kegagalan serta tindakan **Coba lagi** dan **Kembali ke daftar**.
3. Jika **Coba lagi** dipilih, alur kembali ke langkah 2.

## Aturan Bisnis

1. Detail aktif hanya ditampilkan jika kegiatan masih terpublikasi dan tidak dibatalkan.
2. Detail wajib memuat deskripsi, jadwal, lokasi, penyelenggara, kuota, syarat, dan tenggat.
3. Kuota terpakai dihitung dari peserta berstatus diterima, bukan pendaftar yang masih menunggu.
4. Kembali ke daftar mempertahankan konteks pencarian dan filter sebelumnya.
5. Use case ini bersifat baca-saja.

## Kriteria Penerimaan

- Detail memuat deskripsi, jadwal, lokasi, penyelenggara, kuota, syarat, dan tenggat.
- Kegiatan yang dibatalkan atau tidak lagi terpublikasi tidak ditampilkan sebagai kegiatan aktif.
- Informasi kuota menggunakan jumlah peserta berstatus diterima.

