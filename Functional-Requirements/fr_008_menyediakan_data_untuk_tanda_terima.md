# FUNCTIONAL REQUIREMENT (FR)

## FR-008 — MENYEDIAKAN DATA UNTUK TANDA TERIMA

**Sistem Donasi Berulang dan Kanal Pembayaran Digital**  
* **Organisasi:** Baitulmal Tazkia
* **Versi dokumen:** Draft untuk Presentasi

| Informasi | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-008 |
| **Nama Kebutuhan** | Menyediakan Data untuk Tanda Terima |
| **Aktor Utama** | Sistem; modul tanda terima sebagai penerima data |
| **Tujuan** | Menyiapkan dan menyediakan data transaksi yang telah terverifikasi berhasil kepada modul tanda terima melalui mekanisme yang disepakati, serta mencatat hasil pertukaran datanya. |
| **Prioritas** | Belum ditentukan |
| **Acuan** | SRS Draft v0.2; tanggal acuan pada sumber: 26 Oktober 2026 |
| **Status sumber** | Perlu klarifikasi untuk pemilik modul, field, pemicu pengiriman, batas modul, dan kontrak integrasi. |

### 1. Deskripsi Functional Requirement

Apabila transaksi telah terverifikasi berhasil, sistem menyiapkan data transaksi yang diperlukan untuk tanda terima, mengirimkannya melalui mekanisme yang disepakati, dan mencatat hasil pertukaran jika tersedia. Data tanda terima hanya dikirim untuk transaksi dengan status sukses terverifikasi. Apabila pengiriman gagal, kegagalan dicatat dan status pembayaran tetap terpisah; mekanisme pengiriman ulang ditetapkan kemudian.

* **Pemicu:** Transaksi telah terverifikasi berhasil.
* **Kondisi awal:** Data transaksi wajib tersedia dan modul tanda terima/API telah ditentukan.

### 2. Format Outline dan Batasan

* Penerimaan pemicu berupa transaksi yang telah terverifikasi berhasil.
* Penyiapan data transaksi yang diperlukan untuk tanda terima.
* Pengiriman data kepada modul tanda terima melalui mekanisme yang disepakati.
* Pencatatan hasil pertukaran data jika tersedia.
* Penanganan kegagalan pengiriman tanpa mengubah status pembayaran.

> **Batasan:** FR-008 hanya menyediakan data untuk tanda terima. Verifikasi dan pembaruan status transaksi berada pada FR-007. Pengiriman data untuk kebutuhan lain serta rekonsiliasi/pelaporan berada pada FR terkait. Pembuatan dan pengiriman tanda terima kepada donatur belum dapat dipastikan sebagai bagian subsistem ini dan tidak ditetapkan oleh FR-008. FR-008 tidak membahas pemrosesan pembayaran melalui gateway (FR-006), pengingat (FR-005), atau notifikasi (FR-013).

### 3. Proses Bisnis

**Aktor:** Sistem dan modul tanda terima sebagai penerima data. Status transaksi telah ditetapkan pada FR-007.

| Tahap | Aktivitas | Dasar / Catatan |
| :--- | :--- | :--- |
| 1 | Sistem mengenali transaksi yang telah terverifikasi berhasil sebagai pemicu pengiriman. | Tertulis di SRS. Cara dan waktu pemicu (otomatis atau atas permintaan) perlu konfirmasi. |
| 2 | Sistem memastikan data transaksi wajib tersedia dan modul tanda terima/API telah ditentukan. | Disimpulkan dari kondisi awal SRS. Pemilik modul dan daftar data wajib perlu konfirmasi. |
| 3 | Sistem menyiapkan data transaksi yang diperlukan. | Tertulis di SRS. Data yang disebut: referensi donasi, nominal, waktu, dan informasi tanda terima yang disetujui. Field rinci perlu konfirmasi. |
| 4 | Sistem mengirim data melalui mekanisme yang disepakati. | Tertulis di SRS. Bentuk mekanisme, API, dan autentikasi perlu konfirmasi. |
| 5 | Sistem mencatat hasil pertukaran jika tersedia. | Tertulis di SRS. Bentuk pencatatan perlu konfirmasi. |

**Alur alternatif:**
* **Pengiriman data gagal:** Sistem mencatat kegagalan; status pembayaran tetap terpisah dan tidak berubah karena pengiriman gagal. Mekanisme pengiriman ulang dan pencegahan pengiriman ganda perlu konfirmasi.
* **Transaksi belum terverifikasi berhasil (pending, gagal, atau tidak dikenal):** Sistem tidak mengirim data tanda terima sebagai transaksi sukses. Perlakuan jika status berubah menjadi berhasil setelah sempat pending perlu konfirmasi.

### 4. Field, Tipe Data, dan Validasi

