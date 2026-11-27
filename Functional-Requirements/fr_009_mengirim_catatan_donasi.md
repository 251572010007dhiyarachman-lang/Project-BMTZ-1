# FUNCTIONAL REQUIREMENT

## FR-009 — Mengirim Catatan Donasi

**Sistem Donasi Berulang dan Kanal Pembayaran Digital — Baitulmal Tazkia**

| Identitas | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-009 |
| **Nama Kebutuhan** | Mengirim Catatan Donasi |
| **Aktor Utama** | Sistem pengirim; modul/kelompok penerima catatan donasi (pemilik tujuan perlu dikonfirmasi) |
| **Tujuan** | Menyusun dan mengirim catatan donasi dari transaksi yang memenuhi syarat pencatatan, mencatat respons penerimaan, serta menyediakan jejak pemulihan jika integrasi gagal. |
| **Prioritas** | Belum ditentukan |
| **Acuan** | SRS Draft v0.2; dokumen FR-009 versi 0.1 |

> **Catatan Validasi Penting:**  
> Dokumen sumber menyebut “Kelompok 1” sebagai penerima API. Namun, penetapan kelompok tujuan tersebut belum dapat dipastikan dan tidak boleh dianggap sebagai keputusan final. Karena itu, nama kelompok tidak dipertahankan sebagai fakta pada judul/aktor; pemilik modul penerima, nama kelompok, serta kontrak integrasi wajib dikonfirmasi sebelum baseline SRS disetujui.  
> *Perbedaan sumber:* judul dan isi file sumber mencantumkan Kelompok 1, sedangkan pemetaan integrasi proyek yang tersedia belum mendukung penetapan tersebut. Jangan mengganti otomatis menjadi kelompok lain tanpa persetujuan pemilik proyek.

### 1. Deskripsi dan Ruang Lingkup

Apabila hasil penagihan/pembayaran telah memenuhi syarat pencatatan donasi, sistem menyusun catatan donasi berdasarkan skema data yang disepakati, mengirimkannya melalui API ke modul penerima, lalu mencatat respons dari modul tersebut. Jika pengiriman gagal, sistem mencatat kegagalan dan menyimpan referensi yang diperlukan untuk penelusuran serta pemulihan. Pengiriman ulang harus mencegah terbentuknya catatan donasi ganda.

* **Pemicu:** Hasil penagihan/pembayaran memenuhi syarat pencatatan donasi. Berdasarkan SRS, transaksi yang belum terverifikasi berhasil tidak boleh dikirim sebagai catatan donasi.

**Batasan ruang lingkup:**
* FR-009 mencakup penyusunan *payload*, pengiriman melalui API, pencatatan respons, dan dukungan pemulihan integrasi.
* Pencatatan penerimaan donasi dan pengelolaan akun donatur dilakukan oleh modul penerima dan berada di luar tanggung jawab FR-009.
* Verifikasi status transaksi mengacu pada FR-007; penyediaan data tanda terima pada FR-008; data rekonsiliasi/pelaporan pada FR-010; pencegahan pencatatan ganda secara umum pada FR-015.
* Pemrosesan pembayaran melalui gateway berada pada FR-006 dan bukan bagian dari FR-009.

### 2. Proses Bisnis

*Label: `[Tertulis di SRS]` berarti disebutkan pada SRS Draft v0.2; `[Disimpulkan dari SRS]` berarti diturunkan dari pemicu/kondisi atau bagian SRS lain; `[Perlu Konfirmasi]` berarti belum ada keputusan rinci.*

