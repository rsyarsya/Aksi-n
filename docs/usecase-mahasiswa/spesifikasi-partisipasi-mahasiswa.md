# Use Case Sisi Mahasiswa — Pendaftaran Kegiatan Sukarelawan

**Bagian tugas:** Use Case sisi Mahasiswa B
**Cakupan:** Linear Sequence Form + Activity Diagram
**Aktor:** Mahasiswa
**Konteks aplikasi:** Platform untuk mencari dan mendaftar ke kegiatan/event sukarelawan.

> Selain 2 use case yang disebutkan secara eksplisit (Mendaftar Kegiatan, Melihat Status/Pendaftaran), saya menambahkan **Mencari Kegiatan** dan **Membatalkan Pendaftaran** sebagai use case partisipasi mahasiswa lainnya, karena keduanya melengkapi alur penuh (cari → daftar → pantau status → batalkan bila perlu). Kalau kelompok/dosen sudah punya daftar use case lain yang lebih spesifik, kabari saja dan bagian ini bisa disesuaikan.

---

## 1. Use Case: Mendaftar Kegiatan

**Deskripsi singkat:** Mahasiswa memilih sebuah kegiatan sukarelawan dan mendaftarkan diri untuk berpartisipasi.

### Linear Sequence Form

| No | Aksi Mahasiswa | Respon Sistem |
|----|----------------|---------------|
| 1 | Membuka halaman detail kegiatan yang ingin diikuti | Menampilkan informasi kegiatan (nama, deskripsi, jadwal, kuota, syarat) |
| 2 | Menekan tombol "Daftar" | Memeriksa status login, kuota kegiatan, dan apakah mahasiswa sudah pernah terdaftar |
| 3 | Mengisi formulir pendaftaran (jika ada data tambahan) dan mengirimkan | Memvalidasi data formulir |
| 4 | — | Jika data valid: menyimpan pendaftaran dan mengubah status menjadi "Menunggu Konfirmasi" |
| 5 | — | Menampilkan notifikasi bahwa pendaftaran berhasil dikirim |
| 5a | — | *(Alternatif)* Jika kuota penuh / sudah terdaftar / data tidak valid: menampilkan pesan bahwa pendaftaran tidak dapat diproses |

### Activity Diagram

```mermaid
flowchart TD
    Start(["Mulai"]) --> A["Mahasiswa membuka halaman detail kegiatan"]
    A --> B["Mahasiswa menekan tombol 'Daftar'"]
    B --> C{"Kuota tersedia dan belum terdaftar?"}
    C -- Tidak --> Z1["Sistem menampilkan pesan tidak dapat mendaftar"]
    Z1 --> End1(["Selesai"])
    C -- Ya --> D["Mahasiswa mengisi formulir pendaftaran"]
    D --> E{"Data valid?"}
    E -- Tidak --> Z2["Sistem menampilkan pesan kesalahan data"]
    Z2 --> D
    E -- Ya --> F["Sistem menyimpan data pendaftaran"]
    F --> G["Sistem mengubah status menjadi 'Menunggu Konfirmasi'"]
    G --> H["Sistem menampilkan notifikasi pendaftaran berhasil"]
    H --> End2(["Selesai"])
```

---

## 2. Use Case: Melihat Status/Pendaftaran

**Deskripsi singkat:** Mahasiswa memantau status dari kegiatan-kegiatan yang telah ia daftarkan.

### Linear Sequence Form

| No | Aksi Mahasiswa | Respon Sistem |
|----|----------------|---------------|
| 1 | Membuka menu "Kegiatan Saya" / "Riwayat Pendaftaran" | Mengambil seluruh data pendaftaran milik mahasiswa dari basis data |
| 2 | — | Menampilkan daftar kegiatan yang diikuti beserta status masing-masing (Menunggu, Diterima, Ditolak, Selesai) |
| 3 | Memilih salah satu kegiatan dari daftar | Mengambil detail data dan status terkini kegiatan tersebut |
| 4 | — | Menampilkan halaman detail status (jadwal, lokasi, catatan tambahan, riwayat perubahan status) |

### Activity Diagram

