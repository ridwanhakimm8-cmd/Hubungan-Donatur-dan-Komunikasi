# SOFTWARE REQUIREMENTS SPECIFICATION (SRS)
## Subsistem Hubungan Donatur dan Komunikasi

**Baitulmal Tazkia (BMTZ) Kelompok 11 — Klaster Relasi dan Transparansi**

Acuan rekayasa kebutuhan: ISO/IEC/IEEE 29148:2018  
Versi dokumen: 0.1 (Draf untuk validasi klien)  
Tanggal: 21 Oktober 2026  
Status: BELUM DISETUJUI / BELUM BASELINE  

Dokumen kerja berdasarkan WORKBOOK PROYEK “Hubungan Donatur dan Komunikasi”. Seluruh dugaan awal harus dikonfirmasi dengan klien sebelum sign-off.

---

## Kontrol Dokumen

| Atribut | Nilai |
| :--- | :--- |
| Nama dokumen | SRS — Subsistem Hubungan Donatur dan Komunikasi |
| Organisasi / klien | Baitulmal Tazkia (BMTZ) |
| Tim | Kelompok 11 — Hubungan Donatur dan Komunikasi |
| Standar acuan | ISO/IEC/IEEE 29148:2018 (rekayasa kebutuhan) |
| Versi / status | 0.1 — Draf untuk review; belum mendapat sign-off |
| Pemilik dokumen | Kelompok 11 (nama anggota diisi tim) |

---

## Daftar Isi
*(Gunakan fitur *Outline* di editor Markdown atau GitHub untuk navigasi cepat)*
1. Pendahuluan
2. Deskripsi Umum
3. Lingkup dan Batas Sistem
4. Model Proses Bisnis
5. Kebutuhan Fungsional per Modul
6. Kebutuhan Antarmuka Eksternal
7. Kebutuhan Nonfungsional
8. Use Case
9. Data dan Informasi yang Dikelola
10. Kriteria Penerimaan Sistem
11. Matriks Keterlacakan Kebutuhan (RTM) — Draf
12. Risiko dan Mitigasi Awal
13. Operasional, Deployment, dan Dukungan
14. Verifikasi, Validasi, dan Pengelolaan Perubahan
15. Lampiran

---

## 1. Pendahuluan

### 1.1 Tujuan Dokumen
Dokumen ini menetapkan kebutuhan perangkat lunak untuk subsistem Hubungan Donatur dan Komunikasi Baitulmal Tazkia. SRS menjadi acuan bersama bagi klien, analis, perancang, pengembang, penguji, dan tim operasional dalam memahami ruang lingkup, fungsi, batasan, kualitas, antarmuka, serta cara verifikasi sistem.

### 1.2 Ruang Lingkup Produk
Subsistem direncanakan menggantikan layanan pihak ketiga yang alur kerjanya belum dapat disesuaikan dengan proses BMTZ. Fokusnya adalah riwayat percakapan donatur, pengiriman bukti donasi dan rekapitulasi tahunan, penyampaian kabar penggunaan dana per kampanye, pengelolaan preferensi komunikasi termasuk berhenti berlangganan, serta pencatatan pertanyaan/keluhan sampai penyelesaiannya.

### 1.3 Tujuan Bisnis
- Menyatukan riwayat interaksi donatur agar petugas berikutnya memahami konteks komunikasi sebelumnya.
- Mengirim informasi yang relevan kepada donatur sesuai kampanye dan preferensi komunikasi mereka.
- Menghormati permintaan donatur untuk berhenti menerima jenis kabar tertentu.
- Mengurangi risiko pesan ganda ketika pengiriman massal mengalami kegagalan sebagian.
- Mencatat keluhan dan pertanyaan beserta petugas penanggung jawab serta status penyelesaiannya.
- Mendukung pengiriman bukti donasi dan rekapitulasi tahunan berdasarkan data yang disediakan subsistem terkait.

### 1.4 Konvensi Penulisan
Setiap kebutuhan memiliki ID unik. Kata “harus” menunjukkan kebutuhan wajib pada rancangan awal; kata “perlu dikonfirmasi” menunjukkan keputusan yang belum dapat dianggap final. Prioritas awal: Must (M), Should (S), Could (C). Prioritas akan dikunci setelah wawancara dan review klien.

### 1.5 Referensi
- WORKBOOK PROYEK: Hubungan Donatur dan Komunikasi, Kelompok 11 — Baitulmal Tazkia, Gasal 2026/2027, khususnya Bab 2–5 dan pekerjaan per pertemuan.
- ISO/IEC/IEEE 29148:2018, Systems and software engineering — Life cycle processes — Requirements engineering.
- Undang-Undang Republik Indonesia Nomor 27 Tahun 2022 tentang Pelindungan Data Pribadi (rujukan konteks perlindungan data; penerapan perlu dikaji oleh pihak berwenang).

### 1.6 Definisi dan Singkatan

| Istilah | Definisi |
| :--- | :--- |
| BMTZ | Baitulmal Tazkia. |
| Donatur | Pihak yang memberikan donasi atau tercatat terkait pemberian donasi. |
| Kampanye | Program penggalangan dana yang menjadi konteks donasi dan kabar lanjutan. |
| Preferensi komunikasi | Pilihan donatur tentang jenis kabar/komunikasi yang ingin diterima. |
| Opt-out / berhenti menerima kabar | Permintaan donatur agar jenis komunikasi tertentu tidak dikirim lagi. |
| Antrean pengiriman | Daftar pekerjaan pengiriman yang diproses bertahap agar kegagalan dapat dilanjutkan. |
| Idempotensi | Mekanisme agar pengulangan operasi tidak menghasilkan pengiriman duplikat. |
| API | Application Programming Interface; kontrak pertukaran data antarsubsistem. |
| RTM | Requirements Traceability Matrix; matriks keterlacakan kebutuhan. |

---

## 2. Deskripsi Umum

### 2.1 Perspektif Produk
Subsistem ini adalah aplikasi mandiri yang memiliki penyimpanan dan deployment sendiri sesuai workbook. Subsistem berinteraksi dengan subsistem hulu dan hilir melalui kontrak API. Data donatur dan riwayat pemberian dikelola oleh kelompok Penerimaan Donasi dan Akun Donatur; daftar donatur per kampanye berasal dari Manajemen Kampanye Penghimpunan; status kesediaan donasi berulang berasal dari Donasi Berulang dan Kanal Pembayaran Digital; angka penggunaan dana berasal dari Pelaporan Publik dan Transparansi Dana.

