# FUNCTIONAL REQUIREMENT

## FR-012 — MEMBATALKAN DONASI BERULANG

**Sistem Donasi Berulang dan Kanal Pembayaran Digital**

| Informasi Dokumen | Keterangan |
| :--- | :--- |
| **Organisasi** | Baitulmal Tazkia |
| **ID Kebutuhan** | FR-012 |
| **Versi Dokumen** | 1.0 |
| **Tanggal acuan** | 26 Oktober 2026 (SRS Draft v0.2) |
| **Status** | Dokumen finalisasi kebutuhan; persetujuan aturan bisnis masih diperlukan |
| **Prioritas** | Belum ditetapkan dalam SRS Draft v0.2 |

### 1. Identitas dan Tujuan Kebutuhan

| Elemen | Uraian |
| :--- | :--- |
| **Nama kebutuhan** | Membatalkan Donasi Berulang |
| **Aktor utama** | Donatur dan sistem |
| **Tujuan** | Memungkinkan donatur membatalkan kesediaan donasi berulang sehingga tidak ada penjadwalan baru setelah pembatalan efektif. Transaksi yang telah berjalan ditangani secara terpisah. |
| **Pemicu** | Donatur memilih tindakan pembatalan donasi berulang. |
| **Kondisi awal** | Fitur pengelolaan donasi berulang dan autentikasi donatur tersedia. Donasi berulang telah terdaftar melalui FR-004. |
| **Batasan** | FR-012 hanya mencakup pembatalan kesediaan donasi berulang. Jeda donasi dibahas pada FR-011; pendaftaran kesediaan dan jadwal awal pada FR-004; pemrosesan penagihan pada FR-006; pengingat/notifikasi pada FR-005 dan FR-013. Pengembalian dana tidak termasuk dalam FR-012. |

### 2. Deskripsi Functional Requirement

Sistem harus memungkinkan donatur mengajukan pembatalan donasi berulang. Sistem harus memvalidasi permintaan sebelum memperbarui status kesediaan atau jadwal donasi sesuai aturan bisnis yang disepakati. Apabila tagihan sedang diproses ketika permintaan pembatalan diajukan, sistem harus menerapkan aturan yang disepakati dan menampilkan statusnya dengan jelas. Sistem tidak boleh menjanjikan bahwa transaksi yang sudah berjalan pasti dapat dihentikan. Setelah pembatalan efektif, sistem tidak boleh membuat penjadwalan donasi baru sesuai aturan yang disepakati.

### 3. Proses Bisnis

**Aktor:** Donatur dan sistem. *(Prasyarat: donasi berulang telah terdaftar melalui FR-004).*

| No. | Aktivitas | Dasar / Status |
| :--- | :--- | :--- |
| 1 | Donatur memilih tindakan pembatalan pada donasi berulang. | Tertulis di SRS |
| 2 | Sistem memastikan fitur tersedia dan donatur telah melalui mekanisme autentikasi yang berlaku. | Kondisi awal SRS; mekanisme perlu dikonfirmasi |
| 3 | Sistem memvalidasi permintaan pembatalan dan kewenangan donatur atas donasi tersebut. | Tertulis di SRS; detail validasi perlu dikonfirmasi |
| 4 | Jika valid, sistem memperbarui status kesediaan atau jadwal sesuai aturan pembatalan yang disepakati. | Tertulis di SRS; aturan efektif perlu dikonfirmasi |
| 5 | Setelah pembatalan efektif, sistem tidak membuat penjadwalan baru untuk donasi tersebut. | Kriteria penerimaan SRS |
| 6 | Sistem mencatat status pembatalan dan waktu berlakunya agar dapat ditelusuri. | Disimpulkan dari NFR-005 dan ALT-07; detail pencatatan perlu dikonfirmasi |

#### 3.1 Alur Alternatif: Tagihan Sedang Diproses

* Sistem memeriksa status tagihan dan menerapkan aturan efektif pembatalan yang telah disepakati.
* Sistem menampilkan status tagihan atau hasil penanganannya secara jelas kepada donatur.
* Sistem tidak menjanjikan bahwa transaksi yang sudah berjalan pasti dapat dihentikan.
* Transaksi yang telah berjalan ditangani terpisah dari pembatalan kesediaan donasi berulang.

> *Catatan: Waktu efektif pembatalan dan dampaknya terhadap tagihan yang sedang berjalan masih memerlukan keputusan bisnis (SRS OQ-012).*

#### 3.2 Alur Alternatif: Validasi Gagal atau Donasi Tidak Dapat Dibatalkan

* Sistem tidak mengubah status kesediaan maupun jadwal donasi apabila permintaan tidak lolos validasi atau donasi tidak memenuhi ketentuan pembatalan.
* Sistem menampilkan informasi kegagalan atau alasan donasi tidak dapat dibatalkan sesuai pesan dan aturan yang nantinya disetujui.