```mermaid
flowchart TD
    Start(["Mulai"]) --> A["Mahasiswa membuka menu 'Kegiatan Saya'"]
    A --> B["Sistem mengambil data pendaftaran mahasiswa"]
    B --> C{"Ada data pendaftaran?"}
    C -- Tidak --> Z["Sistem menampilkan pesan 'Belum ada kegiatan diikuti'"]
    Z --> End1(["Selesai"])
    C -- Ya --> D["Sistem menampilkan daftar kegiatan beserta status"]
    D --> E["Mahasiswa memilih salah satu kegiatan"]
    E --> F["Sistem menampilkan detail status kegiatan"]
    F --> End2(["Selesai"])
```

---

## 3. Use Case: Mencari Kegiatan

**Deskripsi singkat:** Mahasiswa menelusuri atau mencari kegiatan sukarelawan yang tersedia berdasarkan kata kunci atau filter tertentu.

### Linear Sequence Form

| No | Aksi Mahasiswa | Respon Sistem |
|----|----------------|---------------|
| 1 | Membuka halaman utama/daftar kegiatan | Menampilkan daftar seluruh kegiatan yang tersedia |
| 2 | Memasukkan kata kunci dan/atau memilih filter (kategori, lokasi, tanggal) | Memproses kriteria pencarian |
| 3 | — | Menampilkan daftar kegiatan yang sesuai dengan kriteria pencarian |
| 4 | Memilih salah satu kegiatan dari hasil pencarian | Menampilkan halaman detail kegiatan tersebut |

### Activity Diagram

```mermaid
flowchart TD
    Start(["Mulai"]) --> A["Mahasiswa membuka halaman daftar kegiatan"]
    A --> B["Mahasiswa memasukkan kata kunci dan/atau filter"]
    B --> C["Sistem memproses kriteria pencarian"]
    C --> D{"Ada kegiatan yang sesuai?"}
    D -- Tidak --> Z["Sistem menampilkan pesan 'Kegiatan tidak ditemukan'"]
    Z --> End1(["Selesai"])
    D -- Ya --> E["Sistem menampilkan daftar hasil pencarian"]
    E --> F["Mahasiswa memilih salah satu kegiatan"]
    F --> G["Sistem menampilkan detail kegiatan"]
    G --> End2(["Selesai"])
```

---

## 4. Use Case: Membatalkan Pendaftaran

**Deskripsi singkat:** Mahasiswa membatalkan partisipasinya pada kegiatan yang sebelumnya sudah ia daftarkan.

### Linear Sequence Form

| No | Aksi Mahasiswa | Respon Sistem |
|----|----------------|---------------|
| 1 | Membuka menu "Kegiatan Saya" dan memilih kegiatan yang ingin dibatalkan | Menampilkan detail kegiatan beserta opsi "Batalkan Pendaftaran" |
| 2 | Menekan tombol "Batalkan Pendaftaran" | Menampilkan dialog konfirmasi pembatalan |
| 3 | Mengonfirmasi pembatalan | Memeriksa apakah pembatalan masih diperbolehkan (mis. sebelum batas waktu tertentu) |
| 4 | — | Jika diperbolehkan: mengubah status pendaftaran menjadi "Dibatalkan" dan mengirim notifikasi |
| 4a | — | *(Alternatif)* Jika melewati batas waktu: menampilkan pesan bahwa pembatalan tidak dapat dilakukan |

### Activity Diagram

```mermaid
flowchart TD
    Start(["Mulai"]) --> A["Mahasiswa memilih kegiatan di 'Kegiatan Saya'"]
    A --> B["Mahasiswa menekan tombol 'Batalkan Pendaftaran'"]
    B --> C["Sistem menampilkan dialog konfirmasi"]
    C --> D["Mahasiswa mengonfirmasi pembatalan"]
    D --> E{"Masih dalam batas waktu pembatalan?"}
    E -- Ya --> F["Sistem mengubah status menjadi 'Dibatalkan'"]
    F --> G["Sistem mengirim notifikasi pembatalan"]
    G --> End1(["Selesai"])
    E -- Tidak --> Z["Sistem menampilkan pesan 'Pembatalan tidak dapat dilakukan'"]
    Z --> End2(["Selesai"])
```