### 2.2 Fungsi Produk pada Tingkat Tinggi
- Mencatat dan menelusuri riwayat komunikasi per donatur.
- Mengelola pertanyaan dan keluhan sampai status selesai.
- Mengelola preferensi jenis kabar dan permintaan berhenti menerima kabar.
- Menyusun dan mengirim kabar penggunaan dana berdasarkan kampanye yang diikuti.
- Mengirim bukti donasi dan rekapitulasi tahunan melalui kanal yang disepakati.
- Memproses pengiriman massal melalui antrean dengan status per penerima.
- Menyediakan laporan status pengiriman, aktivitas komunikasi, dan keluhan.

### 2.3 Kelas Pengguna dan Karakteristik

| Pengguna / aktor | Tanggung jawab utama | Hak akses awal (perlu validasi) |
| :--- | :--- | :--- |
| Petugas layanan donatur | Mencatat percakapan, menangani pertanyaan/keluhan, melihat riwayat | Membaca riwayat yang diizinkan; membuat catatan; memperbarui tiket sesuai penugasan |
| Penyusun komunikasi | Menyusun kabar, memilih kampanye dan kelompok penerima | Membuat draf pesan dan melihat status draf |
| Penyetuju / supervisor | Memeriksa naskah dan kampanye penerima jika proses persetujuan diwajibkan | Menyetujui, meminta revisi, atau menolak pengiriman |
| Administrator sistem | Mengelola akun, peran, konfigurasi dan pemantauan | Akses administratif sesuai kebijakan; akses data dibatasi seperlunya |
| Pimpinan / pelapor | Memantau indikator dan laporan | Membaca laporan agregat sesuai kewenangan |
| Donatur | Menerima informasi dan menyampaikan pilihan/pertanyaan | Interaksi melalui kanal yang disediakan; akses akun mandiri belum diasumsikan |

### 2.4 Lingkungan Operasional
Platform, sistem operasi, penyedia email/pesan, penyedia hosting, dan stack teknologi belum ditetapkan dalam SRS ini. Tim perlu menetapkannya dalam dokumen rancangan/ADR setelah memvalidasi kebutuhan, kontrak API, keamanan, serta ketersediaan layanan pihak ketiga.

### 2.5 Batasan Desain dan Implementasi
- Setiap kelompok mengerjakan satu subsistem utuh dengan database, aplikasi, dan deployment sendiri sesuai workbook.
- Subsistem hilir mengakses data subsistem lain melalui kontrak API; tidak menggunakan foreign key yang melintasi batas subsistem.
- Pengiriman pesan massal harus diproses melalui antrean, bukan hanya tindakan sinkron dari tombol pengguna.
- Status pesan dicatat per penerima: menunggu, terkirim, gagal, atau dibatalkan.
- Pilihan berhenti menerima kabar diperiksa kembali pada saat pengiriman, bukan hanya ketika daftar penerima dibuat.
- Kredensial produksi tidak boleh disimpan di repository. Hingga dokumen pemrosesan data dan perjanjian kerahasiaan ditandatangani, gunakan data sintetis.

### 2.6 Asumsi dan Ketergantungan

| ID | Asumsi / ketergantungan | Status / tindakan |
| :--- | :--- | :--- |
| ASM-01 | API identitas dan riwayat pemberian tersedia dari kelompok Penerimaan Donasi dan Akun Donatur. | Konfirmasi kontrak, field, autentikasi, dan lingkungan uji. |
| ASM-02 | API daftar donatur per kampanye tersedia dari Manajemen Kampanye Penghimpunan. | Konfirmasi filter kampanye dan paginasi. |
| ASM-03 | API status kesediaan donasi berulang tersedia dari kelompok Donasi Berulang dan Kanal Pembayaran Digital. | Konfirmasi makna status dan waktu pembaruan. |
| ASM-04 | Angka penggunaan dana berasal dari Pelaporan Publik dan Transparansi Dana. | Konfirmasi periode, definisi angka, dan status publikasi. |
| ASM-05 | Email dan kanal pesan yang digunakan belum dipastikan. | Wawancara klien dan kaji provider, biaya, batas kirim, serta persetujuan. |
| ASM-06 | Donatur anonim dan preferensi menerima kabar merupakan dua atribut yang berbeda. | Validasi aturan bisnis dengan klien. |
| ASM-07 | Aturan persetujuan naskah sebelum pengiriman belum dipastikan. | Klien menentukan peran, kondisi, dan alur persetujuan. |

---

## 3. Lingkup dan Batas Sistem

### 3.1 Termasuk dalam Lingkup
- Riwayat percakapan/interaksi per donatur, dengan kanal, waktu, ringkasan, dan petugas.
- Pengiriman bukti donasi dan rekapitulasi tahunan melalui email dan pesan sesuai kanal yang disepakati.
- Pengiriman kabar penggunaan dana kepada donatur menurut kampanye yang diikuti.
- Pengelolaan pilihan jenis kabar dan permintaan berhenti menerima kabar.
- Pencatatan pertanyaan/keluhan, penugasan petugas, tindak lanjut, dan penyelesaian.
- Antrean pengiriman, status per penerima, penanganan kegagalan, serta pencegahan pengiriman ganda.
- Laporan operasional untuk status pesan, riwayat komunikasi, dan penanganan keluhan.

### 3.2 Tidak Termasuk dalam Lingkup
- Pengelolaan identitas utama dan riwayat pemberian donatur; dimiliki subsistem Penerimaan Donasi dan Akun Donatur.
- Penghitungan dan pencatatan angka penggunaan dana; sumber data berasal dari subsistem Pelaporan Publik dan Transparansi Dana.
- Penagihan donasi berulang dan pengelolaan kanal pembayaran digital.
- Pengelolaan media sosial sebagai kanal penggalangan dana.
- Pengembangan sistem pembayaran atau rekonsiliasi transaksi donasi.
- Penentuan angka penggunaan dana atau konten laporan keuangan secara mandiri oleh subsistem ini.

### 3.3 Pertanyaan Terbuka yang Harus Diputuskan