*SRS Draft v0.2 menyebut unsur data yang mungkin dikirim, tetapi belum menetapkan field wajib, tipe data, atau aturan validasi. Nama field berikut merupakan usulan pembahasan, bukan nama kolom basis data dan bukan keputusan final.*

| Field Usulan | Tipe Data | Validasi / Aturan Awal | Status |
| :--- | :--- | :--- | :--- |
| **Status transaksi terverifikasi** | Belum ditentukan | Hanya transaksi berstatus sukses terverifikasi yang dikirim. | Perlu konfirmasi daftar status dan pemetaan dari FR-007. |
| **Referensi donasi/transaksi** | Belum ditentukan | Dapat dicocokkan dengan transaksi sumber. | Perlu konfirmasi format referensi. |
| **Nominal** | Belum ditentukan | Sesuai nominal pada transaksi terverifikasi. | Perlu konfirmasi field wajib dan format. |
| **Waktu transaksi** | Belum ditentukan | Sesuai waktu transaksi terverifikasi. | Perlu konfirmasi format dan zona waktu. |
| **Informasi tanda terima yang disetujui** | Belum ditentukan | Hanya memuat informasi yang disetujui. | Perlu konfirmasi apakah mencakup identitas donatur dan peruntukan. |
| **Hasil pertukaran data** | Belum ditentukan | Dicatat jika tersedia. | Perlu konfirmasi bentuk dan nilai status. |
| **Catatan kegagalan pengiriman** | Belum ditentukan | Kegagalan dicatat dan dapat ditelusuri, terpisah dari status pembayaran. | Perlu konfirmasi isi dan bentuk catatan. |

### 5. Mockup Pertukaran Data dan Catatan Pengiriman

*FR-008 berupa pertukaran data antarmodul sehingga mockup berikut menggambarkan struktur data konseptual dan catatan hasil, bukan layar untuk donatur. Data hanya disiapkan untuk transaksi yang telah berstatus sukses terverifikasi.*

```text
+-----------------------+     +-------------------------+     +-----------------------+     +-----------------------+
| Pemicu dari FR-007    |     | Subsistem Donasi        |     | Mekanisme integrasi   |     | Modul tanda terima    |
|                       |     | Berulang                |     |                       |     |                       |
| Status transaksi:     | --> | Menyiapkan data:        | --> | Pengiriman melalui    | --> | Penerima data         |
| SUKSES TERVERIFIKASI  |     | - Referensi transaksi   |     | mekanisme/API yang    |     |                       |
|                       |     | - Nominal               |     | disepakati            |     | Pemilik modul:        |
| Jika belum terverif.: |     | - Waktu transaksi       |     |                       |     | perlu konfirmasi      |
| data tidak dikirim    |     | - Info tanda terima     |     | Kontrak & autentikasi:|     |                       |
|                       |     |   yang telah disetujui  |     | perlu konfirmasi      |     |                       |
+-----------------------+     +-------------------------+     +-----------------------+     +-----------------------+
                                                                                                        |
                                                                                                [hasil pertukaran]
                                                                                                        v
                              +-----------------------------------+     +-----------------------------------+
                              | Catatan hasil pertukaran          |     | Jika pengiriman gagal             |
                              |                                   |     |                                   |
                              | Referensi transaksi               | --> | Catat kegagalan untuk ditelusuri. |
                              | Hasil pengiriman: berhasil/gagal  | [jika| Status pembayaran tetap terpisah  |
                              | Keterangan kegagalan (jika ada)   |gagal| (tidak berubah krn gagal kirim).  |
                              |                                   |     | Aturan pengiriman ulang:          |
                              | Nilai dan format: perlu konfirmasi|     | perlu konfirmasi.                 |
                              +-----------------------------------+     +-----------------------------------+
```
*Sketsa konseptual; field, pemilik modul, pemicu, API, autentikasi, dan retry belum ditetapkan.*

> Contoh unsur data pada *payload*: status sukses terverifikasi, referensi donasi/transaksi, nominal, waktu transaksi, serta informasi tanda terima lain yang telah disetujui. Catatan pengiriman dapat memuat referensi transaksi, hasil pengiriman, dan keterangan kegagalan jika ada. Field dan format sebenarnya perlu dikonfirmasi.

