# BAITULMAL TAZKIA
## SISTEM DONASI BERULANG DAN KANAL PEMBAYARAN DIGITAL

### FUNCTIONAL REQUIREMENT (FR)
# FR-014: MEMBUAT TAUTAN PEMBAYARAN SATU KALI

**Versi:** 1.0 | **Status:** Draft untuk Review dan Validasi Klien | **Tanggal:** 25 November 2026  
**Acuan:** SRS dan BRS Fitur 4 versi 1.0, tanggal acuan 14 November 2026.

---

## A. Identitas Kebutuhan

| Informasi | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-014 |
| **Nama Kebutuhan** | Membuat Tautan Pembayaran Satu Kali |
| **Aktor Utama** | Donatur dan/atau staf internal yang diberi kewenangan; sistem; Payment Gateway. |
| **Tujuan** | Menyediakan pembuatan tautan pembayaran satu kali apabila fungsi tersebut disetujui BMT dan didukung oleh Payment Gateway. |
| **Pemicu** | Donatur atau staf yang berwenang memulai kebutuhan pembayaran satu kali untuk donasi. |
| **Kondisi Awal** | Fungsi tautan pembayaran satu kali telah disetujui; nominal dan informasi donasi tersedia; integrasi gateway mendukung pembuatan tautan. |
| **Prioritas Usulan** | Could Have — usulan, perlu persetujuan Baitulmal Tazkia. |
| **Tingkat Kesulitan Usulan** | 4 — Hard |
| **Status** | Draft untuk review dan validasi; belum menjadi baseline implementasi. |

---

## B. Deskripsi Functional Requirement

FR-014 menjelaskan kemampuan sistem menyediakan tautan pembayaran satu kali untuk suatu donasi. Sistem menyiapkan permintaan pembuatan tautan berdasarkan informasi donasi yang tersedia dan meneruskannya ke Payment Gateway apabila layanan tersebut mendukung. Tautan yang diterima ditampilkan atau disampaikan kepada pihak yang ditentukan. SRS secara eksplisit menyatakan fungsi ini bersyarat: digunakan hanya apabila disetujui dan didukung gateway. Cara pembuatan, masa berlaku, penerima tautan, dan metode pembayaran belum ditetapkan.

### 1. Format Outline dan Batasan
* Sistem menerima permintaan pembuatan tautan pembayaran satu kali dari aktor yang berwenang.
* Sistem memeriksa kelengkapan informasi donasi yang diperlukan.
* Sistem mengirim permintaan pembuatan tautan ke Payment Gateway melalui mekanisme yang disepakati.
* Sistem menerima respons gateway dan menyimpan referensi serta tautan jika berhasil dibuat.
* Sistem menampilkan atau menyediakan tautan kepada penerima yang ditentukan.
* Pembayaran melalui tautan tetap harus diverifikasi melalui FR-007; pembuatan tautan tidak berarti pembayaran berhasil.

### 2. Proses Bisnis

| Tahap | Aktivitas | Dasar / Catatan |
| :---: | :--- | :--- |
| **1** | Aktor memulai permintaan tautan pembayaran satu kali. | Fungsi bersyarat pada SRS FR-014. |
| **2** | Sistem memeriksa nominal dan informasi donasi yang diperlukan. | Field wajib dan aturan nominal perlu konfirmasi. |
| **3** | Sistem mengirim permintaan ke Payment Gateway. | Bergantung pada dukungan gateway dan kontrak integrasi. |
| **4** | Gateway mengembalikan tautan dan referensi atau respons gagal. | Format respons/API perlu konfirmasi. |
| **5** | Sistem menyimpan referensi tautan dan menyediakan tautan kepada penerima. | Penerima dan kanal penyampaian perlu konfirmasi. |

