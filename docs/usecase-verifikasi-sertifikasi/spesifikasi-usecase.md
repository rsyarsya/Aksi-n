# Use Case Specification — Verifikasi & Sertifikasi

## UC01: Verifikasi Kehadiran / Jam Volunteer

| Field | Detail |
| --- | --- |
| **Use Case ID** | UC-VER-01 |
| **Use Case Name** | Verifikasi Kehadiran / Jam Volunteer |
| **Actor** | Penyelenggara / Admin |
| **Description** | Memungkinkan penyelenggara untuk memverifikasi presensi dan mencatat jumlah jam volunteer yang diselesaikan oleh peserta. |
| **Preconditions** | 1. Penyelenggara sudah login.<br>2. Kegiatan telah selesai atau sedang berlangsung. |
| **Postconditions** | Data kehadiran dan jumlah jam volunteer peserta berhasil tercatat di sistem. |

### Normal Flow (Main Success Scenario)
1. Penyelenggara memilih daftar kegiatan yang sedang/telah berlangsung.
2. Sistem menampilkan daftar peserta kegiatan tersebut.
3. Penyelenggara memilih peserta dan mengubah status kehadiran menjadi "Hadir".
4. Penyelenggara memasukkan jumlah jam kerja volunteer untuk peserta tersebut.
5. Penyelenggara mengonfirmasi simpan data.
6. Sistem memvalidasi input data.
7. Sistem menyimpan status kehadiran dan jumlah jam volunteer ke basis data.
8. Sistem menampilkan notifikasi "Verifikasi kehadiran berhasil diperbarui".

### Alternative / Exception Flow
- **4a. Jam Volunteer Tidak Valid (Kurang dari 0 atau melebihi kuota kegiatan):**
  1. Sistem menampilkan pesan kesalahan "Jumlah jam volunteer tidak valid".
  2. Sistem meminta penyelenggara memasukkan ulang jumlah jam.
  3. Kembali ke langkah 4.

---

## UC02: Validasi Penyelesaian Kegiatan

| Field | Detail |
| --- | --- |
| **Use Case ID** | UC-VER-02 |
| **Use Case Name** | Validasi Penyelesaian Kegiatan |
| **Actor** | Penyelenggara |
| **Description** | Memungkinkan penyelenggara untuk memvalidasi bahwa seorang peserta telah memenuhi seluruh kriteria untuk menyelesaikan kegiatan volunteer. |
| **Preconditions** | 1. Penyelenggara sudah login.<br>2. Kehadiran dan jam volunteer peserta sudah diverifikasi (UC-VER-01). |
| **Postconditions** | Status keikutsertaan peserta berubah menjadi "Completed" (Lulus/Selesai). |

### Normal Flow (Main Success Scenario)
1. Penyelenggara membuka halaman validasi penyelesaian kegiatan.
2. Sistem menampilkan ringkasan kehadiran dan total jam volunteer setiap peserta.
3. Penyelenggara menandai peserta yang memenuhi syarat kelulusan.
4. Penyelenggara mengklik tombol "Validasi Penyelesaian".
5. Sistem memverifikasi syarat minimal jam dan kelengkapan tugas peserta.
6. Sistem mengubah status peserta menjadi "Completed".
7. Sistem memperbarui log aktivitas peserta.

### Alternative / Exception Flow
- **5a. Syarat Minimal Kehadiran/Jam Tidak Terpenuhi:**
  1. Sistem menampilkan peringatan "Peserta belum memenuhi batas minimal jam kerja/kehadiran".
  2. Sistem membatalkan perubahan status ke "Completed" dan menetapkan status "Incomplete".

---

## UC03: Penerbitan Sertifikat / Bukti Digital

| Field | Detail |
| --- | --- |
| **Use Case ID** | UC-VER-03 |
| **Use Case Name** | Penerbitan Sertifikat / Bukti Digital |
| **Actor** | Penyelenggara, Sistem (Automated) |
| **Description** | Memproses dan menerbitkan sertifikat digital secara otomatis untuk peserta yang telah tervalidasi menyelesaikannya. |
| **Preconditions** | Status keikutsertaan peserta sudah "Completed" (UC-VER-02). |
| **Postconditions** | File sertifikat digital terbuat dan dapat diunduh oleh peserta. |

### Normal Flow (Main Success Scenario)
1. Penyelenggara memilih menu "Generate Sertifikat" pada kegiatan yang selesai.
2. Sistem mengambil data nama peserta, peran, dan total jam dari basis data.
3. Sistem mendownload template sertifikat kegiatan.
4. Sistem meng-generate sertifikat PDF dan membubuhkan nomor sertifikat/QR code unik.
5. Sistem menyimpan file sertifikat ke server storage.
6. Sistem memperbarui tautan sertifikat pada profil peserta.
7. Sistem memberikan konfirmasi penerbitan sertifikat selesai.

### Alternative / Exception Flow
- **4a. Kegagalan Generate PDF / Server Error:**
  1. Sistem menampilkan pesan error "Gagal membuat dokumen sertifikat".
  2. Sistem memberikan opsi "Coba Lagi" kepada penyelenggara.