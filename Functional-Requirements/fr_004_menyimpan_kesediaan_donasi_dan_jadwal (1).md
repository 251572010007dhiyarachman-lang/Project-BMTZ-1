# BAITULMAL TAZKIA
## SISTEM DONASI BERULANG DAN KANAL PEMBAYARAN DIGITAL

### FUNCTIONAL REQUIREMENT (FR)
# FR-004: MENYIMPAN KESEDIAAN DONASI DAN JADWAL

**Versi:** 1.0 | **Status:** Draft untuk Review dan Validasi Klien | **Tanggal:** 25 November 2026  
**Acuan:** SRS dan BRS Fitur 4 versi 1.0, tanggal acuan 14 November 2026.

---

## A. Identitas Kebutuhan

| Informasi | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-004 |
| **Nama Kebutuhan** | Menyimpan Kesediaan Donasi dan Jadwal |
| **Aktor Utama** | Calon donatur / donatur; Sistem Fitur 4 |
| **Tujuan** | Menyimpan informasi kesediaan donasi berulang, persetujuan donatur, dan jadwal beserta data pendaftaran yang diperlukan, serta memberikan hasil pendaftaran kepada donatur. |
| **Pemicu** | Donatur mengirim pendaftaran setelah melengkapi pengaturan pada FR-003 dan memberikan persetujuan yang disyaratkan. |
| **Kondisi Awal** | Data nominal, jadwal/periode, dan peruntukan telah diisi serta lolos validasi FR-003; persetujuan yang disyaratkan tersedia. |
| **Prioritas Usulan** | Must Have — usulan, perlu persetujuan Baitulmal Tazkia. |
| **Tingkat Kesulitan Usulan** | 4 — Hard |
| **Status** | Draft untuk review dan validasi; belum menjadi baseline implementasi. |

---

## B. Deskripsi Functional Requirement

Setelah donatur melengkapi pengaturan donasi berulang dan memberikan persetujuan sesuai ketentuan, sistem menerima pendaftaran dan menyimpan informasi kesediaan donasi beserta jadwalnya. Informasi yang disimpan mencakup identitas/referensi pendaftaran, nominal, jadwal/periode, peruntukan, status awal, dan bukti persetujuan sesuai aturan yang disepakati. Sistem memberikan hasil pendaftaran kepada donatur. Apabila penyimpanan gagal, sistem tidak boleh menampilkan pendaftaran berhasil dan kegagalan harus dicatat agar dapat ditelusuri. Bentuk bukti persetujuan, rincian data donatur, format referensi, dan status awal masih perlu dikonfirmasi. Pendaftaran tersimpan tidak berarti pembayaran telah berhasil.

### 1. Format Outline dan Batasan
* Sistem menerima data pendaftaran yang telah dilengkapi dan divalidasi pada FR-003.
* Sistem memastikan persetujuan yang disyaratkan tersedia.
* Sistem menyimpan referensi pendaftaran, nominal, jadwal/periode, peruntukan, status, dan bukti persetujuan.
* Sistem memberikan hasil pendaftaran kepada donatur.
* Jika penyimpanan gagal, sistem tidak menampilkan status berhasil dan mencatat kegagalan agar dapat ditelusuri.

> **Batasan:** FR-004 hanya mencakup penyimpanan kesediaan donasi dan jadwal serta penyampaian hasil pendaftaran. Pengisian dan validasi termasuk FR-003. Pembayaran gateway dan verifikasi status pembayaran termasuk FR-006/FR-007. Pengingat, notifikasi, jeda, pembatalan, dan integrasi ke fitur lain berada pada FR terkait.

### 2. Proses Bisnis