> **Alur Alternatif:** Jika fungsi belum disetujui atau gateway tidak mendukung pembuatan tautan, sistem tidak menampilkan opsi yang tidak tersedia. Jika gateway gagal atau tidak mengembalikan tautan yang valid, sistem mencatat kegagalan dan tidak menampilkan tautan seolah-olah berhasil dibuat. Jika pembayaran dilakukan melalui tautan, statusnya tetap menunggu verifikasi sesuai FR-007.

### 3. Field, Tipe Data, dan Validasi

| Field / Informasi | Tipe / Bentuk | Validasi / Aturan Awal | Status |
| :--- | :--- | :--- | :--- |
| **Nominal donasi** | Nilai mata uang | Harus valid sesuai aturan nominal yang disepakati. | Aturan rinci perlu konfirmasi. |
| **Identitas/program donasi** | ID atau referensi | Menghubungkan tautan dengan donasi/program yang benar. | Format referensi perlu konfirmasi. |
| **Referensi gateway** | String/ID | Disimpan untuk penelusuran transaksi/tautan. | Bergantung respons gateway. |
| **URL tautan pembayaran** | URL | Hanya disediakan jika diterima dan dinyatakan valid oleh gateway. | Dukungan gateway perlu konfirmasi. |
| **Masa berlaku tautan** | Tanggal/waktu atau durasi | Belum ditetapkan; mengikuti dukungan gateway dan keputusan BMT. | Perlu konfirmasi. |
| **Status tautan** | Status | Misalnya dibuat, gagal, kedaluwarsa, atau digunakan; daftar final perlu disepakati. | Perlu konfirmasi. |

### 4. Mockup Konseptual

```text
+-------------------------------------------------------+
| BUAT TAUTAN PEMBAYARAN SATU KALI                      |
+-------------------------------------------------------+
| Informasi donasi : [ program / keterangan           ] |
| Nominal          : [ nominal                        ] |
|                                                       |
|                  [ BUAT TAUTAN ]                      |
|                                                       |
| Tautan pembayaran: [ URL dari gateway               ] |
| Status           : [ berhasil dibuat / gagal /      ] |
|                    [ kedaluwarsa                    ] |
+-------------------------------------------------------+
```
*Catatan: Mockup ini konseptual, bukan desain UI final. Arahan visual SRS NFR-006 adalah navy blue dan putih.*

### 5. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Terkait | Catatan |
| :--- | :--- | :--- |
| **Keamanan** | Permintaan dan tautan hanya dapat diakses pihak berwenang. | Mengacu NFR-001. |
| **Integrasi** | Pembuatan tautan mengikuti API/mekanisme gateway yang disepakati. | Mengacu NFR-003; kemampuan gateway perlu validasi. |
| **Keandalan** | Tautan hanya ditampilkan jika respons pembuatan dinyatakan berhasil. | Mengacu NFR-002 sebagai prinsip status transaksi; status tautan perlu aturan. |
| **Konsistensi Data** | Tautan memiliki referensi yang dapat ditelusuri ke donasi/transaksi. | Mengacu NFR-005. |
| **Pemulihan Kegagalan** | Kegagalan pembuatan tautan dapat ditelusuri dan tidak menghasilkan catatan ganda. | Mengacu NFR-007. |

### 6. Kriteria Penerimaan
- [ ] Fungsi tautan pembayaran satu kali hanya diaktifkan setelah disetujui BMT dan dukungan gateway dipastikan.
- [ ] Sistem memeriksa informasi donasi yang diwajibkan sebelum mengirim permintaan.
- [ ] Jika gateway berhasil membuat tautan, sistem menyimpan referensi dan menyediakan tautan yang valid.
- [ ] Jika gateway gagal, sistem menampilkan informasi kegagalan dan tidak membuat tautan palsu.
- [ ] Pembayaran dari tautan tidak langsung dianggap berhasil sebelum diverifikasi melalui FR-007.

### 7. Prioritas dan Tingkat Kesulitan

