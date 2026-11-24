# Dokumen proyek Krisye LMS

Dokumen utama ditulis sebagai dokumen hidup (bisa diedit dan dikomentari). Repo ini menyimpan ringkasan dan keputusan yang sudah disepakati.

| Dokumen | Isi | Status |
| --- | --- | --- |
| [Krisye LMS Phase 1: Visi, BRD, dan PRD](https://claude.ai/artifact/GJSX2auY1829KcsQugQ3Cy) | Visi, KPI, stakeholder, persona, penugasan training, kerangka Q1-Q4, ruang lingkup MVP, user journey, asumsi, rencana tahap | Draf, menunggu persetujuan Ve |
| [Rancangan Aplikasi E-Learning](https://claude.ai/artifact/9S4D1fM9yYSCG9Nvy5WiPJ) | Perbandingan Google Classroom vs aplikasi sendiri, fitur per peran, alur, halaman utama, data | Draf |
| [prototype/index.html](prototype/index.html) | Prototipe klik (peserta, trainer, pengelola) dengan data contoh. Hanya alat bantu visual, bukan kode produksi | Draf |

Sumber kurikulum: *Curiculum Krisye Rev.0.1* (11 level, 0-10).

## Tahapan

1. Phase 1 disetujui (Des 2026 minggu 1)
2. Arsitektur, logika seperti Google Classroom (Des 2026 minggu 1-2)
3. UI/UX (Des 2026 minggu 2-3)
4. Development: Rilis 1 inti kelas (Des 2026 - Jan 2027), Rilis 2 naik level, sertifikat, dasbor (Feb - Mar 2027)
5. Testing dan UAT: akhir Jan 2027 (Rilis 1), Mar 2027 (Rilis 2)
6. Peluncuran: Rilis 1 awal Feb 2027, Rilis 2 awal Apr 2027. Januari 2027: tes penempatan dan Orientation lewat Google Forms, hasil diimpor.

Semua tanggal adalah usulan.

## Keputusan yang sudah diambil

| Tanggal | Keputusan |
| --- | --- |
| 2026-11-24 | Selesaikan Phase 1 dulu, baru coding |
| 2026-11-24 | Langsung aplikasi sendiri, logika arsitektur seperti Google Classroom |
| 2026-11-24 | Semua peserta dan trainer punya akun Google: login dengan Google |
| 2026-11-24 | Sesi campuran online dan tatap muka: presensi otomatis (online) dan kode/QR (tatap muka) |
| 2026-11-24 | Syarat naik level memakai matriks di dokumen Phase 1; angka bisa diubah pengelola |
| 2026-11-24 | Sertifikat resmi bernomor (KLC/tahun/L{level}/urut), bertanda tangan, dengan QR verifikasi |
| 2026-11-24 | Data organisasi masih berubah: perusahaan, departemen, posisi, senioritas jadi data master yang bisa diubah pengelola |