> *Catatan: Daftar kondisi yang menyebabkan pembatalan ditolak serta redaksi pesan kepada donatur perlu dikonfirmasi.*

### 4. Data dan Validasi

*SRS Draft v0.2 belum menetapkan nama field teknis, tipe data, maupun aturan validasi rinci untuk FR-012. Daftar berikut merupakan kebutuhan data konseptual untuk dibahas, bukan keputusan skema basis data.*

| Data yang Diperlukan | Kegunaan / Validasi | Status |
| :--- | :--- | :--- |
| **Referensi donasi berulang** | Mengidentifikasi donasi yang diminta untuk dibatalkan dan memastikan donasi tersebut berada dalam cakupan kewenangan donatur. | Format dan sumber referensi perlu dikonfirmasi |
| **Identitas dan hak akses donatur** | Memastikan permintaan berasal dari donatur yang berhak sebelum status diubah. | Mekanisme autentikasi/otorisasi perlu dikonfirmasi |
| **Permintaan pembatalan** | Menjadi dasar pemrosesan sesuai aturan efektif pembatalan. | Aturan dan tahapan konfirmasi perlu dikonfirmasi |
| **Status kesediaan donasi** | Mencerminkan status donasi berulang, termasuk status batal sesuai daftar status yang disepakati. | Daftar status dan transisi perlu dikonfirmasi |
| **Waktu efektif pembatalan** | Menentukan sejak kapan sistem menghentikan penjadwalan baru. | Aturan penentuan waktu perlu dikonfirmasi |
| **Status transaksi berjalan** | Memisahkan status pembatalan kesediaan dari status pembayaran yang sedang atau telah diproses. | Cara penanganan dan integrasi perlu dikonfirmasi |
| **Alasan pembatalan** | Dicatat hanya apabila organisasi menetapkan bahwa data ini diperlukan. | Kebutuhan pencatatan belum ditetapkan SRS |

### 5. Rancangan Antarmuka (UI)

*Rancangan berikut adalah gambaran elemen fungsional, bukan desain visual final. Tampilan mengikuti arahan awal SRS NFR-006: navy blue dan putih, serta identitas resmi Baitulmal Tazkia.*

#### 5.1 Kondisi Donatur Mengajukan Pembatalan

| Elemen UI | Isi / Perilaku |
| :--- | :--- |
| **Identitas halaman** | Kelola Donasi Berulang |
| **Informasi donasi** | Referensi donasi, nominal, jadwal, peruntukan, dan status donasi |
| **Aksi** | Tombol “Batalkan donasi” ditampilkan sesuai status dan ketentuan donasi yang dapat dibatalkan. |
| **Konfirmasi** | Sistem meminta konfirmasi pembatalan sesuai aturan yang telah disetujui. Teks konfirmasi belum ditetapkan. |

#### 5.2 Kondisi Hasil Permintaan

| Kondisi | Informasi yang Ditampilkan |
| :--- | :--- |
| **Pembatalan diterima** | Status pembatalan dan waktu mulai berlakunya. Sistem menjelaskan bahwa tidak ada penjadwalan baru setelah pembatalan efektif. |
| **Tagihan sedang diproses** | Status tagihan dan informasi penanganan sesuai aturan efektif yang berlaku. Transaksi yang telah berjalan ditangani terpisah. |
| **Permintaan ditolak / tidak valid** | Informasi bahwa pembatalan tidak dapat diproses; status dan jadwal donasi tidak berubah. |

### 6. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Terkait FR-012 | Acuan |
| :--- | :--- | :--- |
| **Keamanan** | Hanya donatur yang berhak dapat mengajukan pembatalan. Permintaan divalidasi sebelum status diubah; data donatur dilindungi sesuai kebijakan yang disepakati. | NFR-001; OQ-013 |
| **Keandalan status** | Tidak ada penjadwalan baru setelah pembatalan efektif. Sistem tidak menjanjikan transaksi yang telah diproses dapat dihentikan dan tidak mengubah status pembayaran yang sudah ditetapkan. | NFR-002; ALT-07 |
| **Keterlacakan** | Status pembatalan dan waktu berlakunya dapat ditelusuri. | NFR-005 |
| **Kemudahan penggunaan** | Instruksi pembatalan dan status tagihan yang sedang diproses ditampilkan dengan jelas. | NFR-004 |
| **Tampilan** | Antarmuka mengikuti arahan awal warna navy blue dan putih serta identitas organisasi. | NFR-006 |
| **Integrasi** | Status batal yang diperlukan oleh kelompok 11 disediakan melalui kontrak integrasi yang disepakati. | NFR-003; OQ-008 |

### 7. Kriteria Penerimaan