### 6. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Awal | Catatan |
| :--- | :--- | :--- |
| **Keamanan** | Data donatur dan transaksi dilindungi sesuai kebijakan yang disepakati. Data kartu atau nomor rekening mentah tidak ditetapkan untuk disimpan/dikirim tanpa dasar dan desain keamanan yang disepakati. | NFR-001; kebijakan akses dan retensi perlu klarifikasi. |
| **Keandalan status** | Data tanda terima tidak dikirim untuk transaksi yang belum terverifikasi berhasil. Kegagalan pengiriman tidak mengubah status pembayaran. | Selaras dengan NFR-002 dan ALT-06. |
| **Integrasi** | Pertukaran data menggunakan kontrak API yang disepakati dan tidak mengakses basis data modul lain secara langsung. | NFR-003; kontrak dan pemilik modul belum final. |
| **Keterlacakan** | Referensi data memungkinkan pencocokan dengan transaksi sumber; kegagalan pengiriman dapat ditelusuri. | NFR-005; format referensi perlu disepakati. |
| **Pemulihan kegagalan integrasi** | Kegagalan pertukaran data dapat ditelusuri dan tidak menyebabkan transaksi dianggap berhasil atau tercatat ganda. | NFR-007; logging, monitoring, retry, dan target pemulihan perlu klarifikasi. |
| **Kinerja** | Data disediakan dalam waktu yang wajar setelah transaksi terverifikasi. | Target waktu respons belum ditetapkan (OQ-014). |

### 7. Kriteria Penerimaan Awal

* [ ] Data tanda terima hanya dikirim untuk transaksi dengan status sukses terverifikasi.
* [ ] Sistem menyiapkan data transaksi yang diperlukan dan mengirimkannya melalui mekanisme yang disepakati.
* [ ] Sistem mencatat hasil pertukaran data jika tersedia.
* [ ] Jika pengiriman gagal, kegagalan dicatat dan dapat ditelusuri, sedangkan status pembayaran tetap terpisah dan tidak berubah.

> *Kriteria penerimaan bersifat awal dan perlu diperbarui setelah aturan bisnis, field, serta kontrak integrasi dikonfirmasi.*

### 8. Hal yang Perlu Dikonfirmasi

1. Apakah tanda terima dikelola oleh modul atau pihak terpisah, dan siapa pemilik modulnya?
2. Apakah pembuatan dan pengiriman tanda terima kepada donatur menjadi bagian subsistem ini, atau subsistem ini hanya menyediakan data?
3. Apa field wajib data tanda terima, dan apakah mencakup identitas donatur, peruntukan, serta metode pembayaran?
4. Apa pemicu pengiriman: otomatis setiap transaksi berhasil atau atas permintaan modul tanda terima?
5. Apa mekanisme pertukaran data (endpoint API, payload, autentikasi, kode respons), dan siapa yang menyepakati kontraknya?
6. Apakah pengiriman data gagal dicoba ulang, berapa jeda dan batasnya, serta bagaimana mencegah pengiriman ganda?
7. Siapa yang menelusuri dan menangani kegagalan pengiriman, serta bagaimana hasil pertukaran data dicatat?
8. Bagaimana penanganan transaksi yang awalnya *pending* lalu berhasil, atau transaksi yang dikoreksi setelah data dikirim?
9. Apakah penyediaan data untuk tanda terima, kebutuhan integrasi lain, dan rekonsiliasi dikirim dalam satu kejadian atau terpisah; apakah urutannya berpengaruh?
10. Apa aturan akses, retensi, dan kepemilikan data tanda terima?
11. Berapa target waktu penyediaan data setelah transaksi terverifikasi?

### 9. Catatan untuk Presentasi

* FR-008 menjelaskan penyediaan data transaksi terverifikasi untuk tanda terima. Fungsi ini berada setelah verifikasi status transaksi (FR-007): hanya transaksi yang telah terverifikasi berhasil yang datanya disiapkan dan dikirim kepada modul tanda terima, lalu hasil pertukarannya dicatat. FR ini tidak membahas pemrosesan pembayaran melalui gateway, pengingat/notifikasi, maupun penyediaan data rekonsiliasi dan pelaporan.
* Jika ditanya mengapa FR-008 masih perlu klarifikasi: SRS Draft v0.2 menyatakan pemilik modul tanda terima, field, pemicu pengiriman, dan API belum jelas. Pembuatan serta pengiriman tanda terima kepada donatur juga belum dapat dipastikan sebagai bagian ruang lingkup subsistem.
* Jika ditanya mengapa data hanya dikirim untuk transaksi terverifikasi: SRS mensyaratkan bahwa data tanda terima tidak dikirim sebagai transaksi sukses sebelum status pembayaran terverifikasi. Jika pengiriman data gagal, status pembayaran tidak berubah karena pembayaran dan pertukaran data merupakan dua proses berbeda.

### 10. Status Dokumen

**Draft untuk Presentasi – Menunggu Validasi dan Persetujuan.** Dokumen ini merapikan isi FR-008 berdasarkan sumber yang diberikan. Field, tipe data, pemilik modul, pemicu, *endpoint/payload* API, autentikasi, *retry*, serta cakupan pembuatan dan pengiriman tanda terima belum boleh dianggap keputusan final sebelum disepakati dengan PIC terkait.