| ID | Pertanyaan untuk klien | Mengapa penting |
| :--- | :--- | :--- |
| Q-01 | Layanan pihak ketiga apa yang digunakan sekarang dan fungsi apa yang tidak dapat disesuaikan? | Menetapkan gap dan kebutuhan pengganti. |
| Q-02 | Kanal masuk dan keluar apa yang dipakai (telepon, pesan, email, surat, media sosial)? | Menetapkan integrasi dan cakupan riwayat. |
| Q-03 | Berapa volume pesan per bulan dan berapa donatur yang meminta berhenti menerima kabar? | Menentukan kapasitas, antrean, dan ukuran operasional. |
| Q-04 | Siapa menulis naskah kabar dan apakah diperlukan persetujuan? | Menetapkan alur status dan peran. |
| Q-05 | Apakah donatur anonim tetap dapat menerima kabar? | Memisahkan anonimitas tampilan dari preferensi komunikasi. |
| Q-06 | Berapa target waktu penyelesaian keluhan dan siapa penanggung jawabnya? | Menentukan SLA dan eskalasi. |
| Q-07 | Bagaimana definisi bukti donasi dan rekapitulasi tahunan, serta siapa sumber datanya? | Menghindari salah data dan duplikasi tanggung jawab. |
| Q-08 | Apa aturan retensi, penghapusan, koreksi, dan akses data komunikasi? | Menetapkan privasi dan tata kelola data. |
| Q-09 | Apakah komunikasi perlu mendukung balasan masuk secara otomatis, atau hanya pencatatan manual oleh petugas? | Mempengaruhi kompleksitas integrasi kanal. |
| Q-10 | Siapa yang berwenang menyetujui SRS dan perubahan kebutuhan? | Menetapkan baseline dan change control. |

---

## 4. Model Proses Bisnis

### 4.1 Proses Berjalan (As-Is) — Hipotesis Awal
Workbook menyebut hubungan donatur saat ini dikelola melalui layanan pihak ketiga yang alur kerjanya tidak dapat disesuaikan dengan proses BMTZ. Rincian langkah, kanal, waktu, peran, dan masalah aktual belum diverifikasi; oleh karena itu, alur di bawah adalah hipotesis untuk dipakai saat wawancara, bukan fakta final.

1. Petugas menerima atau mengirim komunikasi melalui layanan yang sedang digunakan.
2. Riwayat komunikasi mungkin tidak seluruhnya tersimpan dalam satu tempat atau tidak sesuai proses petugas.
3. Petugas perlu mencari data donatur, kampanye, bukti donasi, atau angka penggunaan dana dari sistem/kelompok lain.
4. Pertanyaan dan keluhan ditangani oleh petugas, tetapi status, penanggung jawab, dan waktu penyelesaian perlu diperiksa.
5. Pengiriman pesan massal berisiko mengirim kepada donatur yang telah meminta berhenti atau mengirim pesan yang sama lebih dari sekali.

### 4.2 Proses Usulan (To-Be) — Alur Utama
Alur usulan menggabungkan pengelolaan data dari API hulu, penyusunan kabar, pemeriksaan preferensi pada saat pengiriman, antrean per penerima, pencatatan status, dan pembaruan riwayat. Aturan persetujuan pesan serta detail kanal tetap menunggu keputusan klien.

> **[Gambar: Flowchart Proses Hubungan Donatur & Komunikasi]** 
> *(Silakan masukkan gambar flowchart dari dokumen asli di sini)*

### 4.3 Proses Usulan Penanganan Keluhan

> **[Gambar: Flowchart Penanganan Pertanyaan / Keluhan]**
> *(Silakan masukkan gambar flowchart dari dokumen asli di sini)*

### 4.4 Aturan Bisnis

| ID | Aturan bisnis | Rasional / verifikasi |
| :--- | :--- | :--- |
| BR-01 | Preferensi komunikasi harus diperiksa saat pengiriman untuk setiap penerima. | Mencegah pesan terkirim setelah donatur memilih berhenti. |
| BR-02 | Status pengiriman dicatat per penerima: menunggu, terkirim, gagal, dibatalkan. | Membuat hasil pengiriman massal dapat diaudit. |
| BR-03 | Pengulangan proses setelah kegagalan tidak boleh mengirim ulang pesan yang sudah sukses. | Mencegah pesan duplikat; perlu uji idempotensi. |
| BR-04 | Naskah komunikasi tidak boleh memuat data pribadi penerima manfaat yang tidak disetujui untuk dibagikan. | Mencegah kebocoran data pribadi. |
| BR-05 | Riwayat komunikasi harus dapat ditelusuri per donatur yang teridentifikasi; interaksi anonim ditangani sesuai aturan yang disepakati. | Mendukung kesinambungan layanan tanpa mengasumsikan identitas. |
| BR-06 | Sumber identitas/riwayat donasi, daftar kampanye, status donasi berulang, dan angka penggunaan dana tetap menjadi tanggung jawab subsistem pemiliknya. | Menjaga batas tanggung jawab antarkelompok. |
| BR-07 | Pilihan anonim tidak otomatis berarti menolak semua komunikasi, dan pilihan menerima kabar tidak otomatis membuka identitas publik. | Dua pilihan ini harus dikelola terpisah. |
| BR-08 | Pesan gagal harus menyimpan alasan/status kegagalan yang tersedia dan dapat diproses ulang secara aman. | Mendukung pemulihan dan audit. |

---

## 5. Kebutuhan Fungsional per Modul

Modul berikut diturunkan dari lingkup workbook. Daftar fungsi merupakan baseline awal yang harus dikonfirmasi, bukan klaim bahwa semua detail proses telah disetujui klien.

### MOD-01 — Riwayat Komunikasi Donatur

| ID | Kebutuhan fungsional | Prioritas | Kriteria penerimaan ringkas |
| :--- | :--- | :--- | :--- |
| FR-001 | Sistem harus menampilkan riwayat komunikasi yang terkait dengan donatur yang dipilih. | M | Petugas memilih donatur dan melihat catatan komunikasi yang diizinkan. |
| FR-002 | Sistem harus memungkinkan petugas mencatat interaksi masuk/keluar dengan tanggal, kanal, ringkasan, petugas, dan status tindak lanjut. | M | Catatan tersimpan dan muncul pada riwayat donatur. |
| FR-003 | Sistem harus mendukung pencarian/penyaringan riwayat berdasarkan donatur, rentang tanggal, kanal, dan status jika data tersedia. | S | Hasil pencarian sesuai filter. |
| FR-004 | Sistem harus mencatat sumber dan waktu pembaruan catatan yang dibuat di dalam subsistem. | S | Audit metadata tersedia bagi peran berwenang. |