| No. | Langkah Proses | Dasar / Status |
| :--- | :--- | :--- |
| 1 | Sistem menerima/mengenali hasil pembayaran yang memenuhi syarat pencatatan donasi. | Tertulis di SRS; kriteria rinci dan waktu pemicu perlu konfirmasi. |
| 2 | Sistem memastikan skema/kontrak API atau data contoh tersedia sebelum membentuk payload. | Disimpulkan dari kondisi awal SRS; format data contoh dan penanggung jawabnya perlu konfirmasi. |
| 3 | Sistem menyusun catatan donasi sesuai skema yang disepakati. | Tertulis di SRS; field wajib dan format setiap field perlu konfirmasi. |
| 4 | Sistem mengirim catatan donasi melalui API ke modul penerima yang telah ditetapkan. | Tertulis di SRS; endpoint, autentikasi, metode, dan timeout perlu konfirmasi. |
| 5 | Sistem menerima dan mencatat respons penerimaan dari modul tujuan. | Tertulis di SRS; struktur respons dan pemetaan sukses/gagal perlu konfirmasi. |
| 6 | Jika pengiriman gagal, sistem mencatat kegagalan dan menyimpan referensi untuk pemulihan. | Tertulis di SRS; aturan retry, jadwal, batas percobaan, dan penanggung jawab perlu konfirmasi. |
| 7 | Jika pengiriman ulang dilakukan, sistem memastikan tidak terbentuk catatan donasi ganda. | Tertulis di SRS/FR-015; mekanisme idempotensi dan kunci unik perlu konfirmasi. |

**Alur Alternatif dan Pengecualian:**
* **API tidak tersedia atau mengembalikan kegagalan:** Catat hasil gagal, simpan referensi transaksi/pengiriman, dan jangan menghapus catatan sumber. Pemulihan mengikuti kebijakan *retry* yang kelak disepakati.
* **Referensi transaksi terdeteksi pernah dikirim:** Jangan membuat catatan donasi kedua; catat kejadian duplikasi untuk audit/penelusuran. Detail mekanisme deduplikasi mengikuti FR-015 dan kontrak integrasi.
* **Transaksi belum terverifikasi berhasil:** Jangan kirim catatan donasi. Tunggu status yang sah dari proses FR-007.
* **Catatan yang sudah diterima perlu dikoreksi:** Mekanisme koreksi, pembatalan, atau *reversal* belum ditentukan dan harus dikonfirmasi sebelum implementasi.

### 3. Field, Tipe Data, dan Validasi

*Daftar berikut merupakan rancangan awal berdasarkan elemen data yang disebutkan SRS. Nama field, tipe data, format, mandatory/optional, dan aturan validasi belum merupakan kontrak final.*

| Field Usulan | Tipe Data | Validasi Awal | Status |
| :--- | :--- | :--- | :--- |
| **Referensi donasi/transaksi** | Belum ditentukan | Harus dapat dicocokkan antar-subsistem; kandidat kunci unik/idempotensi | Perlu konfirmasi format dan uniqueness (OQ-006/NFR-005/FR-015) |
| **Nominal** | Belum ditentukan | Harus sama dengan nominal transaksi yang terverifikasi | Perlu konfirmasi tipe, mata uang, presisi, dan kewajiban field |
| **Waktu transaksi** | Belum ditentukan | Mengacu pada waktu transaksi yang sah | Perlu konfirmasi format, zona waktu, dan sumber timestamp |
| **Identitas donatur** | Belum ditentukan | Hanya data yang disepakati dalam kontrak; minimisasi data pribadi | Perlu konfirmasi field yang boleh dikirim |
| **Peruntukan** | Belum ditentukan | Mengacu pada pilihan peruntukan pada donasi | Perlu konfirmasi kode/daftar nilai dan mandatory |
| **Status** | Belum ditentukan | Konsisten dengan hasil verifikasi FR-007 | Perlu konfirmasi enum/status yang diterima |
| **Respons penerima** | Belum ditentukan | Dicatat untuk setiap upaya pengiriman | Perlu konfirmasi kode, pesan, dan struktur respons |
| **Catatan kegagalan/referensi pemulihan** | Belum ditentukan | Menyimpan konteks yang cukup untuk penelusuran | Perlu konfirmasi format log, retensi, dan akses |

### 4. Mockup Integrasi / UI

