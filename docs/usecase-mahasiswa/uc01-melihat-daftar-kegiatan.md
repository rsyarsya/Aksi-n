# UC-01 - Melihat Daftar Kegiatan

## Informasi Use Case

| Elemen | Keterangan |
|---|---|
| Aktor utama | Mahasiswa |
| Tujuan | Melihat daftar kegiatan yang layak ditampilkan dan memilih kegiatan untuk ditelusuri lebih lanjut. |
| Pemicu | Mahasiswa membuka menu **Kegiatan**. |
| Prasyarat | Aplikasi dapat diakses dan data kegiatan tersedia di sistem. |
| Pascakondisi sukses | Daftar kegiatan ditampilkan tanpa mengubah data. Hanya kegiatan terpublikasi dan tidak dibatalkan yang disajikan. |
| Pascakondisi gagal | Tidak ada data yang berubah. Sistem menampilkan keadaan kosong atau pesan kegagalan yang sesuai. |

## Linear Sequence Form - Alur Utama

| No. | Tindakan Mahasiswa | Respons Sistem |
|---:|---|---|
| 1 | Mahasiswa membuka menu **Kegiatan**. | Sistem menerima permintaan halaman daftar kegiatan. |
| 2 | - | Sistem meminta data kegiatan. |
| 3 | - | Sistem mengambil kegiatan dengan status **terpublikasi** dan **tidak dibatalkan**. |
| 4 | - | Sistem menyiapkan informasi ringkas setiap kegiatan untuk kartu daftar. |
| 5 | - | Sistem menampilkan daftar kegiatan yang memenuhi ketentuan. |
| 6 | Mahasiswa menelusuri daftar kegiatan. | Sistem mempertahankan daftar pada layar. |
| 7 | Mahasiswa dapat memilih salah satu kartu kegiatan. | Sistem meneruskan kegiatan yang dipilih ke **UC-03 - Melihat Detail Kegiatan**. |

## Alur Alternatif

### A1 - Tidak ada kegiatan yang tersedia

1. Setelah langkah 3, sistem tidak menemukan kegiatan yang memenuhi ketentuan.
2. Sistem menampilkan pesan **"Belum ada kegiatan tersedia"**.
3. Use case berakhir tanpa perubahan data.

## Alur Kegagalan

### E1 - Pengambilan data gagal

1. Setelah langkah 2, sistem gagal mengambil data kegiatan.
2. Sistem menampilkan pesan bahwa daftar kegiatan gagal dimuat.
3. Sistem menyediakan tindakan **Coba lagi**.
4. Jika mahasiswa memilih **Coba lagi**, alur kembali ke langkah 2.

## Aturan Bisnis

1. Kegiatan yang belum dipublikasikan tidak boleh muncul pada daftar.
2. Kegiatan yang sudah dibatalkan tidak boleh muncul pada daftar.
3. Use case ini bersifat baca-saja.
4. Halaman daftar ditargetkan tampil maksimal tiga detik pada kondisi penggunaan normal.

## Kriteria Penerimaan

- Daftar menampilkan kegiatan terpublikasi yang tidak dibatalkan.
- Jika tidak ada kegiatan yang memenuhi ketentuan, sistem menampilkan keadaan kosong yang informatif.

