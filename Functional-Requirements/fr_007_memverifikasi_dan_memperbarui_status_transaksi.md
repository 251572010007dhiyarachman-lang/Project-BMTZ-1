# FUNCTIONAL REQUIREMENT (FR)

## FR-007 — MEMVERIFIKASI DAN MEMPERBARUI STATUS TRANSAKSI

**Sistem Donasi Berulang dan Kanal Pembayaran Digital**  
* **Organisasi:** Baitulmal Tazkia
* **Versi dokumen:** Draft untuk Presentasi
* **Status:** DRAFT UNTUK PRESENTASI – MENUNGGU VALIDASI DAN PERSETUJUAN

| Informasi | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-007 |
| **Nama Kebutuhan** | Memverifikasi dan Memperbarui Status Transaksi |
| **Aktor Utama** | Subsistem Donasi Berulang; penyedia status transaksi yang disepakati (Payment Gateway Artivisi menurut SRS, sumber final perlu konfirmasi) |
| **Tujuan** | Memeriksa dan memperbarui status transaksi berdasarkan respons tervalidasi serta menyimpan waktu dan referensi hasil. |
| **Prioritas** | Belum ditentukan |
| **Acuan** | SRS Draft v0.2; tanggal acuan pada sumber: 26 Oktober 2026 |

### 1. Deskripsi Functional Requirement

Ketika respons atau status transaksi tersedia dari sumber yang disepakati, sistem memeriksa status dari sumber tepercaya, memperbarui status transaksi berdasarkan respons yang tervalidasi, serta menyimpan waktu dan referensi hasilnya. Status berhasil hanya boleh ditetapkan berdasarkan bukti yang terverifikasi. Jika status masih *pending*, tidak dikenal, atau terlambat, sistem tidak boleh menganggap transaksi berhasil dan pemeriksaan ulang mengikuti kontrak yang disepakati.

* **Pemicu:** Respons atau status transaksi tersedia dari sumber yang disepakati.
* **Kondisi awal:** Referensi transaksi dapat dicocokkan.

### 2. Format Outline dan Batasan

* Pemeriksaan status transaksi dari sumber tepercaya.
* Pembaruan status transaksi berdasarkan respons yang tervalidasi.
* Penyimpanan waktu dan referensi hasil.
* Penanganan status *pending*, tidak dikenal, atau terlambat tanpa menganggap transaksi berhasil.

> **Batasan:** FR-007 hanya membahas pemeriksaan dan pembaruan status transaksi. Pengiriman permintaan ke gateway serta pencatatan kondisi penolakan/timeout berada pada FR-006; pengingat pada FR-005. Penyediaan data untuk tanda terima, integrasi lanjutan, rekonsiliasi/pelaporan, pencegahan duplikasi, dan notifikasi ditangani oleh FR terkait (FR-008, FR-009, FR-010, FR-015, dan FR-013).

### 3. Proses Bisnis

**Aktor:** Subsistem Donasi Berulang dan sumber status transaksi yang disepakati.

| Tahap | Aktivitas | Dasar / Catatan |
| :--- | :--- | :--- |
| 1 | Respons atau status transaksi tersedia dari sumber yang disepakati. | Tertulis di SRS; sumber dan cara perolehan status perlu konfirmasi. |
| 2 | Sistem mencocokkan status dengan referensi transaksi. | Disimpulkan dari kondisi awal SRS; aturan pencocokan perlu dirinci. |
| 3 | Sistem memeriksa status dari sumber tepercaya. | Tertulis di SRS; mekanisme verifikasi perlu konfirmasi. |
| 4 | Sistem memperbarui status berdasarkan respons yang tervalidasi. | Tertulis di SRS; daftar status dan pemetaan perlu konfirmasi. |
| 5 | Sistem menyimpan waktu dan referensi hasil. | Tertulis di SRS. |