### MOD-02 — Pengelolaan Pertanyaan dan Keluhan

| ID | Kebutuhan fungsional | Prioritas | Kriteria penerimaan ringkas |
| :--- | :--- | :--- | :--- |
| FR-010 | Sistem harus memungkinkan petugas membuat tiket pertanyaan/keluhan dengan nomor unik, ringkasan, kanal, tanggal masuk, dan prioritas/status. | M | Tiket dibuat dan memiliki ID unik. |
| FR-011 | Sistem harus memungkinkan tiket ditugaskan kepada petugas penanggung jawab. | M | Nama/peran penanggung jawab tersimpan. |
| FR-012 | Sistem harus mendukung pembaruan status tiket, minimal Baru, Diproses, Menunggu Informasi, Selesai, dan Ditutup; daftar final dikonfirmasi klien. | M | Perubahan status tersimpan dalam riwayat. |
| FR-013 | Sistem harus menyimpan catatan tindak lanjut dan ringkasan penyelesaian tiket. | M | Petugas berikutnya dapat membaca tindakan sebelumnya. |
| FR-014 | Sistem harus memungkinkan petugas mencari tiket yang belum selesai dan memfilter berdasarkan status, petugas, atau tanggal. | S | Tiket yang cocok tampil. |
| FR-015 | Sistem sebaiknya mendukung target waktu penyelesaian dan penanda tiket melewati target setelah SLA disepakati. | S | Tiket melewati target dapat diidentifikasi. |

### MOD-03 — Preferensi dan Berhenti Menerima Kabar

| ID | Kebutuhan fungsional | Prioritas | Kriteria penerimaan ringkas |
| :--- | :--- | :--- | :--- |
| FR-020 | Sistem harus menyimpan preferensi donatur untuk jenis kabar/komunikasi yang ditentukan BMTZ. | M | Preferensi terbaca dan dapat diperbarui oleh peran yang diizinkan. |
| FR-021 | Sistem harus mencatat permintaan berhenti menerima kabar beserta jenis kabar, waktu, sumber permintaan, dan statusnya. | M | Permintaan berhenti tercatat dan dapat ditelusuri. |
| FR-022 | Sistem harus memeriksa preferensi terbaru untuk setiap penerima tepat sebelum pengiriman pesan. | M | Penerima yang telah opt-out tidak dikirimi jenis kabar terkait. |
| FR-023 | Sistem harus membedakan pilihan anonim dari pilihan menerima/menolak komunikasi. | M | Perubahan satu pilihan tidak mengubah pilihan lainnya. |
| FR-024 | Sistem harus mencegah petugas mengabaikan preferensi aktif melalui pengiriman massal biasa. | M | Uji negatif menunjukkan pengiriman dibatalkan untuk penerima opt-out. |
| FR-025 | Sistem sebaiknya mencatat perubahan preferensi dan pengguna/sumber yang melakukan perubahan. | S | Riwayat perubahan dapat diaudit. |

### MOD-04 — Penyusunan dan Pengiriman Kabar Penggunaan Dana

| ID | Kebutuhan fungsional | Prioritas | Kriteria penerimaan ringkas |
| :--- | :--- | :--- | :--- |
| FR-030 | Sistem harus memungkinkan penyusunan draf kabar penggunaan dana yang terhubung dengan kampanye tertentu. | M | Draf memiliki kampanye dan isi pesan. |
| FR-031 | Sistem harus memperoleh daftar penerima yang mengikuti kampanye dari kontrak API subsistem terkait. | M | Daftar penerima berasal dari respons API yang sah. |
| FR-032 | Sistem harus menggunakan angka penggunaan dana dari subsistem Pelaporan Publik dan Transparansi Dana, bukan menghitungnya sendiri. | M | Sumber data tercatat dan angka tidak dibuat manual tanpa otorisasi. |
| FR-033 | Sistem harus memeriksa bahwa isi kabar tidak menyertakan data pribadi penerima manfaat yang tidak disetujui untuk dibagikan. | M | Konten diperiksa melalui aturan/proses review yang disepakati. |
| FR-034 | Sistem harus mendukung status draf dan status persetujuan apabila klien mengonfirmasi alur persetujuan. | S | Status draf/revisi/disetujui/ditolak berjalan sesuai peran. |
| FR-035 | Sistem harus menempatkan pengiriman massal ke antrean dan memproses penerima satu per satu. | M | Pekerjaan pengiriman dapat dilanjutkan setelah kegagalan parsial. |
| FR-036 | Sistem harus mencatat status pesan per penerima: Menunggu, Terkirim, Gagal, atau Dibatalkan. | M | Status per penerima dapat dilihat. |
| FR-037 | Sistem harus mencegah pesan yang telah terkirim terkirim ulang ketika antrean diproses ulang setelah kegagalan. | M | Uji retry tidak menggandakan pesan yang sukses. |
| FR-038 | Sistem harus menyediakan ringkasan hasil pengiriman per kampanye dan periode. | S | Jumlah status cocok dengan detail penerima. |

### MOD-05 — Pengiriman Bukti Donasi dan Rekapitulasi Tahunan

| ID | Kebutuhan fungsional | Prioritas | Kriteria penerimaan ringkas |
| :--- | :--- | :--- | :--- |
| FR-040 | Sistem harus menyediakan proses pengiriman bukti donasi berdasarkan data yang disediakan subsistem pemilik transaksi. | M | Bukti merujuk pada data transaksi dari sumber yang benar. |
| FR-041 | Sistem harus menyediakan proses pengiriman rekapitulasi tahunan berdasarkan data sumber yang disetujui BMTZ. | M | Periode, cakupan, dan sumber angka jelas. |
| FR-042 | Sistem harus mengirim melalui email dan kanal pesan yang dipilih setelah ketersediaan dan mekanisme integrasi dikonfirmasi. | M | Pengiriman hanya dilakukan pada kanal yang tersedia dan diizinkan. |
| FR-043 | Sistem harus mencatat status pengiriman bukti/rekap per penerima dan menyediakan penanganan kegagalan. | M | Status dan error yang tersedia tersimpan. |
| FR-044 | Sistem harus menghindari pengiriman bukti/rekap duplikat ketika proses diulang. | M | Retry tidak membuat duplikasi pengiriman yang tidak diinginkan. |

### MOD-06 — Antrean, Status, dan Pemulihan Pengiriman