| Tahap | Aktivitas | Dasar / Catatan |
| :---: | :--- | :--- |
| **1** | Donatur mengirim pendaftaran yang telah dilengkapi. | Tertulis di SRS; titik aksi/tombol pengiriman perlu konfirmasi. |
| **2** | Sistem memastikan data wajib dan persetujuan yang disyaratkan tersedia. | Disimpulkan dari kondisi awal dan alur utama; bentuk/lokasi consent perlu konfirmasi. |
| **3** | Sistem menyimpan referensi, nominal, jadwal/periode, peruntukan, status, dan bukti persetujuan. | Tertulis di SRS; rincian field dan aturan penyimpanan perlu konfirmasi. |
| **4** | Sistem memberikan hasil pendaftaran kepada donatur. | Tertulis di SRS; bentuk tampilan dan isi pesan perlu konfirmasi. |

> **Alur Alternatif — Penyimpanan Gagal:** Sistem tidak menampilkan pendaftaran sukses dan mencatat kegagalan agar dapat ditelusuri. Isi pesan kepada donatur, mekanisme percobaan ulang, dan tindakan jika consent belum tersedia masih perlu konfirmasi.

### 3. Field, Tipe Data, dan Validasi

| Field | Tipe Data | Validasi / Aturan Awal | Status |
| :--- | :--- | :--- | :--- |
| **ID/referensi pendaftaran** | Belum ditentukan | Pendaftaran berhasil memiliki identitas/referensi yang dapat ditelusuri. | Perlu konfirmasi format, pembentuk, dan keunikan. |
| **Identitas donatur** | Belum ditentukan | Hanya data yang diperlukan dan disetujui yang disimpan. | Perlu konfirmasi jenis data wajib. |
| **Nominal donasi** | Mengikuti FR-003 | Nilai berasal dari data pengaturan yang telah divalidasi. | Mengikuti aturan FR-003. |
| **Jadwal/periode donasi** | Mengikuti FR-003 | Nilai berasal dari data pengaturan yang telah divalidasi. | Mengikuti aturan FR-003. |
| **Peruntukan donasi** | Mengikuti FR-003 | Nilai berasal dari data pengaturan yang telah divalidasi. | Mengikuti aturan FR-003. |
| **Status pendaftaran** | Belum ditentukan | Pendaftaran tersimpan memiliki status awal yang jelas. | Perlu konfirmasi nama dan arti status awal. |
| **Bukti persetujuan (consent)** | Belum ditentukan | Bukti persetujuan tersimpan sesuai mekanisme yang disujui. | Perlu konfirmasi bentuk, waktu, versi, dan cakupan persetujuan. |
| **Catatan kegagalan** | Belum ditentukan | Kegagalan penyimpanan dicatat untuk penelusuran. | Perlu konfirmasi isi log, akses, dan masa retensi. |

### 4. Mockup Konseptual

```text
+-----------------------------------------------------------------------+
| HASIL PENDAFTARAN DONASI BERULANG                                     |
+-----------------------------------------------------------------------+
| Pesan hasil pendaftaran : [ pesan hasil — perlu konfirmasi          ] |
| Referensi pendaftaran   : [ ID/referensi                            ] |
| Status pendaftaran      : [ status awal                             ] |
| Ringkasan donasi        : [ nominal, jadwal, peruntukan —           ] |
|                           [ jika disepakati                         ] |
+-----------------------------------------------------------------------+
```
*Catatan: Jika penyimpanan gagal, tampilkan informasi bahwa pendaftaran belum berhasil; jangan tampilkan status sukses. Mockup ini konseptual, bukan desain UI final. Arahan visual SRS NFR-006 adalah navy blue dan putih.*

### 5. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Terkait | Catatan |
| :--- | :--- | :--- |
| **Keamanan** | Data donatur dan persetujuan dilindungi dari akses tidak berwenang. | Mengacu NFR-001 SRS. |
| **Keandalan** | Penyimpanan gagal tidak boleh menghasilkan status sukses palsu. | Selaras NFR-002 dan kriteria penerimaan FR-004. |
| **Konsistensi/keterlacakan** | Pendaftaran memiliki referensi yang dapat ditelusuri. | Mengacu NFR-005 SRS; format referensi perlu ditetapkan. |
| **Kemudahan penggunaan** | Hasil pendaftaran dan pesan kegagalan mudah dipahami. | Mengacu NFR-004 SRS. |
| **Tampilan** | Antarmuka mengikuti navy blue dan putih. | Mengacu NFR-006 SRS. |