* [ ] Sistem menerima permintaan pembatalan dari donatur melalui fitur pengelolaan donasi berulang.
* [ ] Sistem memvalidasi permintaan sebelum mengubah status kesediaan atau jadwal donasi.
* [ ] Permintaan yang tidak lolos validasi tidak mengubah status maupun jadwal donasi.
* [ ] Setelah pembatalan efektif, sistem tidak membuat penjadwalan baru untuk donasi tersebut.
* [ ] Transaksi yang telah berjalan ditangani terpisah dari pembatalan kesediaan donasi berulang.
* [ ] Jika tagihan sedang diproses, sistem menerapkan aturan yang disepakati dan menampilkan statusnya dengan jelas.
* [ ] Sistem tidak menyatakan atau menjanjikan bahwa transaksi yang sudah berjalan pasti dapat dihentikan.
* [ ] Status pembatalan dan waktu efektifnya dapat ditelusuri sesuai kebijakan pencatatan yang disepakati.

> *Catatan: Kriteria yang bergantung pada aturan efektif, status transaksi, autentikasi, dan pencatatan hanya dapat diuji secara final setelah keputusan bisnis terkait disepakati.*

### 8. Keputusan Bisnis yang Masih Memerlukan Konfirmasi

*Butir berikut merupakan keputusan terbuka yang tidak ditetapkan oleh SRS Draft v0.2. Butir ini harus disepakati oleh Baitulmal Tazkia sebelum FR-012 dinyatakan disetujui untuk implementasi.*

1. Bagaimana pembatalan berlaku apabila penagihan sedang diproses, dan apa dampaknya terhadap tagihan yang berjalan? (OQ-012; ALT-07)
2. Kapan pembatalan mulai efektif: segera, pada akhir periode berjalan, atau berdasarkan batas waktu sebelum tanggal penagihan? (OQ-003)
3. Status donasi apa yang dapat dibatalkan? Apakah donasi yang sedang dijeda (FR-011) juga dapat dibatalkan?
4. Apakah pembatalan bersifat final, atau donatur dapat mendaftar ulang/mengaktifkan kembali donasi?
5. Bagaimana autentikasi dan validasi hak donatur dilakukan? Apakah konfirmasi ulang diwajibkan?
6. Apakah pengingat dan penagihan terjadwal yang sudah ada dihentikan setelah pembatalan efektif? (FR-005, FR-006, FR-013)
7. Apakah pembatalan perlu diteruskan ke Payment Gateway Artivisi untuk metode yang mendukung penagihan otomatis, termasuk pencabutan persetujuan? (OQ-001, OQ-002)
8. Apakah penghentian kesediaan akibat kegagalan tagihan berulang termasuk ruang lingkup FR-012, atau merupakan proses terpisah? (OQ-004)
9. Status apa yang dibutuhkan kelompok 11 dan kapan status batal disinkronkan? (OQ-008)
10. Apakah donatur menerima konfirmasi pembatalan, siapa pengirimnya, dan apakah alasan pembatalan perlu dicatat?
11. Apakah staf internal dapat membatalkan donasi atas permintaan donatur?
12. Bagaimana aturan akses, retensi, kepemilikan riwayat pembatalan, dan target waktu respons ditetapkan? (OQ-013, OQ-014)

### 9. Batasan dan Ketergantungan

* **FR-004:** Pendaftaran kesediaan donasi berulang dan penyimpanan jadwal awal.
* **FR-005 dan FR-013:** Pengingat serta notifikasi.
* **FR-006:** Pemrosesan penagihan melalui *payment gateway*.
* **FR-011:** Jeda donasi berulang.
* **NFR-001 sampai NFR-006:** Keamanan, keandalan, integrasi, kemudahan penggunaan, keterlacakan, dan tampilan.
* **Kelompok 11:** Penerimaan/sinkronisasi status batal melalui kontrak integrasi yang disepakati.

### 10. Ringkasan untuk Validasi

* FR-012 menetapkan fungsi pembatalan donasi berulang oleh donatur. Hasil utama yang wajib dijaga adalah: (1) permintaan divalidasi sebelum status diubah; (2) setelah pembatalan efektif tidak ada penjadwalan baru; (3) transaksi yang telah berjalan ditangani secara terpisah; dan (4) sistem menampilkan status tagihan yang sedang diproses secara jelas tanpa menjanjikan bahwa transaksi tersebut pasti dapat dihentikan.
* Dokumen ini telah disusun sebagai versi finalisasi kebutuhan berdasarkan informasi yang tersedia pada SRS Draft v0.2. Dokumen belum dapat dianggap sebagai persetujuan final klien untuk aturan bisnis yang tercantum pada Bagian 8.

### 11. Referensi

SRS Draft v0.2: Bab 2.3; Bab 3.2 (ALT-07); Bab 4 (FR-012: pemicu, kondisi awal, alur utama, alur alternatif, dan kriteria penerimaan); NFR-001, NFR-002, NFR-003, NFR-004, NFR-005, NFR-006; serta OQ-001, OQ-002, OQ-003, OQ-004, OQ-008, OQ-012, OQ-013, dan OQ-014.