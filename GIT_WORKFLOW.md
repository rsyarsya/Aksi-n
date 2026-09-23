# Git Workflow — Aksi!n

Dokumen ini menjadi panduan penggunaan Git dan GitHub pada pengembangan **Aksi!n** agar proses development tetap terstruktur, mudah dilacak, dan meminimalkan konflik antaranggota tim.

## 1. Branch Structure

Gunakan tiga jenis branch utama:

```text
main
develop
feature/*
fix/*
```

### `main`
Branch untuk versi yang sudah stabil.

**Rules:**
- Tidak boleh melakukan `push` langsung ke `main`.
- Perubahan hanya masuk melalui Pull Request dari `develop`.
- Merge dilakukan setelah fitur telah diuji.

### `develop`
Branch utama untuk proses development.

**Rules:**
- Semua feature dan bug fix digabungkan terlebih dahulu ke `develop`.
- Tidak melakukan development langsung di branch ini.
- Pull Request minimal diperiksa oleh 1 anggota tim sebelum merge.

### `feature/*`
Digunakan untuk pengembangan fitur baru.

Format:

```text
feature/nama-fitur
```

Contoh:

```text
feature/login
feature/activity-list
feature/activity-registration
feature/certificate
```

### `fix/*`
Digunakan untuk memperbaiki bug.

Format:

```text
fix/nama-bug
```

Contoh:

```text
fix/login-validation
fix/activity-filter
```

---

## 2. Workflow

Workflow standar:

```text
Issue
  ↓
Create Branch
  ↓
Development
  ↓
Commit
  ↓
Push
  ↓
Pull Request
  ↓
Review
  ↓
Merge to develop
  ↓
Testing
  ↓
Merge develop → main
```

Sebelum mulai bekerja:

```bash
git checkout develop
git pull origin develop
```

Buat branch baru:

```bash
git checkout -b feature/nama-fitur
```

Setelah selesai:

```bash
git add .
git commit -m "feat: deskripsi perubahan"
git push origin feature/nama-fitur
```

Kemudian buat **Pull Request menuju `develop`** melalui GitHub.

---

## 3. Commit Convention

Gunakan format:

```text
<type>: <description>
```

Type yang digunakan:

| Type | Digunakan untuk |
|---|---|
| `feat` | Menambahkan fitur baru |
| `fix` | Memperbaiki bug |
| `docs` | Mengubah dokumentasi |
| `style` | Perubahan tampilan atau formatting |
| `refactor` | Mengubah struktur kode tanpa mengubah fungsi |
| `test` | Menambah atau memperbaiki testing |
| `chore` | Konfigurasi atau pekerjaan pendukung |

Contoh:

```text
feat: add volunteer activity registration
fix: validate duplicate registration
docs: update project setup guide
style: improve activity card layout
refactor: simplify authentication service
```

Gunakan commit message yang singkat dan menjelaskan perubahan yang dilakukan.

Hindari:

```text
update
fix
revisi
coba
final
final banget
```

---

## 4. Pull Request Rules

Setiap Pull Request harus:

- Mengarah ke branch `develop`.
- Memiliki judul yang menjelaskan perubahan.
- Menjelaskan secara singkat apa yang dikerjakan.
- Menghubungkan PR dengan GitHub Issue jika tersedia.
- Tidak memiliki conflict.
- Sudah diuji oleh developer sebelum meminta review.

Contoh judul:

```text
feat: implement volunteer activity registration
```

Contoh deskripsi:

```md
## Changes
- Menambahkan form pendaftaran kegiatan
- Menambahkan validasi kapasitas peserta
- Menghubungkan form dengan API pendaftaran

Closes #12
```

Gunakan:

```text
Closes #nomor-issue
```

agar GitHub Issue otomatis tertutup setelah Pull Request di-merge.

---

## 5. Code Review

Minimal **1 anggota tim** melakukan review sebelum merge.

Reviewer memastikan:

- Fitur sesuai requirement.
- Tidak ada bug yang terlihat.
- Tidak ada file yang tidak seharusnya ikut ter-commit.
- Tidak terdapat credential atau data rahasia.
- Code masih dapat dijalankan.

Jika terdapat masalah, gunakan:

```text
Request changes
```

Jika sudah sesuai:

```text
Approve
```

---

## 6. Merge Rules

Gunakan:

```text
Squash and Merge
```

agar histori branch tetap bersih.

Feature branch dapat dihapus setelah berhasil di-merge.

```text
feature/login
        ↓
      PR
        ↓
     develop
        ↓
     testing
        ↓
      main
```

Dilarang melakukan:

```bash
git push --force
```

ke:

```text
main
develop
```

---

## 7. GitHub Issue

Setiap pekerjaan yang cukup signifikan sebaiknya dibuat sebagai GitHub Issue.

Issue minimal berisi:

```md
## Description
Deskripsi singkat pekerjaan.

## Task
- [ ] Task 1
- [ ] Task 2
- [ ] Task 3

## Acceptance Criteria
Kondisi yang menentukan pekerjaan dianggap selesai.
```

Contoh:

```text
#12 Implement Volunteer Registration
```

Branch terkait dapat dibuat sebagai:

```text
feature/12-volunteer-registration
```

---

## 8. Before Starting Work

Selalu sinkronisasi repository sebelum mulai coding:

```bash
git checkout develop
git pull origin develop
```

Jika bekerja pada branch yang sudah ada:

```bash
git checkout feature/nama-fitur
git pull origin develop
```

Tujuannya agar branch tidak terlalu tertinggal dari perkembangan terbaru.

---

## 9. Files That Must Not Be Committed

Jangan melakukan commit terhadap:

```text
.env
.env.local
node_modules/
bin/
obj/
*.log
```

Credential seperti berikut juga dilarang masuk repository:

```text
API_KEY
DATABASE_PASSWORD
PRIVATE_KEY
ACCESS_TOKEN
```

Gunakan `.gitignore` dan environment variable.

---

## 10. Team Rules

1. Jangan melakukan push langsung ke `main`.
2. Hindari development langsung di `develop`.
3. Satu branch digunakan untuk satu fitur atau satu perbaikan.
4. Pull perubahan terbaru sebelum mulai bekerja.
5. Commit perubahan dalam ukuran kecil dan logis.
6. Gunakan commit convention yang telah ditentukan.
7. Setiap perubahan utama masuk melalui Pull Request.
8. Minimal satu anggota melakukan review sebelum merge.
9. Selesaikan conflict sebelum melakukan merge.
10. Jangan menyimpan credential atau data sensitif di repository.

## Branch Flow

```text
feature/* ──┐
            │
fix/* ──────┼──> develop ──> main
            │
feature/* ──┘
```

`develop` menjadi tempat integrasi pekerjaan tim, sedangkan `main` selalu menyimpan versi aplikasi yang stabil.