**Alur alternatif:**
* **Pending, tidak dikenal, atau terlambat:** Sistem tidak menganggap transaksi berhasil; tidak menyatakan berhasil/gagal tanpa dasar; pemeriksaan ulang mengikuti kontrak. Waktu tunggu, mekanisme pemeriksaan ulang, dan dukungan penyimpanan status sementara perlu konfirmasi.
* **Hasil gagal dari sumber terverifikasi:** Sistem mencatat hasil gagal, mempertahankan referensi transaksi, dan menyediakan status untuk pemantauan atau rekonsiliasi. Bentuk penyediaan status dan aturan *retry* penagihan perlu konfirmasi.

### 4. Field, Tipe Data, dan Validasi

*SRS Draft v0.2 belum menetapkan tipe data, daftar status, maupun mekanisme verifikasi. Nama berikut merupakan field usulan untuk pembahasan, bukan nama kolom basis data atau keputusan final.*

| Field Usulan | Tipe Data | Validasi / Aturan Awal | Status |
| :--- | :--- | :--- | :--- |
| **Referensi transaksi** | Belum ditentukan | Dapat dicocokkan dengan transaksi terkait. | Perlu konfirmasi format dan keunikan. |
| **Sumber status/respons** | Belum ditentukan | Berasal dari sumber tepercaya yang disepakati. | Perlu konfirmasi sumber dan metode perolehan. |
| **Status transaksi** | Belum ditentukan | Status berhasil hanya berdasarkan bukti terverifikasi; pending dan gagal dibedakan. | Perlu konfirmasi daftar status dan pemetaan. |
| **Waktu hasil** | Belum ditentukan | Disimpan bersama hasil pemeriksaan/pembaruan. | Perlu konfirmasi format dan zona waktu. |
| **Referensi hasil** | Belum ditentukan | Disimpan untuk penelusuran hasil. | Perlu konfirmasi bentuk dan sumber referensi. |
| **Status sementara** | Belum ditentukan | Disimpan jika mekanisme mendukung. | Perlu konfirmasi apakah didukung. |

### 5. Mockup Alur Sistem

*SRS tidak menetapkan layar antarmuka khusus untuk FR-007 karena fungsi ini merupakan proses sistem. Karena itu, mockup berikut berupa diagram alur verifikasi, bukan tampilan halaman donatur. Apakah status ditampilkan kepada donatur atau staf masih perlu konfirmasi.*

```text
+-----------------------+     +-----------------------+     +-----------------------+     +-----------------------+
| Sumber status         |     | Subsistem Donasi      |     | Cocokkan referensi    |     | Perbarui status       |
| transaksi             | --> | Berulang              | --> | & validasi respons    | --> | + simpan waktu dan    |
| (yang disepakati)     |     | Menerima respons      |     |                       |     | referensi hasil       |
| Perlu konfirmasi      |     |                       |     |                       |     |                       |
+-----------------------+     +-----------------------+     +-----------------------+     +-----------------------+
                                                                        |
                                                                 [jika belum final]
                                                                        v
                              +-----------------------+     +-----------------------+     +-----------------------+
                              | Pending / tidak       |     | Pemeriksaan ulang     |     | Hasil gagal           |
                              | dikenal / terlambat   | --> | mengikuti kontrak     | --> | terverifikasi:        |
                              | Tidak dianggap        |     | (detail perlu         | [jika| catat hasil &         |
                              | berhasil              |     | konfirmasi)           |hasil| pertahankan referensi |
                              |                       |     |                       |gagal| transaksi             |
                              +-----------------------+     +-----------------------+     +-----------------------+
```
*Sketsa proses sistem; bukan desain layar donatur. Mekanisme callback/webhook atau polling belum ditetapkan.*  
*Catatan visual: Susunan alur, nama status, dan kontrak data harus dikonfirmasi kepada penyedia gateway dan PIC. Jika status ditampilkan pada antarmuka, arahan awal pada SRS menyebut warna navy blue dan putih.*

