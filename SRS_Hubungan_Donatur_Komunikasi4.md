# 13. Operasional, Deployment, dan Dukungan

SRS ini mendefinisikan kebutuhan operasional tingkat tinggi; keputusan rinci disimpan pada dokumen rancangan dan Architecture Decision Record (ADR).

- Setiap lingkungan (pengembangan, pengujian, produksi) harus memiliki konfigurasi dan secret yang dipisahkan.
- Pipeline harus menjalankan test suite, pemeriksaan secret, validasi kontrak API, dan pemeriksaan health endpoint sesuai workbook.
- Log operasional harus membantu diagnosis antrean, provider, API, dan tiket tanpa memuat data pribadi secara berlebihan.
- Harus ada prosedur pemulihan pekerjaan antrean dan rekonsiliasi status setelah kegagalan.
- Runbook cutover harus menjelaskan konfigurasi, migrasi yang diperlukan, pemeriksaan pascadeployment, pemantauan, dan prosedur rollback.
- Data produksi tidak boleh disalin ke lingkungan pengembangan tanpa otorisasi dan kontrol yang sesuai.

## 14. Verifikasi, Validasi, dan Pengelolaan Perubahan

### 14.1 Verifikasi

Verifikasi memastikan kebutuhan diterapkan dengan benar. Metode yang relevan meliputi review dokumen, pengujian unit, pengujian integrasi/API, pengujian kontrak, pengujian keamanan dasar, pengujian antrean/retry, dan pengujian penerimaan.

### 14.2 Validasi dan Sign-off

Sesuai workbook, SRS dan RTM masuk ke siklus review baseline: draf, review dosen, revisi, review klien, revisi, lalu sign-off klien. SRS final harus memiliki versi, tanggal, identitas narasumber/pemberi persetujuan, serta bukti persetujuan. SRS ini belum berstatus baseline.

### 14.3 Change Control

1. Setiap perubahan setelah sign-off diajukan secara tertulis dengan alasan dan pemohon.
2. Analisis dampak mencakup kebutuhan terkait, API, data, keamanan, pengujian, jadwal, dan ruang lingkup.
3. Perubahan disetujui atau ditolak oleh pemilik baseline yang berwenang.
4. Dokumen, RTM, use case, dan pengujian diperbarui bersamaan; simpan riwayat versi dan keputusan.

## 15. Lampiran A — Daftar Fungsi per Modul (Ringkasan)

| Modul | Fungsi utama | Prioritas awal |
|---|---|---|
| MOD-01 Riwayat Komunikasi | Melihat, mencatat, mencari dan menelusuri interaksi donatur. | M/S |
| MOD-02 Keluhan dan Pertanyaan | Membuat tiket, menetapkan petugas, memperbarui status, mencatat solusi dan mencari tiket. | M/S |
| MOD-03 Preferensi Komunikasi | Mencatat jenis kabar, opt-out, perubahan preferensi dan memeriksa preferensi saat kirim. | M |
| MOD-04 Kabar Penggunaan Dana | Menyusun kabar per kampanye, mengambil data sumber, persetujuan jika perlu, antrean dan status penerima. | M/S |
| MOD-05 Bukti Donasi dan Rekap Tahunan | Menyiapkan dan mengirim bukti/rekap dari data sumber dengan status dan retry aman. | M |
| MOD-06 Antrean dan Pemulihan | Memproses per penerima, mencatat status, retry aman, rate limit dan diagnosis kegagalan. | M/S |
| MOD-07 Laporan Operasional | Ringkasan pesan, status keluhan, laporan periode, pembatasan akses. | S/C |
| MOD-08 Pengguna, Hak Akses, Audit | Autentikasi, otorisasi, audit aktivitas sensitif dan perlindungan secret. | M/S |

## Lampiran B — Checklist Validasi dengan Klien

- [ ] Konfirmasi layanan pihak ketiga yang sedang digunakan dan fungsi yang perlu diganti.
- [ ] Konfirmasi kanal komunikasi masuk dan keluar serta volume bulanan.
- [ ] Konfirmasi siapa yang menulis dan menyetujui kabar penggunaan dana.
- [ ] Konfirmasi preferensi komunikasi, jenis kabar, dan cara mencatat permintaan berhenti.
- [ ] Konfirmasi kebijakan untuk donatur anonim.
- [ ] Konfirmasi target waktu penyelesaian keluhan dan mekanisme eskalasi.
- [ ] Konfirmasi format bukti donasi dan rekapitulasi tahunan serta sumber datanya.
- [ ] Konfirmasi API, field, autentikasi, rate limit, dan lingkungan uji dari setiap kelompok terkait.
- [ ] Konfirmasi target performa, ketersediaan, retensi, backup, dan pemulihan.
- [ ] Konfirmasi penanggung jawab, reviewer, pemberi sign-off, dan prosedur perubahan.

## Lampiran C — Catatan Kepatuhan dan Penggunaan Dokumen

Dokumen ini merupakan draf kerja yang disusun berdasarkan workbook proyek yang tersedia. Dokumen ini mengacu pada praktik rekayasa kebutuhan ISO/IEC/IEEE 29148:2018, tetapi tidak menyatakan sertifikasi atau kepatuhan formal penuh terhadap standar. Struktur, prioritas, target, antarmuka, dan kebutuhan harus diperiksa serta disesuaikan dengan hasil elisitasi, review dosen, review klien, dan sign-off.

Data donatur bersifat sensitif. Jangan menambahkan data pribadi nyata, token, password, API key, atau kredensial produksi ke dokumen maupun repository. Gunakan data sintetis sampai semua persyaratan persetujuan pemrosesan data dan kerahasiaan pada workbook terpenuhi.