### 6. Kriteria Penerimaan
- [ ] Sistem menerima pendaftaran setelah data pengaturan dilengkapi dan persetujuan yang disyaratkan tersedia.
- [ ] Sistem menyimpan referensi pendaftaran, nominal, jadwal/periode, peruntukan, status, dan bukti persetujuan sesuai aturan yang disepakati.
- [ ] Pendaftaran berhasil memiliki ID/referensi dan status awal yang jelas.
- [ ] Sistem memberikan hasil pendaftaran kepada donatur.
- [ ] Jika penyimpanan gagal, sistem tidak menampilkan pendaftaran berhasil.
- [ ] Kegagalan penyimpanan dicatat agar dapat ditelusuri.

### 7. Prioritas dan Tingkat Kesulitan

| Komponen | Usulan | Dasar |
| :--- | :--- | :--- |
| **Prioritas MoSCoW** | Must Have — usulan, perlu persetujuan Baitulmal Tazkia. | Must Have diturunkan dari BR-004 pada BRS yang berprioritas Tinggi. |
| **Tingkat kesulitan** | 4 — Hard | 4 — Hard karena membutuhkan penyimpanan konsisten, referensi terlacak, pengelolaan bukti persetujuan, keamanan data, dan penanganan kegagalan. |

### 8. Dasar Pertimbangan Penilaian
Skala kesulitan 1–5: **1–2 Easy**, **3 Medium**, dan **4–5 Hard**. FR-004 diusulkan pada tingkat **4 (Hard)** karena melibatkan penyimpanan beberapa unsur data, bukti persetujuan, referensi yang dapat ditelusuri, status awal, dan penanganan kegagalan agar tidak muncul status sukses palsu. Prioritas *Must Have* merupakan usulan berdasarkan BR-004 yang berprioritas Tinggi, bukan persetujuan final klien.

### 9. Hal yang Perlu Dikonfirmasi kepada Klien
1. Persetujuan apa yang harus diberikan donatur dan kapan persetujuan diberikan?
2. Apakah persetujuan satu kali cukup untuk donasi berulang atau perlu persetujuan pada setiap periode pembayaran?
3. Bukti persetujuan apa yang harus disimpan (waktu, pernyataan, versi persetujuan)?
4. Data identitas donatur apa saja yang wajib disimpan?
5. Apa format ID/referensi pendaftaran dan bagaimana referensi digunakan untuk penelusuran?
6. Apa status awal pendaftaran setelah berhasil disimpan?
7. Informasi apa yang ditampilkan pada hasil pendaftaran?
8. Bagaimana pesan kegagalan disampaikan dan apakah donatur dapat mengirim ulang pendaftaran?
9. Bagaimana kegagalan penyimpanan dicatat, siapa yang dapat mengakses catatan, dan berapa lama disimpan?
10. Bagaimana aturan akses, retensi, dan kepemilikan data pendaftaran?

### 10. Checklist Konfirmasi Client

| ID & Nama Kebutuhan | Prioritas Usulan | Kesulitan Usulan | Tidak Dibutuhkan / Catatan Client |
| :--- | :--- | :--- | :--- |
| **FR-004 — Menyimpan Kesediaan Donasi dan Jadwal** | Must Have — usulan, perlu persetujuan Baitulmal Tazkia. | 4 — Hard | |

### 11. Catatan dan Status Dokumen
FR-004 berada setelah FR-003. Fungsi ini menyimpan kesediaan donasi dan jadwal, termasuk bukti persetujuan yang disyaratkan. FR-004 tidak berarti pembayaran telah diproses atau berhasil; proses pembayaran dan verifikasi status transaksi diatur pada FR-006 dan FR-007. Dokumen diselaraskan dengan SRS/BRS Fitur 4 versi 1.0 tanggal 14 November 2026. Bentuk consent, rincian data, referensi, status awal, dan penanganan pengiriman ulang masih perlu konfirmasi.  
**Status:** Draft untuk Review dan Validasi Klien.