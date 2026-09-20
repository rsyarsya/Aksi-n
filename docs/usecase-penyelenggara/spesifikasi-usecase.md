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