| ID | Kebutuhan fungsional | Prioritas | Kriteria penerimaan ringkas |
| :--- | :--- | :--- | :--- |
| FR-050 | Sistem harus membuat pekerjaan antrean untuk pengiriman massal dan memprosesnya secara bertahap. | M | Pengiriman massal tidak bergantung pada satu permintaan sinkron yang panjang. |
| FR-051 | Sistem harus menyimpan status dan identitas unik pekerjaan per penerima. | M | Setiap penerima memiliki status sendiri. |
| FR-052 | Sistem harus memungkinkan pekerjaan gagal ditinjau dan dicoba ulang tanpa mengulang penerima yang sudah sukses. | M | Retry hanya memproses item yang memenuhi aturan retry. |
| FR-053 | Sistem harus mencatat waktu percobaan, status hasil, dan alasan kegagalan yang tersedia. | S | Log dapat digunakan untuk diagnosis. |

### MOD-07 — Laporan dan Pemantauan Operasional

| ID | Kebutuhan fungsional | Prioritas | Kriteria penerimaan ringkas |
| :--- | :--- | :--- | :--- |
| FR-060 | Sistem harus menampilkan ringkasan jumlah pesan terkirim, gagal, menunggu, dan dibatalkan untuk periode tertentu. | S | Angka ringkasan konsisten dengan detail status. |
| FR-061 | Sistem harus menyediakan daftar tiket keluhan berdasarkan status, petugas, dan periode. | S | Daftar laporan sesuai filter. |
| FR-062 | Sistem sebaiknya menyediakan ringkasan waktu penyelesaian keluhan setelah target SLA disepakati. | C | Perhitungan memakai definisi waktu yang disetujui. |
| FR-063 | Sistem harus membatasi laporan dan detail yang mengandung data pribadi sesuai hak akses. | M | Peran tanpa izin tidak dapat mengakses data terbatas. |

### MOD-08 — Pengguna, Hak Akses, dan Audit

| ID | Kebutuhan fungsional | Prioritas | Kriteria penerimaan ringkas |
| :--- | :--- | :--- | :--- |
| FR-070 | Sistem harus mengautentikasi pengguna internal sebelum mengakses fungsi yang dilindungi. | M | Pengguna tanpa sesi sah ditolak. |
| FR-071 | Sistem harus mengotorisasi tindakan berdasarkan peran dan kewenangan yang disetujui BMTZ. | M | Akses lintas peran diuji. |
| FR-072 | Sistem harus mencatat aktivitas sensitif seperti perubahan preferensi, penugasan tiket, persetujuan, dan perubahan konfigurasi. | S | Log audit menyimpan aktor, waktu, dan tindakan. |
| FR-073 | Sistem tidak boleh menyimpan kredensial produksi atau secret dalam repository kode. | M | Secret scanning tidak menemukan kredensial yang ditanam di kode. |

---

## 6. Kebutuhan Antarmuka Eksternal

### 6.1 Antarmuka Perangkat Lunak / API

| ID | Sistem terkait | Data / fungsi yang dibutuhkan | Ketentuan |
| :--- | :--- | :--- | :--- |
| IF-001 | Penerimaan Donasi dan Akun Donatur | Identitas donatur dan riwayat pemberian | Gunakan kontrak API; jangan membuat foreign key lintas subsistem; gunakan data sintetis saat kontrak belum tersedia. |
| IF-002 | Manajemen Kampanye Penghimpunan | Daftar donatur per kampanye | Penerima kabar ditentukan berdasarkan kampanye yang diikuti dan respons API. |
| IF-003 | Donasi Berulang dan Kanal Pembayaran Digital | Status kesediaan donasi berulang | Gunakan untuk menyesuaikan kabar yang relevan; makna status harus dikonfirmasi. |
| IF-004 | Pelaporan Publik dan Transparansi Dana | Angka penggunaan dana / informasi laporan yang disetujui | Subsistem ini tidak menjadi sumber kebenaran angka penggunaan dana. |
| IF-005 | Penyedia email/pesan | Pengiriman keluar dan status hasil, jika didukung provider | Provider, autentikasi, biaya, rate limit, webhook, dan kebijakan retry perlu diputuskan. |

### 6.2 Antarmuka Pengguna
Rancangan tampilan final bukan bagian dari SRS ini, tetapi aplikasi perlu menyediakan akses yang jelas ke riwayat donatur, tiket keluhan, preferensi komunikasi, draf kabar, antrean/status pengiriman, dan laporan.

### 6.3 Antarmuka Komunikasi
Kanal yang disebut workbook adalah email dan pesan untuk pengiriman bukti/rekap; kanal masuk yang lain (telepon, surat, media sosial) masih perlu dikonfirmasi. Bila sebuah kanal tidak dapat diintegrasikan, petugas dapat memerlukan pencatatan manual ke riwayat, sesuai keputusan klien.

### 6.4 Format dan Validasi Data
- Validasi format kontak dan alamat kanal dilakukan sesuai aturan provider serta data sumber.
- Timestamp disimpan dengan zona waktu yang disepakati dan ditampilkan secara konsisten.
- Pesan dan status pengiriman harus mempunyai identitas unik untuk mencegah duplikasi.
- Kesalahan validasi pengguna harus dibedakan dari kegagalan server/provider.
- Data dari API eksternal divalidasi sebelum digunakan; kegagalan API tidak boleh diam-diam dianggap sebagai data kosong yang valid.

---

## 7. Kebutuhan Nonfungsional

