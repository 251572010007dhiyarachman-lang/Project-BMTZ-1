# FUNCTIONAL REQUIREMENT

## FR-014 — MEMBUAT TAUTAN PEMBAYARAN SATU KALI

**Sistem Donasi Berulang dan Kanal Pembayaran Digital**

### Riwayat dan Status Dokumen

| Atribut | Keterangan |
| :--- | :--- |
| **ID / Nama** | FR-014 — Membuat Tautan Pembayaran Satu Kali |
| **Versi sumber** | Draft Awal v0.1 |
| **Versi dokumen** | 1.0 |
| **Acuan** | SRS Draft v0.2, tanggal 26 Oktober 2026 |
| **Status** | Rumusan dan struktur kebutuhan telah difinalisasi berdasarkan materi yang tersedia. Detail bisnis dan integrasi yang belum tersedia tetap ditandai perlu konfirmasi. |

> *Catatan: “Final” pada dokumen ini berarti finalisasi dokumen kebutuhan berdasarkan sumber yang diberikan, bukan pernyataan bahwa seluruh aturan bisnis atau kontrak teknis telah disetujui klien.*

### 1. Identitas Kebutuhan

| Elemen | Uraian |
| :--- | :--- |
| **ID kebutuhan** | FR-014 |
| **Nama** | Membuat Tautan Pembayaran Satu Kali |
| **Aktor utama** | Penggalang dana atau staf yang berwenang; sistem; Payment Gateway Artivisi |
| **Pihak terkait** | Donatur sebagai penerima dan pengguna tautan pembayaran |
| **Tujuan** | Membuat tautan pembayaran satu kali melalui gateway untuk dibagikan dan, jika didukung, dipantau progresnya. |
| **Prioritas** | Belum ditentukan dalam SRS. |
| **Pemicu** | Penggalang dana atau staf yang berwenang meminta tautan pembayaran satu kali. |
| **Kondisi awal** | Pihak peminta berwenang dan aturan tautan sudah ditentukan. |

### 2. Deskripsi Kebutuhan Fungsional

Sistem harus menyediakan fungsi bagi penggalang dana atau staf yang berwenang untuk meminta pembuatan tautan pembayaran satu kali. Sistem membuat atau meminta tautan melalui Payment Gateway Artivisi sesuai mekanisme integrasi yang disepakati, kemudian mengembalikan tautan yang valid agar dapat dibagikan kepada donatur.

Tautan harus dapat digunakan sesuai masa berlakunya. Apabila gateway mendukung fasilitas pemantauan, sistem dapat menampilkan progres atau status tautan. Jika gateway gagal membuat tautan, sistem harus menampilkan informasi kegagalan dan tidak mengembalikan tautan yang tidak valid.

Pembayaran melalui tautan tetap mengikuti proses verifikasi transaksi. Sistem tidak boleh menyatakan pembayaran berhasil sebelum menerima hasil yang terverifikasi sesuai FR-007 dan NFR-002.

### 3. Ruang Lingkup dan Batasan

**Termasuk dalam ruang lingkup:**
* Menerima permintaan pembuatan tautan dari pihak yang berwenang.
* Memastikan prasyarat kewenangan dan aturan tautan telah ditentukan.
* Membuat atau meminta tautan melalui Payment Gateway Artivisi.
* Mengembalikan tautan pembayaran yang valid untuk dibagikan kepada donatur.
* Menyediakan pemantauan progres apabila fitur tersebut didukung gateway.
* Menangani kegagalan pembuatan tautan agar tautan tidak valid tidak dibagikan.

**Di luar ruang lingkup:**
* Pemrosesan pembayaran dilakukan oleh Payment Gateway Artivisi.
* Verifikasi status transaksi mengikuti FR-007.
* Pengiriman catatan donasi ke kelompok 1 mengikuti FR-009.
* Pencegahan pencatatan ganda mengikuti FR-015.
* Pendaftaran, jeda, dan pembatalan donasi berulang tidak dibahas dalam FR-014.

### 4. Alur Proses Bisnis