| Komponen | Usulan | Dasar |
| :--- | :--- | :--- |
| **Prioritas MoSCoW** | Could Have — usulan, perlu persetujuan Baitulmal Tazkia. | Usulan analisis berdasarkan tujuan dan kebutuhan pada SRS; perlu persetujuan BMT. |
| **Tingkat Kesulitan** | 4 — Hard | FR-014 diusulkan pada tingkat 4 (Hard) karena bergantung pada kemampuan dan kontrak Payment Gateway, pembuatan referensi/URL, pengelolaan masa berlaku, serta keterkaitan tautan dengan proses verifikasi pembayaran. Prioritas *Could Have* merupakan usulan karena SRS menyatakan fungsi ini bersyarat pada persetujuan dan dukungan gateway, bukan fungsi inti yang dipastikan tersedia. |

### 8. Dasar Pertimbangan Penilaian
Skala kesulitan 1–5: **1–2 Easy**, **3 Medium**, dan **4–5 Hard**. FR-014 diusulkan pada tingkat **4 (Hard)** karena bergantung pada kemampuan dan kontrak Payment Gateway, pembuatan referensi/URL, pengelolaan masa berlaku, serta keterkaitan tautan dengan proses verifikasi pembayaran. Prioritas *Could Have* merupakan usulan karena SRS menyatakan fungsi ini bersyarat pada persetujuan dan dukungan gateway, bukan fungsi inti yang dipastikan tersedia. Penilaian prioritas dan kesulitan merupakan usulan, bukan keputusan final klien.

### 9. Hal yang Perlu Dikonfirmasi kepada Klien / Tim Teknis
1. Apakah BMT benar-benar membutuhkan tautan pembayaran satu kali? Jika tidak, FR-014 dapat dinyatakan tidak digunakan.
2. Apakah Payment Gateway Artivisi mendukung pembuatan tautan pembayaran satu kali melalui API atau dashboard?
3. Siapa yang boleh membuat tautan: donatur, staf internal, atau keduanya?
4. Informasi apa yang wajib dimasukkan saat membuat tautan (nominal, program, peruntukan, identitas donatur, keterangan)?
5. Apakah tautan dibuat untuk nominal tetap atau donatur dapat mengubah nominal saat membuka tautan?
6. Berapa lama masa berlaku tautan dan apakah tautan dapat diperpanjang atau dibuat ulang?
7. Bagaimana tautan disampaikan kepada penerima: ditampilkan di sistem, dikirim melalui kanal komunikasi, atau disalin manual?
8. Metode pembayaran apa saja yang tersedia melalui tautan tersebut?
9. Bagaimana status tautan (dibuat, digunakan, kedaluwarsa, dibatalkan) diperoleh dan diperbarui?
10. Apakah transaksi dari tautan satu kali juga masuk ke FR-008, FR-009, FR-010, FR-013, dan mekanisme pencegahan transaksi ganda FR-015?
11. Bagaimana sistem menghubungkan pembayaran dari tautan dengan referensi transaksi yang diverifikasi FR-007?

### 10. Checklist Konfirmasi Client

| ID & Nama Kebutuhan | Prioritas Usulan | Kesulitan Usulan | Tidak Dibutuhkan / Catatan Client |
| :--- | :--- | :--- | :--- |
| **FR-014 — Membuat Tautan Pembayaran Satu Kali** | Could Have — usulan, perlu persetujuan Baitulmal Tazkia. | 4 — Hard | |

*Catatan: Isi kolom terakhir apabila kebutuhan tidak diperlukan atau terdapat catatan/perubahan dari klien. Biarkan kosong jika kebutuhan tetap diperlukan.*

### 11. Catatan dan Status Dokumen
FR-014 bersifat kondisional sesuai SRS: tautan pembayaran satu kali hanya disediakan jika disetujui dan didukung Payment Gateway. FR-014 mencakup pembuatan dan penyediaan tautan, bukan verifikasi pembayaran. Pembayaran melalui tautan tetap mengikuti FR-007. Detail gateway, aktor, masa berlaku, nominal, dan kanal penyampaian belum ditetapkan.  
**Status:** Draft untuk Review dan Validasi Klien.