*FR-009 merupakan pertukaran data antarsubsistem, bukan layar donatur. Mockup berikut menggambarkan alur integrasi dan pencatatan hasil. Nama kelompok/pemilik modul penerima masih perlu dikonfirmasi.*

```text
                MOCKUP ALUR INTEGRASI FR-009
   Nama kelompok / pemilik modul penerima API: PERLU KONFIRMASI

+-------------------+        +-------------------+        +-------------------+        +-------------------+
|      FR-007       |        |      FR-009       |        |   API Integrasi   |        |  Modul Penerima   |
|                   | pemicu |                   |payload |                   |  API   |                   |
| Status pembayaran | -----> | Susun catatan     | -----> | Kirim payload dan | -----> | Penerimaan /      |
| terverifikasi     |        | donasi sesuai     |        | terima respons    |        | pencatatan oleh   |
| berhasil          |        | skema disepakati  |        |                   |        | pemilik tujuan    |
+-------------------+        +-------------------+        +-------------------+        +-------------------+
                                                                    |
                                                             [respons gagal]
                                                                    v
                             +-------------------+        +-------------------+
                             |    Jika gagal     |        | Pengiriman ulang  |
                             |                   |pemulih-|                   |
                             | Catat kegagalan   |  an    | Ikuti aturan      |
                             | & simpan ref.     | -----> | retry & idempoten |
                             | pemulihan         |        | yang disepakati   |
                             +-------------------+        +-------------------+
```

**Contoh struktur payload (ilustratif, bukan kontrak API):**

| Elemen | Nilai Contoh Konseptual |
| :--- | :--- |
| **Referensi donasi/transaksi** | `[referensi unik – format perlu disepakati]` |
| **Nominal** | `[nominal terverifikasi]` |
| **Waktu transaksi** | `[timestamp dan zona waktu perlu disepakati]` |
| **Identitas donatur** | `[data minimum sesuai persetujuan/kontrak]` |
| **Peruntukan** | `[kode peruntukan sesuai kesepakatan]` |
| **Status** | `[status terverifikasi yang diterima modul tujuan]` |

> *Catatan: Contoh ini hanya menunjukkan kelompok informasi yang mungkin dipertukarkan. Jangan menganggapnya sebagai JSON final, nama kolom database, atau spesifikasi endpoint.*

### 5. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Awal | Catatan |
| :--- | :--- | :--- |
| **Keamanan dan privasi** | Data donatur/transaksi dilindungi; hanya data yang disepakati yang dikirim. Data kartu atau nomor rekening mentah tidak ditetapkan untuk dikirim/disimpan oleh FR ini. | Kebijakan akses, enkripsi, retensi, dan dasar pemrosesan data perlu konfirmasi (NFR-001/OQ-013). |
| **Keandalan status** | Hanya transaksi yang terverifikasi berhasil yang menjadi pemicu pencatatan donasi. Kegagalan integrasi tidak boleh mengubah transaksi menjadi berhasil. | Selaras NFR-002 dan FR-007. |
| **Integrasi** | Komunikasi melalui kontrak API yang disepakati; tidak mengakses database modul lain secara langsung. | Endpoint, autentikasi, versi API, dan format pesan belum final (NFR-003). |
| **Keterlacakan** | Referensi memungkinkan pencocokan catatan antara subsistem donasi, gateway, penerima, dan rekonsiliasi. | Format referensi dan korelasi log perlu disepakati (NFR-005). |
| **Pemulihan dan pencegahan duplikasi** | Kegagalan dapat ditelusuri dan pengiriman ulang tidak menghasilkan catatan ganda. | Retry, idempotensi, monitoring, dan target pemulihan perlu konfirmasi (NFR-007/FR-015). |
| **Kinerja** | Pengiriman dilakukan dalam waktu yang disepakati setelah transaksi memenuhi syarat. | Target waktu respons, throughput, dan SLA belum ditentukan (OQ-006/OQ-014). |