| ID | Aspek | Kebutuhan | Cara verifikasi | Prioritas |
| :--- | :--- | :--- | :--- | :--- |
| NFR-001 | Keamanan akses | Sistem harus membatasi akses berdasarkan autentikasi dan otorisasi peran. | Uji akses dengan akun berbeda; tindakan tak berizin ditolak. | M |
| NFR-002 | Kerahasiaan data | Data donatur dan riwayat komunikasi hanya ditampilkan kepada pengguna berwenang. | Uji akses positif/negatif dan pemeriksaan log. | M |
| NFR-003 | Perlindungan data | Penggunaan data asli hanya setelah dokumen pemrosesan data dan NDA yang diawajibkan workbook ditandatangani; sebelum itu gunakan data sintetis. | Periksa konfigurasi dan dataset pengembangan. | M |
| NFR-004 | Manajemen secret | Kredensial produksi, token, dan signing key tidak boleh disimpan di repository. | Secret scanning pada pipeline lulus. | M |
| NFR-005 | Keandalan pengiriman | Pemrosesan antrean harus dapat dilanjutkan setelah kegagalan parsial tanpa mengirim ulang item sukses. | Uji retry dan simulasi worker berhenti di tengah proses. | M |
| NFR-006 | Integritas preferensi | Opt-out terbaru diperiksa tepat sebelum pesan dikirim. | Uji: penerima berhenti setelah daftar dibuat tetapi sebelum pengiriman. | M |
| NFR-007 | Privasi konten | Kabar tidak boleh membocorkan data pribadi penerima manfaat yang tidak disetujui. | Review konten dan skenario uji kebocoran. | M |
| NFR-008 | Keterlacakan | Perubahan preferensi, status tiket, dan status pesan penting harus memiliki jejak audit sesuai kebijakan. | Periksa log dengan aktor, waktu, dan tindakan. | S |
| NFR-009 | Kinerja | Target waktu respons dan volume pengiriman ditentukan setelah volume aktual dan batas provider diketahui. | Uji beban berdasarkan target yang disepakati. | TBD |
| NFR-010 | Ketersediaan | Target uptime, jendela pemeliharaan, dan pemulihan ditetapkan bersama klien. | Review konfigurasi monitoring dan hasil uji pemulihan. | TBD |
| NFR-011 | Pemeliharaan | Konfigurasi kanal dan kredensial dikelola di luar kode dan dapat diganti tanpa perubahan kode yang tidak perlu. | Review konfigurasi dan prosedur rotasi secret. | S |
| NFR-012 | Observabilitas | Sistem harus mencatat error integrasi dan status antrean tanpa mengekspos data pribadi secara berlebihan. | Uji dashboard/log; periksa redaksi data sensitif. | S |
| NFR-013 | Kompatibilitas integrasi | Kontrak API harus didokumentasikan dan divalidasi terhadap implementasi. | Validasi OpenAPI dan tes kontrak pada pipeline. | M |
| NFR-014 | Kepatuhan proses | Baseline SRS memiliki versi, tanggal, dan persetujuan narasumber; perubahan setelah sign-off mengikuti change control. | Audit dokumen dan riwayat perubahan. | M |

---

## 8. Use Case

### 8.1 Daftar Use Case

| ID | Use case | Aktor utama | Hasil |
| :--- | :--- | :--- | :--- |
| UC-01 | Mencatat interaksi donatur | Petugas layanan donatur | Interaksi tersimpan pada riwayat. |
| UC-02 | Mencatat dan menindaklanjuti keluhan | Petugas layanan donatur / supervisor | Tiket tercatat sampai selesai. |
| UC-03 | Memperbarui preferensi komunikasi | Petugas berwenang / kanal masuk yang disepakati | Preferensi terbaru tersimpan. |
| UC-04 | Menyusun kabar penggunaan dana | Penyusun komunikasi | Draf terkait kampanye tersedia. |
| UC-05 | Menyetujui kabar (jika diwajibkan) | Supervisor / penyetuju | Draf disetujui, direvisi, atau ditolak. |
| UC-06 | Mengirim kabar kampanye | Petugas berwenang / proses antrean | Status tercatat per penerima; opt-out dihormati. |
| UC-07 | Mengirim bukti donasi | Petugas / proses otomatis sesuai desain | Status bukti donasi tercatat. |
| UC-08 | Mengirim rekapitulasi tahunan | Petugas / proses terjadwal sesuai desain | Status pengiriman rekap tercatat. |
| UC-09 | Melihat laporan operasional | Pimpinan / petugas berwenang | Ringkasan dan daftar detail tersedia. |

### 8.2 Use Case Rinci UC-06 — Mengirim Kabar Kampanye

| Elemen | Deskripsi |
| :--- | :--- |
| Tujuan | Mengirim kabar penggunaan dana kepada donatur yang mengikuti kampanye tertentu dan masih memilih menerima jenis kabar tersebut. |
| Aktor | Penyusun komunikasi, penyetuju jika berlaku, worker antrean, API kampanye, API pelaporan dana, provider pesan/email. |
| Prasyarat | Pengguna terautentikasi; data kampanye dan angka penggunaan dana tersedia; kanal pengiriman terkonfigurasi; aturan persetujuan ditentukan. |
| Pemicu | Petugas mengajukan pengiriman kabar kampanye. |
| Alur utama | 1. Petugas memilih kampanye dan membuat/meninjau naskah.<br>2. Sistem mengambil angka penggunaan dana dari sumber yang ditetapkan.<br>3. Sistem mengambil daftar donatur yang mengikuti kampanye melalui API.<br>4. Jika disyaratkan, naskah melalui persetujuan.<br>5. Sistem membuat pekerjaan antrean per penerima.<br>6. Tepat sebelum mengirim setiap pesan, sistem memeriksa preferensi terbaru.<br>7. Jika diizinkan, pesan dikirim dan status dicatat.<br>8. Jika tidak diizinkan, item ditandai dibatalkan.<br>9. Sistem menyajikan ringkasan hasil. |
| Alur alternatif A1 | Data API kampanye tidak tersedia: pengiriman tidak dimulai; tampilkan error dan catat kegagalan integrasi. |
| Alur alternatif A2 | Penerima sudah opt-out: pesan untuk penerima tersebut dibatalkan; penerima lain tetap dapat diproses. |
| Alur alternatif A3 | Provider gagal mengirim: catat status gagal dan alasan yang tersedia; item dapat dicoba ulang sesuai kebijakan. |
| Alur alternatif A4 | Worker berhenti setelah sebagian pesan terkirim: saat dilanjutkan, pesan sukses tidak dikirim ulang; item yang belum selesai diproses berdasarkan status. |
| Alur alternatif A5 | Naskah ditolak: pengiriman tidak dimulai; petugas memperbaiki naskah sesuai catatan reviewer. |
| Pasca kondisi | Setiap penerima mempunyai status akhir/sementara yang dapat ditelusuri; preferensi opt-out tetap dihormati. |
| Kriteria sukses | Tidak ada penerima yang mendapat jenis kabar setelah opt-out aktif; pesan sukses tidak digandakan saat retry; status setiap penerima tercatat. |

### 8.3 Use Case Rinci UC-02 — Menangani Keluhan

