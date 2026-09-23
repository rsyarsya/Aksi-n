# Audit repository Aksi!n — 23 September 2026

Aturan utama: [GIT_WORKFLOW.md](../GIT_WORKFLOW.md). Pelacakan: [issue #28](https://github.com/rsyarsya/Aksi-n/issues/28).

## Snapshot sebelum perubahan

Empat branch, delapan commit unik, 26 issue terbuka (tidak termasuk PR), satu PR terbuka, dan tidak ada PR tertutup/merged. Semua branch tidak dilindungi; ruleset dan run GitHub Actions kosong. Default branch adalah `develop`. Repository berisi dokumentasi; tidak ada implementasi aplikasi, build, atau test suite yang dapat dijalankan.

| Branch | Head awal | Kondisi |
|---|---|---|
| `main` | `83e20ac0e6784405c19be80aa161cbcf903477eb` | Commit awal dengan README kosong; belum merupakan aplikasi stabil yang teruji. |
| `develop` | `eb2e8722591c5d820b1f88834d9dd586cd43a339` | Satu commit setelah main, kontribusi Wahyu dengan pesan `Add files via upload`, tanpa PR. |
| `feature` | `1aef745694838f30e6136a05daf3eb95a2e6397a` | Lima commit setelah main: empat Soqi dan satu Fachry; belum ada PR. |
| `danis-verification-and-certificate` | `9584568063693429d12bd4e951f4859d17f87281` | Satu commit dokumentasi setelah main; PR #26 ke develop, tanpa review. |

Seluruh kontribusi bersifat penambahan. Perbandingan dua ujung branch dapat menampilkan dokumen Wahyu seolah terhapus karena branch anggota dibuat sebelum commit tersebut. Merge tiga arah mempertahankan dokumen itu; tidak boleh mengganti seluruh tree develop dengan tree branch anggota.

## Pelestarian dan integrasi

| Kontributor | Sumber | Jalur integrasi |
|---|---|---|
| Soqi / Muhammad Syauqi Fittuqo | `767543a`, `47e1363`, `52fff2d`, `b6b1ea2` | Cherry-pick empat commit dengan author asli ke `fix/integrate-organizer-usecases`; [PR #29](https://github.com/rsyarsya/Aksi-n/pull/29). |
| Fachry Alfareeza | `1aef745` | Cherry-pick dengan author asli ke `fix/integrate-student-discovery`; pesan commit baru menjadi `docs: add student activity discovery use cases`; [PR #30](https://github.com/rsyarsya/Aksi-n/pull/30). |
| Bintang Daneswara / Danis | `9584568` | [PR #26](https://github.com/rsyarsya/Aksi-n/pull/26) dipertahankan dan dilengkapi konteks issue, validasi, serta poin review. |
| Wahyu | `eb2e872` dan [issue #27](https://github.com/rsyarsya/Aksi-n/issues/27) | Sudah ada di develop; isi dan riwayat dipertahankan. |

Branch sumber tidak dihapus atau ditulis ulang. Nama lama `feature` menghalangi `feature/*` karena benturan namespace ref Git. Branch perbaikan integrasi memakai `fix/*`. Branch Danis tetap memakai nama lama demi menjaga PR yang ada; perubahan nama legacy memerlukan koordinasi tim. Commit lama di main/develop tidak diubah hanya untuk memperbaiki pesan commit.

PR perapian workflow menambahkan dokumen aturan yang diberikan pengguna, AGENTS.md, indeks README, .gitignore sesuai daftar workflow, template PR, dan laporan ini. Dokumen kebutuhan asli tidak dipindah atau diubah.

## Verifikasi

- Keempat file Soqi dan keenam file Fachry dibandingkan terhadap tree sumber: identik.
- Simulasi tiga arah masing-masing branch sumber dengan develop: tidak ada konflik Git.
- Rehearsal gabungan dilakukan secara lokal, tanpa memindahkan ref develop/main di server; seluruh file kontribusi dibandingkan kembali dengan sumber setelah penggabungan.
- Pemeriksaan struktur blok PlantUML, penanda konflik, daftar file terlarang, serta diff dilakukan pada hasil rehearsal.
- Ada baris kosong ekstra bawaan sumber di akhir tujuh file Soqi/Fachry. Ini temuan formatting yang dipertahankan untuk menjaga kesamaan byte kontribusi; bukan konflik Git.
- Pemeriksaan struktur diagram tidak membuktikan diagram dapat dirender atau alur bisnis benar. Renderer PlantUML dan pengujian aplikasi belum dijalankan; aplikasi belum tersedia.

## Masalah yang masih memerlukan review

1. Pencarian kegiatan dibahas oleh Fachry dan Wahyu. Ada tumpang tindih topik, bukan file identik yang aman dihapus.
2. `Menunggu Konfirmasi`, `Menunggu Persetujuan`, `Menunggu`, dan `PENDING` belum memiliki pemetaan istilah resmi. Cakupan filter lokasi di dokumen Wahyu berbeda dengan kategori/tanggal pada issue #2 dan dokumen Fachry.
3. Diagram UC03 pengelolaan peserta Soqi tersedia, tetapi uraian UC03 belum ada dalam spesifikasi Markdown.
4. Dokumen Danis perlu ditinjau terhadap issue #6/#7: kepemilikan kegiatan, validasi batas jam, validasi kode sertifikat, dan pencegahan penerbitan ganda belum seluruhnya eksplisit. Penetapan peran admin juga perlu disepakati.
5. Issue #27 dan file Wahyu mengandung materi yang sama; issue tetap menjadi sumber pelacakan. Issue fitur #1–#12 dan tugas #13–#25 tetap terbuka karena keberadaan dokumen tidak memenuhi seluruh kriteria implementasi, pengujian, dan review.
6. Semua issue awal belum memiliki assignee formal. Nama PIC pada body tidak dipetakan ke username secara spekulatif.
7. Belum ada branch protection, ruleset, atau CI. GitHub mengizinkan merge commit/rebase selain squash; pelaksanaan workflow masih bergantung pada disiplin tim. Konfigurasi akses tidak diubah pada audit ini.

## Kondisi handoff

PR disiapkan untuk review, belum di-merge. `GIT_WORKFLOW.md` mengharuskan minimal satu review anggota tim sebelum merge; pemeriksaan oleh agen ini tidak dicatat sebagai persetujuan anggota tim. Setelah review, gunakan Squash and Merge dengan pesan yang menjelaskan kontribusi dan trailer co-author yang sesuai. Periksa kembali SHA head, konflik, dan pelestarian dokumen sebelum setiap merge.

`develop` tetap pada `eb2e872`; `main` tetap pada `83e20ac`. Tidak ada direct push, force push, penghapusan branch, atau perubahan implementasi fitur. Main belum layak disebut rilis aplikasi stabil; promosi hanya melalui PR develop ke main setelah pengujian dan review yang sesuai.