### 6. Kriteria Penerimaan Awal

* [ ] Catatan hanya dikirim setelah transaksi memenuhi syarat pencatatan dan statusnya terverifikasi berhasil.
* [ ] Payload mengikuti skema/kontrak yang telah disepakati dengan pemilik modul penerima.
* [ ] Sistem mencatat respons penerimaan untuk setiap upaya pengiriman.
* [ ] Jika API gagal, sistem mencatat kegagalan dan mempertahankan referensi yang diperlukan untuk penelusuran/pemulihan.
* [ ] Pengiriman ulang dengan referensi yang sama tidak menghasilkan catatan donasi ganda.
* [ ] Transaksi yang belum terverifikasi berhasil tidak dikirim sebagai catatan donasi.

> *Kriteria ini bersifat awal. Pengujian rinci baru dapat ditetapkan setelah pemilik modul tujuan, kontrak API, dan aturan idempotensi disepakati.*

### 7. Hal yang Perlu Dikonfirmasi

1. Siapa pemilik modul penerima dan kelompok mana yang benar? Dokumen sumber menyebut Kelompok 1; penetapan tersebut perlu divalidasi dan tidak dianggap final.
2. Apa *endpoint*, metode HTTP, versi API, autentikasi, *payload*, dan mekanisme keamanan yang digunakan?
3. Apa *field* wajib, *field* opsional, tipe data, format tanggal/waktu, mata uang, dan daftar nilai status?
4. Referensi unik apa yang digunakan sebagai *correlation ID/idempotency key*?
5. Apa kode respons sukses, respons duplikat, validasi gagal, dan *server error*?
6. Kapan catatan dikirim: segera setelah status berhasil atau melalui proses terjadwal/*batch*?
7. Apakah setiap pembayaran berkala menghasilkan satu catatan tersendiri? Apakah pembayaran tautan satu kali (FR-014) juga dikirim?
8. Bagaimana *retry* dilakukan: pemicu, jeda, batas percobaan, *backoff*, monitoring, dan penanggung jawab pemulihan?
9. Bagaimana koreksi, pembatalan, *reversal*, atau perubahan status setelah catatan diterima ditangani?
10. Data contoh apa yang digunakan sebelum kontrak API final, siapa penyedianya, dan bagaimana persetujuan penggunaannya?
11. Apakah pengiriman catatan donasi, data tanda terima (FR-008), dan data rekonsiliasi (FR-010) merupakan proses terpisah?
12. Bagaimana aturan akses, retensi, audit, dan kepemilikan data donatur yang dikirim?

### 8. Catatan untuk Presentasi

* FR-009 berada setelah verifikasi transaksi pada FR-007. Fungsinya meneruskan catatan donasi ke modul penerima, bukan memproses pembayaran.
* Modul penerima bertanggung jawab atas pencatatan penerimaan donasi dan pengelolaan akun donatur; FR-009 bertanggung jawab pada pengiriman dan keterlacakan integrasi.
* Fokus risiko teknis adalah kontrak API yang belum final, kegagalan pengiriman, pemulihan, dan pencegahan duplikasi.
* Judul/aktor sumber menyebut Kelompok 1, tetapi penetapan kelompok tujuan harus dikonfirmasi. Sampaikan sebagai isu validasi, bukan keputusan.

### 9. Status Dokumen

**Draft untuk Presentasi – Menunggu Validasi dan Persetujuan.** Dokumen ini telah dirapikan untuk pembahasan SRS, tetapi belum menjadi persyaratan final yang disetujui klien/pemilik sistem. Bagian yang berstatus “Perlu Konfirmasi” harus diputuskan sebelum *baseline* kebutuhan dan implementasi.  
*Acuan isi: FR-009 versi 0.1 yang diunggah dan SRS Draft v0.2 sebagaimana dirujuk dalam dokumen sumber. Isi yang tidak didukung sumber tidak ditetapkan sebagai keputusan teknis.*