| Elemen | Deskripsi |
| :--- | :--- |
| Tujuan | Mencatat, menugaskan, menindaklanjuti, dan menutup pertanyaan atau keluhan donatur. |
| Aktor | Petugas layanan donatur; supervisor bila diperlukan. |
| Prasyarat | Petugas berwenang; kanal dan data yang tersedia dapat dicatat. |
| Alur utama | 1. Petugas menerima keluhan.<br>2. Petugas mencari donatur jika teridentifikasi.<br>3. Petugas membuat tiket dan mencatat kanal, waktu, ringkasan, serta prioritas.<br>4. Sistem memberi nomor tiket.<br>5. Tiket ditugaskan.<br>6. Petugas mencatat tindak lanjut.<br>7. Setelah solusi disepakati, petugas mencatat penyelesaian.<br>8. Tiket ditutup dan riwayat tetap tersedia. |
| Alur alternatif | Jika donatur tidak teridentifikasi, catat sebagai interaksi anonim sesuai aturan; jangan mengarang identitas. Jika belum selesai, status tetap terbuka dan penanggung jawab melanjutkan tindak lanjut. |
| Pasca kondisi | Tiket dan riwayat tindak lanjut tersimpan; status serta penanggung jawab dapat dilihat oleh pengguna berwenang. |

---

## 9. Data dan Informasi yang Dikelola

### 9.1 Entitas Konseptual

| Entitas | Atribut konseptual | Sumber / pemilik |
| :--- | :--- | :--- |
| Referensi Donatur | ID referensi eksternal, nama/label yang diizinkan, kanal kontak yang tersedia | API Penerimaan Donasi dan Akun Donatur; jangan menjadikan subsistem ini sumber identitas utama. |
| Preferensi Komunikasi | ID referensi donatur, jenis kabar, status izin, waktu perubahan, sumber perubahan | Subsistem ini; aturan dan otorisasi perlu divalidasi. |
| Catatan Komunikasi | ID, ID referensi donatur jika diketahui, waktu, kanal, arah masuk/keluar, ringkasan, petugas, status | Subsistem ini. |
| Tiket Keluhan | ID tiket, referensi donatur, kategori, prioritas, status, penanggung jawab, waktu masuk/selesai | Subsistem ini. |
| Kampanye Referensi | ID kampanye, nama/label, status relevan | API Manajemen Kampanye Penghimpunan. |
| Kabar / Pesan | ID pesan, kampanye, naskah/versi, pembuat, persetujuan jika berlaku, jenis kabar | Subsistem ini; sumber angka penggunaan dana berasal dari API yang ditentukan. |
| Item Pengiriman | ID pekerjaan, ID penerima referensi, kanal, status, waktu percobaan, hasil/error | Subsistem ini. |
| Bukti / Rekap Pengiriman | Referensi transaksi/periode, tujuan kanal, status dan waktu pengiriman | Data sumber dari subsistem pemilik; pencatatan pengiriman di subsistem ini. |
| Audit Log | Aktor, tindakan, waktu, objek yang berubah, hasil | Subsistem ini sesuai kebijakan akses. |

### 9.2 Kualitas dan Privasi Data
- Gunakan ID referensi dari API untuk menghubungkan data lintas subsistem; jangan membuat foreign key lintas database.
- Minimalkan penyimpanan data pribadi yang tidak diperlukan untuk fungsi komunikasi.
- Batasi isi log dan pesan error agar tidak membocorkan informasi pribadi atau kredensial.
- Bedakan identitas anonim yang ditampilkan kepada publik dengan preferensi menerima kabar.
- Tentukan masa retensi dan prosedur koreksi/penghapusan bersama klien serta pihak yang bertanggung jawab atas kepatuhan.

---

## 10. Kriteria Penerimaan Sistem

| ID | Skenario penerimaan | Kondisi lulus |
| :--- | :--- | :--- |
| AT-01 | Petugas mencatat interaksi donatur yang teridentifikasi. | Catatan tersimpan dan terlihat pada riwayat donatur yang benar. |
| AT-02 | Petugas membuat keluhan dan menugaskan penanggung jawab. | Tiket memiliki ID, status, dan petugas; perubahan dapat ditelusuri. |
| AT-03 | Donatur berhenti menerima kabar setelah daftar penerima dibuat tetapi sebelum pengiriman. | Pada waktu pengiriman, sistem memeriksa preferensi terbaru dan membatalkan item tersebut. |
| AT-04 | Pengiriman massal gagal setelah sebagian pesan berhasil. | Saat proses dilanjutkan, pesan yang telah sukses tidak terkirim ulang. |
| AT-05 | API sumber angka penggunaan dana tidak tersedia. | Sistem tidak mengarang atau menggunakan angka sebagai seolah-olah valid; pengiriman ditahan dan error dicatat. |
| AT-06 | Konten kabar memuat data pribadi penerima manfaat yang tidak disetujui. | Proses review/aturan yang disepakati mencegah pengiriman konten tersebut. |
| AT-07 | Pengguna tanpa hak akses mencoba melihat data terbatas. | Akses ditolak dan peristiwa dicatat sesuai kebijakan. |
| AT-08 | Petugas mengirim bukti donasi atau rekapitulasi tahunan. | Sumber data, tujuan, waktu, dan status pengiriman dapat ditelusuri. |
| AT-09 | Provider gagal mengirim ke salah satu penerima. | Item penerima berstatus gagal dengan alasan yang tersedia; penerima lain tetap diproses. |
| AT-10 | SRS akan menjadi baseline. | Versi, tanggal, narasumber/pemilik kebutuhan, review, dan persetujuan tercatat. |

---

## 11. Matriks Keterlacakan Kebutuhan (RTM) — Draf

Matriks berikut menghubungkan kebutuhan dengan lingkup workbook dan pengujian penerimaan. Setelah wawancara, tambahkan referensi ke catatan wawancara, stakeholder, user story, dan use case final.

