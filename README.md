# Aksi!n

Campus Volunteer & Community Hours Tracker — proyek RPL.

Repository saat ini berisi analisis kebutuhan dan dokumentasi use case. Implementasi aplikasi, perintah build, dan pengujian otomatis belum tersedia.

## Panduan kontribusi

Ikuti [Git Workflow](GIT_WORKFLOW.md): satu branch per pekerjaan, PR menuju `develop`, minimal satu review anggota tim, lalu **Squash and Merge**. Rilis ke `main` hanya melalui PR dari `develop` setelah pengujian.

Nama branch `feature` yang sudah ada merupakan branch lama bersama dan menghalangi pembuatan `feature/*` pada Git. Selama branch tersebut dipertahankan, branch perapian integrasi memakai `fix/integrate-*`. Penataan nama branch lama memerlukan koordinasi dengan pemilik pekerjaan.

## Indeks kontribusi

| Kontributor | Dokumentasi | Sumber |
|---|---|---|
| Wahyu | [Pendaftaran, status, pencarian, dan pembatalan mahasiswa](use-case-mahasiswa-kegiatan-sukarelawan.md) | [Issue #27](https://github.com/rsyarsya/Aksi-n/issues/27), commit `eb2e872` di `develop` |
| Soqi | Spesifikasi dan diagram pengelolaan kegiatan/peserta | [PR #29](https://github.com/rsyarsya/Aksi-n/pull/29), menunggu review |
| Fachry | Daftar, pencarian/filter, dan detail kegiatan mahasiswa | [PR #30](https://github.com/rsyarsya/Aksi-n/pull/30), menunggu review |
| Danis | Verifikasi kehadiran/jam, penyelesaian, dan sertifikasi | [PR #26](https://github.com/rsyarsya/Aksi-n/pull/26), menunggu review |

Status di atas adalah hasil audit 23 September 2026; status terbaru tersedia pada PR masing-masing. Lihat [laporan audit](docs/repository-audit-2026-09-23.md) untuk asal commit, verifikasi pelestarian isi, dan tindak lanjut.