### 6. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Awal | Catatan |
| :--- | :--- | :--- |
| **Keandalan status** | Status berhasil hanya berdasarkan hasil terverifikasi; pending dan gagal tetap dibedakan. | Dasar tersedia pada SRS NFR-002 dan kriteria penerimaan. |
| **Integrasi** | Pertukaran data dengan sumber status menggunakan kontrak API yang disepakati. | Dasar tersedia pada SRS NFR-003; kontrak belum final. |
| **Keterlacakan** | Waktu dan referensi hasil disimpan agar status dapat dicocokkan antarsubsistem. | Dasar umum tersedia pada SRS NFR-005; format referensi perlu disepakati. |
| **Pemulihan kegagalan integrasi** | Kegagalan pertukaran data dapat ditelusuri dan tidak menyebabkan transaksi dianggap berhasil atau tercatat ganda. | NFR-007 perlu klarifikasi; logging, monitoring, retry, dan target pemulihan belum ditetapkan. |
| **Kinerja** | Waktu tunggu dan target waktu respons mengikuti hasil klarifikasi. | Belum ditetapkan; terkait OQ-005 dan OQ-014. |

### 7. Kriteria Penerimaan Awal

* [ ] Status berhasil hanya ditetapkan berdasarkan bukti terverifikasi.
* [ ] Status pending dan gagal tetap dibedakan.
* [ ] Sistem memperbarui status berdasarkan respons tervalidasi dan menyimpan waktu serta referensi hasil.
* [ ] Status pending, tidak dikenal, atau terlambat tidak dianggap berhasil; pemeriksaan ulang mengikuti kontrak.
* [ ] Hasil gagal dari sumber terverifikasi dicatat dan referensi transaksi tetap dipertahankan.

> *Kriteria penerimaan ini bersifat awal dan harus diperbarui setelah daftar status serta mekanisme verifikasi dikonfirmasi.*

### 8. Hal yang Perlu Dikonfirmasi

1. Apa sumber status yang tepercaya, dan apakah status diperoleh melalui *callback/webhook*, pemeriksaan berkala, atau keduanya?
2. Apa daftar status transaksi dari sumber dan bagaimana pemetaannya menjadi berhasil, gagal, atau *pending* di sistem?
3. Apa kriteria agar respons dianggap tervalidasi dan bukti dianggap terverifikasi?
4. Berapa lama sistem menunggu sebelum pemeriksaan ulang, dan bagaimana aturan pemeriksaan ulang menurut kontrak?
5. Apakah status sementara didukung dan disimpan?
6. Di mana batas antara pencatatan penolakan/timeout pada FR-006 dan pemeriksaan status pada FR-007?
7. Kapan dan bagaimana hasil terverifikasi memicu penyediaan data untuk tanda terima, integrasi lanjutan, dan rekonsiliasi/pelaporan (FR-008, FR-009, FR-010)?
8. Bagaimana hasil transaksi memengaruhi status kesediaan donasi, dan FR mana yang mengaturnya?
9. Siapa yang memantau status transaksi, dan bagaimana status disediakan untuk pemantauan?
10. Apakah *retry* dilakukan untuk tagihan gagal, dan bagaimana hubungannya dengan pembaruan status?

### 9. Catatan untuk Presentasi

* FR-007 berada setelah pengiriman permintaan ke gateway pada FR-006. Sistem memeriksa status dari sumber tepercaya, memperbarui status berdasarkan respons tervalidasi, lalu menyimpan waktu dan referensi hasil. Permintaan yang terkirim ke gateway tidak otomatis berarti pembayaran berhasil; keberhasilan harus menunggu bukti yang dapat diverifikasi.
* Jika ditanya mengapa daftar status dan mekanisme verifikasi belum dirinci: SRS Draft v0.2 sendiri menyatakan bahwa status gateway, mekanisme verifikasi, dan waktu tunggu masih perlu klarifikasi. Dokumentasi penyedia gateway serta kontrak API belum tersedia dalam bahan sumber.

### 10. Status Dokumen

**Draft untuk Presentasi – Menunggu Validasi dan Persetujuan.** Dokumen ini merapikan isi FR-007 berdasarkan sumber yang diberikan. Field, tipe data, daftar status, mekanisme *callback/polling*, *retry*, dan tampilan status belum boleh dianggap sebagai keputusan final sebelum disepakati dengan PIC dan penyedia gateway.