| Kebutuhan | Sumber / alasan | Use case | Uji penerimaan |
| :--- | :--- | :--- | :--- |
| FR-001-004 | Workbook 3.2: riwayat percakapan per donatur | UC-01 | AT-01 |
| FR-010-015 | Workbook 3.2: keluhan/pertanyaan beserta penyelesaian dan petugas | UC-02 | AT-02 |
| FR-020-025; BR-01; BR-07 | Workbook 3.2 dan risiko 3.6-3.7: pilihan kabar/opt-out | UC-03, UC-06 | AT-03 |
| FR-030-038; BR-02-04 | Workbook 3.2, 3.6, 3.7: kabar penggunaan dana, antrean, status per penerima, pencegahan duplikasi | UC-04, UC-05, UC-06 | AT-04, AT-05, AT-06, AT-09 |
| FR-040-044 | Workbook 3.2: bukti donasi dan rekapitulasi tahunan | UC-07, UC-08 | AT-08 |
| FR-050-054; NFR-005; NFR-006 | Workbook 3.7: antrean, status, opt-out saat pengiriman | UC-06 | AT-03, AT-04, AT-09 |
| FR-060-063 | Kebutuhan operasional turunan; perlu konfirmasi klien | UC-09 | AT-01, AT-02 |
| FR-070-073; NFR-001-004; NFR-008 | Workbook 2.1 dan kebutuhan keamanan/akses | Semua use case terlindungi | AT-07 |

---

## 12. Risiko dan Mitigasi Awal

| ID | Risiko | Dampak | Mitigasi / kontrol | Pemilik (dilihat) |
| :--- | :--- | :--- | :--- | :--- |
| R-01 | Donatur opt-out tetap menerima kabar. | Pelanggaran preferensi, hilangnya kepercayaan. | Periksa preferensi pada saat pengiriman untuk setiap penerima; uji kasus perubahan preferensi setelah antrean dibuat. | [Belum ditentukan] |
| R-02 | Pesan terkirim dua kali setelah retry. | Gangguan dan pengalaman donatur buruk. | Status per penerima, ID unik, idempotensi, serta pengujian worker gagal di tengah proses. | [Belum ditentukan] |
| R-03 | Naskah kabar membocorkan data pribadi penerima manfaat. | Risiko privasi dan kepatuhan. | Minimisasi data, review konten, aturan redaksi, pembatasan akses. | [Belum ditentukan] |
| R-04 | Riwayat komunikasi tidak lengkap. | Donatur harus mengulang keluhan; layanan tidak konsisten. | Satu riwayat per donatur yang teridentifikasi; proses pencatatan kanal manual/integrasi dikonfirmasi. | [Belum ditentukan] |
| R-05 | API subsistem hulu tidak tersedia atau berubah. | Pengiriman tertunda atau salah data. | Kontrak API berversi, stub integrasi, validasi kontrak, penanganan kegagalan yang jelas. | [Belum ditentukan] |
| R-06 | Volume dan batas provider tidak diketahui. | Antrean menumpuk atau provider membatasi pengiriman. | Ukur volume aktual, tentukan rate limit, metrik antrean dan mekanisme retry. | [Belum ditentukan] |
| R-07 | Data asli digunakan sebelum perjanjian ditandatangani. | Risiko kerahasiaan dan pelanggaran proses. | Gunakan data sintetis sampai dokumen pemrosesan data dan NDA ditandatangani. | [Belum ditentukan] |
| R-08 | Persetujuan naskah tidak jelas. | Pesan tidak akurat atau tidak berwenang dikirim. | Tentukan pemilik konten, approver, status dan bukti persetujuan saat wawancara. | [Belum ditentukan] |

---

## 13. Operasional, Deployment, dan Dukungan

SRS ini mendefinisikan kebutuhan operasional tingkat tinggi; keputusan rinci disimpan pada dokumen rancangan dan Architecture Decision Record (ADR).

- Setiap lingkungan (pengembangan, pengujian, produksi) harus memiliki konfigurasi dan secret yang dipisahkan.
- Pipeline harus menjalankan test suite, pemeriksaan secret, validasi kontrak API, dan pemeriksaan health endpoint sesuai workbook.
- Log operasional harus membantu diagnosis antrean, provider, API, dan tiket tanpa memuat data pribadi secara berlebihan.
- Harus ada prosedur pemulihan pekerjaan antrean dan rekonsiliasi status setelah kegagalan.
- Runbook cutover harus menjelaskan konfigurasi, migrasi yang diperlukan, pemeriksaan pascadeployment, pemantauan, dan prosedur rollback.
- Data produksi tidak boleh disalin ke lingkungan pengembangan tanpa otorisasi dan kontrol yang sesuai.

---

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

---

## 15. Lampiran

### Lampiran A — Daftar Fungsi per Modul (Ringkasan)

| Modul | Fungsi utama | Prioritas awal |
| :--- | :--- | :--- |
| MOD-01 Riwayat Komunikasi | Melihat, mencatat, mencari dan menelusuri interaksi donatur. | M/S |
| MOD-02 Keluhan dan Pertanyaan | Membuat tiket, menetapkan petugas, memperbarui status, mencatat solusi dan mencari tiket. | M/S |
| MOD-03 Preferensi Komunikasi | Mencatat jenis kabar, opt-out, perubahan preferensi dan memeriksa preferensi saat kirim. | M |
| MOD-04 Kabar Penggunaan Dana | Menyusun kabar per kampanye, mengambil data sumber, persetujuan jika perlu, antrean dan status penerima. | M/S |
| MOD-05 Bukti Donasi dan Rekap Tahunan | Menyiapkan dan mengirim bukti/rekap dari data sumber dengan status dan retry aman. | M |
| MOD-06 Antrean dan Pemulihan | Memproses per penerima, mencatat status, retry aman, rate limit dan diagnosis kegagalan. | M/S |
| MOD-07 Laporan Operasional | Ringkasan pesan, status keluhan, laporan periode, pembatasan akses. | S/C |
| MOD-08 Pengguna, Hak Akses, Audit | Autentikasi, otorisasi, audit aktivitas sensitif dan perlindungan secret. | M/S |

### Lampiran B — Checklist Validasi dengan Klien

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

### Lampiran C — Catatan Kepatuhan dan Penggunaan Dokumen

Dokumen ini merupakan draf kerja yang disusun berdasarkan workbook proyek yang tersedia. Dokumen ini mengacu pada praktik rekayasa kebutuhan ISO/IEC/IEEE 29148:2018, tetapi tidak menyatakan sertifikasi atau kepatuhan formal penuh terhadap standar. Struktur, prioritas, target, antarmuka, dan kebutuhan harus diperiksa serta disesuaikan dengan hasil elisitasi, review dosen, review klien, dan sign-off.

Data donatur bersifat sensitif. Jangan menambahkan data pribadi nyata, token, password, API key, atau kredensial produksi ke dokumen maupun repository. Gunakan data sintetis sampai semua persyaratan persetujuan pemrosesan data dan kerahasiaan pada workbook terpenuhi.