| No. | Langkah | Dasar |
| :--- | :--- | :--- |
| 1 | Penggalang dana atau staf yang berwenang meminta tautan pembayaran satu kali. | Tertulis di SRS |
| 2 | Sistem memastikan pihak peminta berwenang dan aturan tautan telah ditentukan. | Disimpulkan dari kondisi awal SRS |
| 3 | Sistem membuat atau meminta tautan melalui gateway sesuai integrasi. | Tertulis di SRS |
| 4 | Sistem mengembalikan tautan yang valid untuk dibagikan. | Tertulis di SRS |
| 5 | Sistem menyediakan pemantauan progres tautan apabila fitur didukung. | Tertulis di SRS sebagai kriteria penerimaan |
| 6 | Pembayaran melalui tautan hanya dinyatakan berhasil setelah hasilnya terverifikasi. | Disimpulkan dari SRS Bab 2.1, NFR-002, dan FR-007 |

#### 4.1 Alur Alternatif

| Kondisi | Perilaku Sistem | Hal yang Perlu Dikonfirmasi |
| :--- | :--- | :--- |
| **Gateway gagal membuat tautan** | Sistem menampilkan kegagalan dan tidak mengembalikan tautan yang tidak valid. | Aturan pengulangan permintaan, jumlah percobaan, dan pesan kegagalan. |
| **Peminta tidak berwenang** | Sistem tidak membuat tautan. | Mekanisme verifikasi identitas dan kewenangan. |
| **Tautan kedaluwarsa atau sudah digunakan** | Tautan hanya dapat digunakan sesuai masa berlaku. | Definisi “satu kali” dan perlakuan setelah tautan digunakan/kedaluwarsa. |
| **Status pembayaran pending, timeout, atau belum diterima** | Sistem tidak menyatakan berhasil atau gagal tanpa dasar hasil terverifikasi. | Pemetaan status gateway, waktu tunggu, dan mekanisme pengecekan. |
| **Hasil gateway diterima lebih dari sekali** | Referensi transaksi unik digunakan untuk mencegah pencatatan ganda sesuai FR-015. | Detail teknis idempotensi dan kontrak integrasi. |

### 5. Data dan Validasi

*SRS Draft v0.2 belum menetapkan nama field, tipe data, maupun aturan validasi terperinci untuk FR-014. Daftar berikut merupakan kebutuhan data konseptual untuk dikonfirmasi, bukan rancangan skema basis data final.*

| Data Konseptual | Tipe Data | Aturan Awal | Status |
| :--- | :--- | :--- | :--- |
| **Pihak peminta** | Belum ditentukan | Hanya penggalang dana atau staf berwenang. | Konfirmasi identitas dan verifikasi kewenangan. |
| **Nominal** | Belum ditentukan | Belum ditetapkan apakah nominal tetap atau bebas. | Perlu konfirmasi. |
| **Peruntukan/program** | Belum ditentukan | Keterkaitan tautan dengan program belum dijelaskan. | Konfirmasi apakah wajib. |
| **Masa berlaku** | Belum ditentukan | Tautan digunakan sesuai masa berlaku. | Konfirmasi durasi dan aturan kedaluwarsa. |
| **Tautan pembayaran** | Belum ditentukan | Tautan yang dikembalikan harus valid. | Konfirmasi format dan respons gateway. |
| **Referensi tautan/transaksi** | Belum ditentukan | Memungkinkan pencocokan dengan gateway dan pencegahan duplikasi. | Konfirmasi format dan keunikan. |
| **Status/progres** | Belum ditentukan | Dapat dipantau apabila fitur didukung. | Konfirmasi daftar status dan mekanisme. |
| **Catatan kegagalan** | Belum ditentukan | Kegagalan ditampilkan dan tidak menghasilkan tautan. | Konfirmasi isi dan penyimpanan log. |

### 6. Rancangan Antarmuka Konseptual

*Mockup berikut menggambarkan kebutuhan interaksi, bukan desain final. Tampilan halaman pembayaran yang dibuka donatur mungkin disediakan oleh gateway.*

#### 6.1 Form Permintaan Tautan

