# Arsitektur Krisye LMS (ringkasan)

Dokumen lengkap: [Krisye LMS: Arsitektur Sistem](https://claude.ai/artifact/Q4qAExhnV3EpSpe4prAbjB). Status: draf, menunggu persetujuan.

## Teknologi

| Bagian | Pilihan |
| --- | --- |
| Aplikasi web | Next.js, TypeScript, di Vercel |
| Database | PostgreSQL di Supabase (region Singapura), Row Level Security |
| Login | Supabase Auth dengan Google; hanya email yang didaftarkan pengelola |
| File | Supabase Storage |
| Email | Resend (Rilis 2) |
| CI | GitHub Actions: cek tipe, lint, tes di setiap PR |

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
- Hak akses ditegakkan dengan Row Level Security dan diuji di tes otomatis.
- Nomor sertifikat dibuat di dalam transaksi database agar tidak ganda.
- Produksi hanya dideploy dari `main`.
