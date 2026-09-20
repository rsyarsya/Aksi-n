# Spesifikasi Use Case Penyelenggara — Aksi!n

Modul: Use Case sisi Penyelenggara (Campus Volunteer & Community Hours Tracker)

## Aturan Bisnis Umum

| Kode | Aturan |
|------|--------|
| BR-01 | Status kegiatan: `DRAFT` → `PUBLISHED` → `COMPLETED`; `DRAFT`/`PUBLISHED` → `CANCELLED`. |
| BR-02 | Data wajib: judul, deskripsi, kategori, lokasi, tanggal mulai, tanggal selesai, batas pendaftaran, kuota, jam volunteer. |
| BR-03 | Draft boleh disimpan dengan data tidak lengkap (minimal judul). Publish mewajibkan semua data wajib valid. |
| BR-04 | Tanggal mulai harus di masa depan; tanggal selesai ≥ tanggal mulai; batas pendaftaran ≤ tanggal mulai. |
| BR-05 | Kuota bilangan bulat ≥ 1; jam volunteer (community hours) > 0. |
| BR-06 | Kuota terpakai = jumlah pendaftaran berstatus `DITERIMA`. Peserta `PENDING` belum memakai kuota. |
| BR-07 | Kuota tidak boleh diubah menjadi lebih kecil dari jumlah peserta `DITERIMA`. |
| BR-08 | Kegiatan `COMPLETED` atau `CANCELLED` tidak dapat diubah. |
| BR-09 | Pembatalan wajib disertai alasan; semua pendaftaran aktif menjadi `DIBATALKAN`, peserta dinotifikasi, dan tidak ada jam volunteer yang dikreditkan. |
| BR-10 | Perubahan tanggal/lokasi/jam pada kegiatan `PUBLISHED` yang sudah punya peserta wajib memicu notifikasi ke peserta. |
| BR-11 | Terima/tolak hanya pada pendaftaran `PENDING`, dan hanya untuk kegiatan `PUBLISHED`. |
| BR-12 | Penerimaan dijalankan dalam transaksi dengan penguncian baris kegiatan agar kuota tidak terlampaui saat dua penyelenggara menerima bersamaan. |
| BR-13 | Penolakan wajib mencantumkan alasan (dikirim ke peserta). |
| BR-14 | Hanya penyelenggara pemilik kegiatan yang dapat mengelolanya. |

---

## UC-01 — Membuat Kegiatan (Drafting & Publishing)

| Elemen | Isi |
|--------|-----|
| **Nama Use Case** | Membuat Kegiatan (Drafting & Publishing) |
| **Actor** | Penyelenggara (utama); Sistem Notifikasi (pendukung) |
| **Pre-condition** | Penyelenggara sudah login dan berperan `PENYELENGGARA` (terverifikasi). |
| **Post-condition (sukses simpan draft)** | Kegiatan tersimpan berstatus `DRAFT`, tidak tampil ke relawan. |
| **Post-condition (sukses publish)** | Kegiatan berstatus `PUBLISHED`, tampil di katalog, dapat didaftar relawan, sisa kuota = kuota. |

**Main Flow**
1. Penyelenggara memilih menu "Buat Kegiatan".
2. Sistem menampilkan formulir kegiatan.
3. Penyelenggara mengisi judul, deskripsi, kategori, lokasi, tanggal mulai, tanggal selesai, batas pendaftaran, kuota, dan jam volunteer.
4. Penyelenggara memilih "Simpan sebagai Draft".
5. Sistem memvalidasi minimal data draft (judul terisi) — BR-03.
6. Sistem menyimpan kegiatan dengan status `DRAFT`.
7. Penyelenggara membuka draft dan memilih "Publikasikan".
8. Sistem memvalidasi kelengkapan data wajib (BR-02).
9. Sistem memvalidasi tanggal (BR-04) dan kuota/jam (BR-05).
10. Sistem mengubah status menjadi `PUBLISHED` dan mencatat waktu publikasi.
11. Sistem menampilkan konfirmasi berhasil beserta tautan kegiatan.

**Alternative Flow**
- **A1 – Hanya simpan draft:** setelah langkah 6 use case selesai; kegiatan bisa dilanjutkan nanti.
- **A2 – Edit draft:** penyelenggara membuka draft lama, kembali ke langkah 3.

**Exception Flow**
- **E1 – Judul kosong saat simpan draft (langkah 5):** sistem menolak dan menampilkan "Judul wajib diisi".
- **E2 – Data wajib belum lengkap saat publish (langkah 8):** sistem menolak publish, menandai field kosong, status tetap `DRAFT`.
- **E3 – Tanggal mulai di masa lalu / tanggal selesai < tanggal mulai / batas pendaftaran > tanggal mulai (langkah 9):** sistem menampilkan pesan kesalahan spesifik, status tetap `DRAFT`.
- **E4 – Kuota < 1 atau bukan bilangan bulat / jam ≤ 0 (langkah 9):** sistem menolak dan meminta perbaikan.
- **E5 – Gagal menyimpan (kesalahan sistem/DB):** sistem menampilkan pesan gagal, data isian dipertahankan di formulir.

