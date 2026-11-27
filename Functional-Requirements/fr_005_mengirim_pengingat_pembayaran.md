# FUNCTIONAL REQUIREMENT

## FR-005 — Mengirim Pengingat Pembayaran

**Sistem Donasi Berulang dan Kanal Pembayaran Digital | Baitulmal Tazkia**

### A. Identitas Kebutuhan

| Elemen | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-005 |
| **Nama Kebutuhan** | Mengirim Pengingat Pembayaran |
| **Aktor Utama** | Sistem; donatur sebagai penerima pengingat. |
| **Tujuan** | Mengirim pengingat kepada donatur sesuai jadwal dan kanal yang disepakati untuk pembayaran donasi berulang secara manual, serta mencatat hasil pengirimannya. |
| **Prioritas** | Belum ditentukan. |
| **Status** | Draft untuk presentasi; belum menjadi persyaratan final klien. Hubungan pengingat dengan penagihan otomatis (autodebit), waktu, frekuensi, dan kanal masih perlu klarifikasi. |
| **Acuan** | FR-005 versi 0.1 Draft Awal dan SRS Draft v0.2 (tanggal acuan 26 Oktober 2026). |

### B. Deskripsi Functional Requirement

Apabila jadwal pengingat tercapai berdasarkan aturan yang disepakati, sistem menentukan jadwal pengingat, mengirim pesan kepada donatur melalui kanal yang disepakati, dan mencatat hasil pengiriman jika kanal mendukung. Apabila pengiriman gagal, sistem mencatat kegagalan tersebut sehingga dapat ditelusuri. Jumlah percobaan ulang dan eskalasi belum ditetapkan dan perlu dikonfirmasi.

* **Pemicu:** Jadwal pengingat tercapai berdasarkan aturan yang disepakati.
* **Kondisi awal:** Pengingat untuk pembayaran manual diputuskan masuk ruang lingkup dan kontak/kanal tersedia.

### C. Ruang Lingkup dan Batasan

**Termasuk dalam FR-005:**
* Menentukan jadwal pengingat pembayaran berdasarkan aturan yang disepakati.
* Mengirim pesan pengingat kepada donatur melalui kanal yang disepakati.
* Mencatat hasil pengiriman pengingat jika kanal mendukung.
* Mencatat kegagalan pengiriman agar dapat ditelusuri.
* Mencatat bahwa pembayaran belum terkonfirmasi apabila donatur belum membayar setelah pengingat.

**Tidak termasuk dalam FR-005:**
* Pemrosesan pembayaran atau penagihan melalui gateway (FR-006).
* Verifikasi status transaksi (FR-007).
* Notifikasi sebelum/sesudah penagihan (FR-013).
* Penyimpanan kesediaan donasi dan jadwal (FR-004).
* Jeda dan pembatalan donasi berulang.
* Isi atau penjadwalan komunikasi berkala yang menurut SRS Bab 6 berada pada Kelompok 11.

> **Batas penting:** FR-005 hanya membahas pengingat untuk pembayaran manual. Pengiriman pengingat tidak membuktikan pembayaran berhasil dan tidak dengan sendirinya mengubah status pembayaran.

### D. Proses Bisnis

*Kesediaan donasi dan jadwal telah tersimpan pada FR-004. Label dasar informasi dipertahankan agar jelas mana yang tertulis pada SRS dan mana yang masih perlu dikonfirmasi.*

| No. | Aktor | Aktivitas | Dasar / Catatan |
| :--- | :--- | :--- | :--- |
| 1 | Sistem | Menentukan jadwal pengingat berdasarkan aturan yang disepakati. | Tertulis di SRS; tanggal, frekuensi, dan dasar perhitungan perlu konfirmasi. |
| 2 | Sistem | Memastikan pengingat pembayaran manual masuk ruang lingkup dan kontak/kanal donatur tersedia. | Disimpulkan dari kondisi awal SRS; sumber kontak dan izin penggunaan perlu konfirmasi. |
| 3 | Sistem | Mengirim pesan pengingat melalui kanal yang disepakati. | Tertulis di SRS; kanal, isi pesan, dan pengelola naskah perlu konfirmasi. |
| 4 | Sistem | Mencatat hasil pengiriman jika kanal mendukung. | Tertulis di SRS; bentuk pencatatan perlu konfirmasi. |

**Alur alternatif — pengiriman pengingat gagal:**
* Sistem mencatat kegagalan pengiriman agar dapat ditelusuri.
* Jumlah percobaan ulang, jeda antarpercobaan, dan eskalasi belum ditentukan.
* Penanganan apabila kanal tidak mendukung pencatatan hasil pengiriman perlu dikonfirmasi.