| Elemen | Keterangan |
| :--- | :--- |
| **Identitas** | Identitas Baitulmal Tazkia. |
| **Judul** | Buat Tautan Pembayaran Satu Kali. |
| **Nominal** | Aturan nominal tetap atau bebas perlu dikonfirmasi. |
| **Peruntukan/program** | Ditampilkan apabila diwajibkan oleh aturan bisnis. |
| **Masa berlaku** | Ditentukan berdasarkan aturan yang disepakati. |
| **Aksi** | Tombol “Buat tautan”. |

#### 6.2 Hasil Berhasil

| Elemen | Keterangan |
| :--- | :--- |
| **Status** | Tautan pembayaran siap dibagikan. |
| **Tautan** | Tautan pembayaran yang diterima dari gateway. |
| **Berlaku sampai** | Waktu kedaluwarsa berdasarkan aturan/response gateway. |
| **Aksi** | Bagikan atau salin tautan. |
| **Progres** | Status tautan apabila fitur pemantauan didukung. |

#### 6.3 Hasil Gagal

| Elemen | Keterangan |
| :--- | :--- |
| **Status** | Tautan gagal dibuat. |
| **Pesan** | Informasi kegagalan sesuai hasil gateway dan redaksi yang disetujui. |
| **Aturan tampilan** | Tidak ada tautan pembayaran yang ditampilkan. |

> *Arahan visual awal pada SRS NFR-006 adalah navy blue dan putih, sejauh tampilan berada dalam kendali subsistem ini.*

### 7. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Terkait | Acuan / Catatan |
| :--- | :--- | :--- |
| **Keamanan** | Hanya pihak berwenang dapat membuat tautan. Data donatur/transaksi dilindungi; data pembayaran sensitif tidak disimpan tanpa dasar dan aturan yang disepakati. | NFR-001; SRS Bab 2.3; OQ-013. |
| **Keandalan status** | Tautan tidak valid tidak dikembalikan. Pembayaran tidak dinyatakan berhasil tanpa hasil terverifikasi. | NFR-002; FR-007. |
| **Integrasi** | Pembuatan dan pemantauan tautan mengikuti kontrak gateway. | Field, token, autentikasi, callback/webhook, timeout, dan retry perlu dikonfirmasi. |
| **Keterlacakan** | Referensi tautan/transaksi memungkinkan pencocokan subsistem, gateway, penerimaan donasi, dan rekonsiliasi. | NFR-005; format referensi perlu disepakati. |
| **Kemudahan penggunaan** | Tautan mudah dibagikan; instruksi kepada donatur jelas dan mudah dipahami. | NFR-004; kriteria uji perlu dikonfirmasi. |
| **Kinerja** | Tautan dibuat dalam waktu yang wajar setelah diminta. | Target waktu respons dan volume belum ditetapkan; OQ-014. |

### 8. Kriteria Penerimaan

* [ ] Pihak yang berwenang dapat mengajukan permintaan pembuatan tautan pembayaran satu kali.
* [ ] Sistem membuat atau meminta tautan melalui Payment Gateway Artivisi sesuai integrasi yang disepakati.
* [ ] Jika pembuatan berhasil, sistem mengembalikan tautan yang valid untuk dibagikan.
* [ ] Tautan dapat digunakan sesuai masa berlaku yang ditetapkan.
* [ ] Progres tautan dapat dipantau apabila fitur pemantauan didukung gateway.
* [ ] Jika gateway gagal membuat tautan, sistem menampilkan kegagalan dan tidak mengembalikan tautan yang tidak valid.
* [ ] Pihak yang tidak berwenang tidak dapat membuat tautan.
* [ ] Status pembayaran melalui tautan hanya dinyatakan berhasil berdasarkan hasil yang terverifikasi.
* [ ] Hasil gateway yang diterima lebih dari sekali tidak menyebabkan pencatatan transaksi ganda; mekanismenya mengikuti FR-015.

> *Kriteria yang bergantung pada aturan bisnis atau kemampuan gateway baru dapat diuji secara terukur setelah detail tersebut dikonfirmasi.*

### 9. Hal yang Perlu Dikonfirmasi

