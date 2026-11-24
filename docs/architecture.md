# Arsitektur Krisye LMS (ringkasan)

Dokumen lengkap: [Krisye LMS: Arsitektur Sistem](https://claude.ai/artifact/Q4qAExhnV3EpSpe4prAbjB). Status: draf, menunggu persetujuan.

## Teknologi

Aplikasi berjalan di hosting milik kantor (keputusan 2026-11-24). Jenis hosting masih perlu dipastikan: harus server/VPS yang bisa menjalankan Docker atau Node.js. Bila shared hosting (hanya PHP), jalur cadangan Laravel + MySQL.

| Bagian | Pilihan |
| --- | --- |
| Aplikasi web | Next.js, TypeScript, server Node.js di Docker |
| Database | PostgreSQL 16 di server yang sama |
| Login | Auth.js dengan Google (project Google Cloud atas nama pantasfoundation@gmail.com); hanya email yang didaftarkan pengelola |
| File | MinIO (penyimpanan gaya S3) di disk server |
| Pemasangan | Docker Compose: app, postgres, minio, caddy (HTTPS) |
| Backup | Harian, disalin ke Google Drive pantasfoundation@gmail.com |
| Email | SMTP (Rilis 2) |
| CI | GitHub Actions: cek tipe, lint, tes di setiap PR |

Server minimal (perkiraan): Ubuntu 22.04+, 2 vCPU, 4 GB RAM, 40 GB disk, domain + HTTPS.

Perawat aplikasi setelah peluncuran: Ve dan Josep. Domain: ditentukan nanti.

## Model data

Inti seperti Google Classroom: `kelas`, `pengajar_kelas`, `anggota_kelas`, `topik`, `pengumuman`, `komentar`, `materi`, `tugas`, `soal_kuis`, `pengumpulan`, `nilai`.

Lapisan Krisye:

- Data master (bisa diubah pengelola, dinonaktifkan bukan dihapus): `perusahaan`, `departemen`, `posisi`, `senioritas`; riwayat mutasi di `penempatan_kerja`.
- Kurikulum: `level` (0-10, batas kehadiran dan nilai, perlu persetujuan atasan), `jenis_training`, `komponen_nilai` (bobot 40/40/20).
- Sesi: `sesi` (online, tatap muka, campuran; kode presensi), `presensi` (via link, kode/QR, manual).
- Tes penempatan: `tes_penempatan`, `hasil_tes`.
- Naik level (Rilis 2): `riwayat_level`, `rekomendasi`, `persetujuan`.
- Sertifikat (Rilis 2): `sertifikat` dengan nomor `KLC/tahun/L{level}/urut` dan token verifikasi QR.
- Jejak: `log_perubahan`.

## Aturan yang mengikat kode

- Angka aturan (bobot, batas lulus) disimpan di database, tidak ditulis langsung di kode.
- Hak akses ditegakkan di server aplikasi untuk setiap permintaan dan diuji di tes otomatis; Row Level Security sebagai lapis kedua.
- Nomor sertifikat dibuat di dalam transaksi database agar tidak ganda.
- Produksi hanya dideploy dari `main`.