**Alur alternatif — donatur belum membayar setelah pengingat:**
* Sistem mencatat bahwa pembayaran belum terkonfirmasi.
* Sistem tidak menyatakan pembayaran berhasil hanya karena pengingat telah dikirim.
* Aturan pengingat lanjutan, masa tunggu, dan dampaknya pada status donasi mengikuti keputusan bisnis yang belum dikonfirmasi.

### E. Field, Tipe Data, dan Validasi

*SRS Draft v0.2 belum menetapkan field, tipe data, maupun aturan validasi rinci untuk FR-005. Field berikut merupakan usulan untuk pembahasan, bukan nama kolom basis data atau keputusan final.*

| Field Usulan | Tujuan / Isi | Tipe Data | Validasi / Aturan |
| :--- | :--- | :--- | :--- |
| **Jadwal pengingat** | Tanggal/waktu atau aturan jadwal pengiriman. | Belum ditentukan. | Pengingat dikirim sesuai jadwal yang disetujui; tanggal dan frekuensi perlu konfirmasi (OQ-003). |
| **Kanal pengiriman** | Media untuk mengirim pesan pengingat. | Belum ditentukan. | Hanya menggunakan kanal yang disetujui; kanal perlu konfirmasi (OQ-003). |
| **Kontak donatur tujuan** | Alamat/nomor tujuan pengiriman. | Belum ditentukan. | Kontak dan kanal harus tersedia sebelum pengingat dikirim; sumber data dan izin perlu konfirmasi. |
| **Isi pesan pengingat** | Naskah pesan yang dikirim kepada donatur. | Teks (usulan). | Isi, tautan/cara pembayaran, dan pengelola naskah perlu konfirmasi (OQ-008). |
| **Hasil pengiriman** | Hasil proses pengiriman pesan. | Belum ditentukan. | Dicatat jika kanal mendukung; bentuk dan nilai status perlu konfirmasi. |
| **Catatan kegagalan pengiriman** | Informasi untuk menelusuri kegagalan. | Belum ditentukan. | Kegagalan harus dapat ditelusuri; isi dan bentuk catatan perlu konfirmasi. |
| **Percobaan ulang dan eskalasi** | Informasi percobaan ulang jika pengiriman gagal. | Belum ditentukan. | Jumlah, jeda, batas percobaan, dan eskalasi belum ditentukan. |

### F. UI Mockup

*FR-005 terutama berupa proses pengiriman pesan. Tampilan berikut adalah wireframe konseptual untuk bahan presentasi, bukan desain final. Kanal, redaksi pesan, dan tampilan pencatatan hasil harus dikonfirmasi. Arah visual awal: navy blue dan putih (SRS NFR-006), sejauh kanal mendukung.*

**Contoh susunan pesan yang diterima donatur:**
```text
+-----------------------------------------------------------------------+
| BAITULMAL TAZKIA — Pengingat Donasi Berulang                          |
+-----------------------------------------------------------------------+
| Identitas        : Baitulmal Tazkia                                   |
| Sapaan / pesan   : [Sapaan dan kalimat pengingat — teks perlu         |
|                    dikonfirmasi]                                      |
| Nominal          : [Nominal donasi]                                   |
| Periode / jadwal : [Jadwal donasi]                                    |
| Peruntukan       : [Peruntukan donasi]                                |
| Batas waktu      : [Batas waktu pembayaran — perlu dikonfirmasi]      |
| Cara membayar    : [Cara atau tautan pembayaran — jika disepakati]    |
+-----------------------------------------------------------------------+
```
*Catatan: contoh ini menggambarkan isi pesan, bukan tampilan aplikasi tertentu. Kanal (misalnya email, SMS, atau WhatsApp) belum diputuskan pada SRS.*

**Contoh tampilan internal untuk penelusuran hasil pengiriman:**
```text
+-----------------------------------------------------------------------+
| BAITULMAL TAZKIA — Catatan Pengiriman Pengingat                       |
+-----------------------------------------------------------------------+
| Referensi pendaftaran : [ID / referensi]                              |
| Jadwal pengingat      : [Tanggal / jadwal]                            |
| Kanal                 : [Kanal pengiriman]                            |
| Hasil pengiriman      : [Terkirim / gagal — nilai status perlu        |
|                         dikonfirmasi]                                 |
| Catatan kegagalan     : [Rincian kegagalan jika terjadi]              |
+-----------------------------------------------------------------------+
```
*Catatan: pengguna yang dapat melihat catatan, bentuk pencatatan, dan nilai status masih perlu dikonfirmasi.*

