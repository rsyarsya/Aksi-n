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

---

## UC-02 — Mengubah dan Membatalkan Kegiatan

| Elemen | Isi |
|--------|-----|
| **Nama Use Case** | Mengubah dan Membatalkan Kegiatan |
| **Actor** | Penyelenggara (utama); Sistem Notifikasi (pendukung); Relawan (penerima notifikasi) |
| **Pre-condition** | Penyelenggara login dan merupakan pemilik kegiatan; kegiatan berstatus `DRAFT` atau `PUBLISHED`. |
| **Post-condition (ubah)** | Data kegiatan diperbarui; jika `PUBLISHED` dan ada peserta, peserta dinotifikasi. |
| **Post-condition (batal)** | Status `CANCELLED`; pendaftaran aktif menjadi `DIBATALKAN`; peserta dinotifikasi; tidak ada jam volunteer dikreditkan; kegiatan hilang dari katalog. |

**Main Flow — Mengubah**
1. Penyelenggara membuka daftar "Kegiatan Saya" dan memilih kegiatan.
2. Sistem memeriksa kepemilikan (BR-14) dan status kegiatan (BR-08).
3. Sistem menampilkan formulir edit berisi data saat ini.
4. Penyelenggara mengubah data dan memilih "Simpan Perubahan".
5. Sistem memvalidasi kelengkapan data wajib, tanggal (BR-04), kuota/jam (BR-05).
6. Sistem memeriksa kuota baru ≥ jumlah peserta `DITERIMA` (BR-07).
7. Sistem menyimpan perubahan dan mencatat riwayat perubahan (siapa, kapan, field).
8. Jika kegiatan `PUBLISHED` dan tanggal/lokasi/jam berubah serta ada peserta, sistem mengirim notifikasi ke peserta (BR-10).
9. Sistem menampilkan konfirmasi berhasil.

**Main Flow — Membatalkan**
1. Penyelenggara memilih "Batalkan Kegiatan" pada kegiatan miliknya.
2. Sistem meminta alasan pembatalan dan konfirmasi.
3. Penyelenggara mengisi alasan dan mengonfirmasi.
4. Sistem memvalidasi alasan terisi (BR-09).
5. Sistem mengubah status menjadi `CANCELLED`.
6. Sistem mengubah semua pendaftaran `PENDING`/`DITERIMA` menjadi `DIBATALKAN`.
7. Sistem menandai bahwa tidak ada jam volunteer yang dikreditkan.
8. Sistem mengirim notifikasi berisi alasan ke seluruh peserta terdampak.
9. Sistem menampilkan konfirmasi pembatalan.

**Alternative Flow**
- **A1 – Kegiatan `DRAFT`:** langkah notifikasi (8 ubah / 8 batal) dilewati karena belum ada peserta.
- **A2 – Tidak ada perubahan data:** sistem menginformasikan "Tidak ada perubahan" tanpa menyimpan.
- **A3 – Penyelenggara membatalkan konfirmasi pembatalan:** proses dihentikan, status tidak berubah.

**Exception Flow**
- **E1 – Bukan pemilik kegiatan (langkah 2):** akses ditolak (403).
- **E2 – Status `COMPLETED` atau `CANCELLED` (langkah 2):** sistem menolak "Kegiatan tidak dapat diubah".
- **E3 – Data wajib kosong / tanggal invalid / kuota atau jam invalid (langkah 5):** simpan ditolak dengan pesan spesifik.
- **E4 – Kuota baru < jumlah peserta diterima (langkah 6):** simpan ditolak, sistem menampilkan jumlah peserta diterima saat ini.
- **E5 – Alasan pembatalan kosong (batal, langkah 4):** pembatalan ditolak.
- **E6 – Kegiatan sudah berjalan/lewat (tanggal mulai telah lewat) saat ubah tanggal:** perubahan tanggal ditolak (BR-04).
- **E7 – Gagal mengirim notifikasi:** perubahan/pembatalan tetap tersimpan; notifikasi dimasukkan ke antrean retry dan dicatat di log.
- **E8 – Konflik edit (versi data sudah berubah oleh sesi lain):** sistem meminta muat ulang.