1. Siapa yang termasuk “penggalang dana atau staf yang berwenang”, dan bagaimana kewenangannya diverifikasi?
2. Apa aturan tautan: nominal tetap atau bebas, masa berlaku, dan apakah terkait program/peruntukan tertentu?
3. Apa definisi “satu kali”: tautan hanya dapat dipakai sekali atau menghasilkan satu transaksi? Bagaimana perlakuan tautan yang sudah dipakai atau kedaluwarsa?
4. Metode pembayaran apa yang tersedia melalui tautan (transfer, virtual account, e-wallet), dan kapan masing-masing dinyatakan didukung? (SRS Bab 2.4, OQ-002)
5. Apa saja status yang dipantau, bagaimana mekanismenya (callback/webhook atau pengecekan), dan siapa yang dapat melihatnya? (SRS OQ-005)
6. Data donatur apa yang dikumpulkan saat membayar melalui tautan, dan apakah donatur perlu akun?
7. Apakah hasil pembayaran diteruskan ke kelompok 1 (FR-009), tanda terima (FR-008), serta rekonsiliasi dan pelaporan (FR-010) dengan alur yang sama seperti donasi berulang?
8. Bagaimana status pending, timeout, atau hasil gateway yang diterima lebih dari sekali ditangani? (SRS OQ-005, ALT-08, FR-015)
9. Apakah tautan juga dipakai untuk pembayaran manual pada donasi berulang? (SRS FR-006, OQ-001)
10. Apakah permintaan pembuatan tautan yang gagal dapat dicoba ulang, berapa batas percobaannya, dan pesan apa yang ditampilkan?
11. Bagaimana aturan akses, retensi, kepemilikan data, target waktu respons, dan volume transaksi? (SRS OQ-013, OQ-014)

### 10. Ketergantungan dan Relasi dengan FR Lain

| Acuan | Hubungan |
| :--- | :--- |
| **Payment Gateway Artivisi (SRS Bab 2.3)** | Penyedia layanan pembuatan tautan dan pemrosesan pembayaran; kontrak integrasi perlu disepakati. |
| **FR-007** | Acuan verifikasi status transaksi; FR-014 tidak menetapkan sendiri keberhasilan pembayaran. |
| **FR-009** | Acuan pengiriman catatan donasi ke kelompok 1 setelah alur transaksi terpenuhi. |
| **FR-015** | Acuan pencegahan pencatatan ganda untuk hasil gateway yang diterima lebih dari sekali. |
| **FR-008 dan FR-010** | Perlu dikonfirmasi bagaimana transaksi dari tautan terhubung dengan tanda terima, rekonsiliasi, dan pelaporan. |
| **FR-006** | Perlu dikonfirmasi apakah tautan satu kali juga digunakan untuk pembayaran manual pada donasi berulang. |

### 11. Ringkasan

* FR-014 memungkinkan penggalang dana atau staf yang berwenang membuat tautan pembayaran satu kali melalui Payment Gateway Artivisi. Sistem mengembalikan tautan valid untuk dibagikan dan menyediakan pemantauan progres apabila didukung. Jika gateway gagal membuat tautan, sistem menampilkan kegagalan dan tidak mengembalikan tautan yang tidak valid. Status pembayaran tetap harus diverifikasi sesuai FR-007.
* Kebutuhan inti tersedia dalam SRS Draft v0.2, tetapi aturan nominal, masa berlaku, definisi satu kali, status pemantauan, metode pembayaran, dan kontrak teknis gateway belum ditetapkan. Hal-hal tersebut dipertahankan sebagai butir konfirmasi dan tidak diasumsikan sebagai keputusan final.

### 12. Referensi

* FR-014 — Membuat Tautan Pembayaran Satu Kali, Draft Awal v0.1 (5 halaman).
* SRS Draft v0.2, tanggal acuan 26 Oktober 2026: Bab 1.2, Bab 2.1, Bab 2.3, Bab 2.4, Bab 3.2 (ALT-02 dan ALT-08), Bab 4 (FR-014), Bab 6, FR-007, FR-008, FR-009, FR-010, FR-015, NFR-001, NFR-002, NFR-004, NFR-005, NFR-006, OQ-002, OQ-005, OQ-013, dan OQ-014.