### G. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Awal | Catatan |
| :--- | :--- | :--- |
| **Keamanan** | FR-005 tidak memproses atau menyimpan data pembayaran; perlindungan data donatur dan kontak mengikuti NFR-001 SRS. | Kebijakan, akses, dan retensi perlu klarifikasi (OQ-013). |
| **Keandalan status** | Pengiriman pengingat dan kegagalannya tidak mengubah status pembayaran. Pembayaran tidak dinyatakan berhasil tanpa hasil terverifikasi. | Selaras dengan NFR-002 SRS dan ALT-03. |
| **Keterlacakan** | Hasil pengiriman dan kegagalan pengiriman dapat ditelusuri. | Format referensi mengacu pada NFR-005 dan perlu disepakati. |
| **Kinerja** | Pengingat dikirim sesuai jadwal yang disepakati. | Target ketepatan waktu belum ditetapkan (OQ-014). |
| **Kemudahan penggunaan** | Isi pengingat jelas dan mudah dipahami donatur. | Mengacu pada NFR-004; kriteria uji perlu klarifikasi. |

### H. Kriteria Penerimaan Awal

* [ ] Sistem menentukan jadwal pengingat berdasarkan aturan yang disepakati.
* [ ] Pengingat hanya dikirim sesuai jadwal dan kanal yang disetujui.
* [ ] Sistem mencatat hasil pengiriman jika kanal mendukung.
* [ ] Jika pengiriman gagal, sistem mencatat kegagalan dan kegagalan dapat ditelusuri.
* [ ] Pengiriman pengingat maupun kegagalannya tidak mengubah status pembayaran.
* [ ] Jika donatur belum membayar setelah pengingat, pembayaran dicatat sebagai belum terkonfirmasi dan tidak dianggap berhasil hanya karena pesan telah dikirim.

> *Kriteria penerimaan masih bersifat awal dan harus diperbarui setelah aturan bisnis dikonfirmasi.*

### I. Hal yang Perlu Dikonfirmasi

| No. | Pertanyaan / Keputusan | Status |
| :--- | :--- | :--- |
| 1 | Apakah pengingat pembayaran manual masuk ruang lingkup versi ini? Apakah pengingat menggantikan autodebit, berjalan bersama autodebit, atau hanya untuk metode tertentu? (OQ-001) | Belum dikonfirmasi |
| 2 | Kapan tanggal pengingat ditetapkan, berapa frekuensinya, dan kanal apa yang digunakan? (OQ-003) | Belum dikonfirmasi |
| 3 | Dari mana kontak donatur diperoleh, dan izin apa yang harus dipenuhi sebelum pengingat dikirim? | Belum dikonfirmasi |
| 4 | Siapa yang mengelola isi pesan dan penjadwalan: subsistem ini atau Kelompok 11 (Hubungan Donatur dan Komunikasi)? (OQ-008) | Belum dikonfirmasi |
| 5 | Apa isi pesan pengingat, dan apakah pesan memuat tautan atau cara pembayaran? | Belum dikonfirmasi |
| 6 | Bagaimana hasil pengiriman dicatat, dan bagaimana jika kanal tidak mendukung pencatatan hasil? | Belum dikonfirmasi |
| 7 | Apakah pengiriman gagal dicoba ulang? Berapa jeda dan batas percobaannya, serta bagaimana eskalasinya? | Belum dikonfirmasi |
| 8 | Jika donatur tidak membayar setelah pengingat, berapa masa tunggu, apakah ada pengingat lanjutan, dan apa dampaknya pada status donasi? | Belum dikonfirmasi |
| 9 | Apa hubungan FR-005 dengan FR-013 (notifikasi sebelum/sesudah penagihan): satu fungsi atau dua fungsi terpisah? | Belum dikonfirmasi |
| 10 | Apakah pengingat dihentikan ketika donatur menjeda atau membatalkan donasi (FR-011 dan FR-012), dan sejak kapan? (OQ-012) | Belum dikonfirmasi |

### J. Catatan untuk Presentasi

* FR-005 menjelaskan pengiriman pengingat pembayaran kepada donatur setelah kesediaan donasi dan jadwal tersimpan pada FR-004.
* Ketika jadwal pengingat tercapai, sistem mengirim pesan melalui kanal yang disepakati dan mencatat hasil pengiriman jika kanal mendukung.
* FR-005 hanya membahas pengingat pembayaran manual; pemrosesan pembayaran/gateway dan verifikasi transaksi berada pada FR lain.
* Pengiriman pengingat bukan bukti pembayaran berhasil. Status pembayaran harus menunggu hasil terverifikasi.
* Hubungan pengingat manual dengan autodebit, waktu, frekuensi, kanal, isi pesan, dan percobaan ulang masih perlu keputusan.
* Dokumen ini dirapikan untuk bahan presentasi; belum menjadi baseline kebutuhan dan belum disetujui klien.

*— Akhir Dokumen FR-005 —*