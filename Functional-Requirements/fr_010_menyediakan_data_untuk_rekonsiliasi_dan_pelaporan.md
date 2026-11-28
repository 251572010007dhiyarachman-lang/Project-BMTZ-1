# BAITULMAL TAZKIA
## SISTEM DONASI BERULANG DAN KANAL PEMBAYARAN DIGITAL

### FUNCTIONAL REQUIREMENT (FR)
# FR-010: MENYEDIAKAN DATA UNTUK REKONSILIASI DAN PELAPORAN

**Versi:** 1.0 | **Status:** Draft untuk Review dan Validasi Klien | **Tanggal:** 25 November 2026  
**Acuan:** SRS dan BRS Fitur 4 versi 1.0, tanggal acuan 14 November 2026.

---

## A. Identitas Kebutuhan

| Informasi | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-010 |
| **Nama Kebutuhan** | Menyediakan Data untuk Rekonsiliasi dan Pelaporan |
| **Aktor Utama** | Sistem Fitur 4; Kelompok 5 – Rekonsiliasi dan Settlement; serta modul pelaporan yang pemilik dan jalur integrasinya masih perlu dikonfirmasi. |
| **Tujuan** | Menyiapkan dan menyediakan data hasil penagihan/pembayaran—sekurang-kurangnya referensi transaksi, nominal, waktu, dan status terverifikasi—untuk mendukung pencocokan dan kebutuhan pelaporan sesuai kontrak data. |
| **Pemicu** | Data hasil penagihan/pembayaran tersedia dan status transaksi telah ditetapkan melalui proses verifikasi FR-007. |
| **Kondisi Awal** | Referensi transaksi tersedia; kontrak data, tujuan, dan mekanisme pertukaran dengan pihak terkait telah disepakati. |
| **Prioritas Usulan** | Must Have — usulan, perlu persetujuan Baitulmal Tazkia. |
| **Tingkat Kesulitan Usulan** | 4 — Hard |
| **Status** | Draft untuk review dan validasi; pemilik modul pelaporan, jalur data, skema, frekuensi, dan mekanisme sinkronisasi belum final. |

---

## B. Deskripsi Functional Requirement

Ketika data hasil penagihan/pembayaran tersedia dan status transaksi telah diverifikasi melalui FR-007, sistem menyiapkan data transaksi yang diperlukan untuk kebutuhan rekonsiliasi dan pelaporan. Data sekurang-kurangnya memuat referensi transaksi, nominal, waktu, dan status terverifikasi. Data kemudian dikirimkan atau disediakan kepada Kelompok 5 dan/atau modul pelaporan sesuai tujuan serta kontrak data yang telah disepakati. Apabila pertukaran gagal atau data belum lengkap, sistem mencatat kondisi tersebut dan tidak menandai data sebagai berhasil terkirim atau terkonfirmasi. Data sumber tetap dipertahankan untuk mendukung sinkronisasi ulang.

### B.1 Batasan Ruang Lingkup
* FR-010 hanya mencakup penyiapan dan penyediaan data transaksi untuk kebutuhan rekonsiliasi dan pelaporan.
* Pencocokan mutasi rekening dan proses *settlement* merupakan tanggung jawab Kelompok 5, bukan Fitur 4.
* Pemilik modul pelaporan dan jalur penyaluran data—melalui Kelompok 5, langsung ke modul pelaporan, atau keduanya—belum ditetapkan.
* Verifikasi status transaksi berada pada FR-007; penyediaan data tanda terima pada FR-008; pengiriman catatan donasi untuk integrasi pada FR-009; pemrosesan pembayaran pada FR-006.
* FR-010 tidak menentukan isi laporan publik, melakukan verifikasi/publikasi laporan, atau membuka data pribadi donatur kepada publik.

---

## C. Proses Bisnis

| Tahap | Aktor | Aktivitas | Dasar / Catatan |
| :---: | :--- | :--- | :--- |
| **1** | Sistem Fitur 4 | Mengenali tersedianya data hasil penagihan/pembayaran dengan status yang telah diverifikasi. | Dasar tersedia pada SRS; pemicu teknis perlu konfirmasi. |
| **2** | Sistem Fitur 4 | Memastikan tujuan dan kontrak data dengan Kelompok 5 dan/atau modul pelaporan telah disepakati. | Kondisi awal; jalur integrasi belum final. |
| **3** | Sistem Fitur 4 | Menyiapkan data transaksi yang mencakup referensi, nominal, waktu, dan status terverifikasi. | Sesuai kebutuhan SRS; rincian field perlu konfirmasi. |
| **4** | Sistem Fitur 4 | Mengirimkan atau menyediakan data kepada tujuan sesuai kontrak data. | Kanal, autentikasi, frekuensi, dan jadwal perlu konfirmasi. |
| **5** | Sistem Fitur 4 | Mencatat status pertukaran agar hasil pengiriman dapat ditelusuri. | Format status dan pencatatan perlu konfirmasi. |
| **6** | Sistem Fitur 4 | Jika gagal atau data belum lengkap, mencatat kondisi dan mempertahankan data untuk sinkronisasi ulang. | Aturan retry dan penanggung jawab perlu konfirmasi. |

### C.1 Alur Alternatif dan Kondisi Khusus
* **Pertukaran data gagal:** Sistem mencatat kegagalan, tidak menandai data sebagai berhasil terkirim/terkonfirmasi, dan mempertahankan data untuk sinkronisasi ulang.
* **Data belum lengkap:** Sistem mencatat bahwa data belum lengkap dan tidak menandainya sebagai berhasil terkirim.
* **Status transaksi gagal atau pending:** Status tersebut disampaikan sesuai kontrak dan tidak boleh dinyatakan sebagai transaksi berhasil.
* **Status transaksi berubah setelah data pertama kali disediakan:** Mekanisme pengiriman pembaruan status belum ditetapkan dan perlu konfirmasi.

---

## D. Data, Tipe Data, dan Validasi

| Elemen Data | Tujuan / Validasi Awal | Status |
| :--- | :--- | :--- |
| **Referensi transaksi** | Menelusuri dan mencocokkan transaksi antarsubsistem. | Format dan aturan keunikan perlu konfirmasi. |
| **Referensi gateway** | Mengacu pada referensi yang diberikan Payment Gateway Artivisi. | Nama dan format field perlu dikonfirmasi. |
| **Nominal** | Sesuai hasil penagihan/pembayaran. | Tipe, mata uang, presisi, dan kewajiban field perlu konfirmasi. |
| **Waktu transaksi** | Mengacu pada waktu hasil penagihan/pembayaran. | Format dan zona waktu perlu konfirmasi. |
| **Status transaksi** | Sesuai hasil verifikasi; status sukses, gagal, dan pending dibedakan. | Daftar status final dan pemetaan perlu konfirmasi. |
| **Referensi pencocokan** | Mendukung proses pencocokan yang dilakukan pihak rekonsiliasi. | Bentuk dan sumber referensi perlu konfirmasi. |
| **Status pengiriman data** | Menunjukkan data terkirim, gagal, atau belum lengkap. | Nilai status dan cara pencatatan perlu konfirmasi. |

*Catatan: Tipe data, nama field basis data, format, dan aturan validasi final belum ditetapkan. Tabel ini merupakan daftar kebutuhan data untuk divalidasi, bukan skema final.*

---

## E. Gambaran UI / Pertukaran Data

*FR-010 merupakan fungsi pertukaran data antarsubsistem, bukan fitur yang digunakan langsung oleh donatur. Gambaran konseptual:*

| Urutan | Proses / Informasi |
| :---: | :--- |
| **1** | Transaksi telah diverifikasi melalui FR-007. |
| **2** | Sistem menyiapkan referensi transaksi, referensi gateway, nominal, waktu, status, dan referensi pencocokan sesuai kontrak. |
| **3** | Sistem menyediakan data kepada Kelompok 5 dan/atau modul pelaporan melalui jalur yang disepakati. |
| **4** | Sistem mencatat status pertukaran: terkirim, gagal, atau belum lengkap sesuai nilai final yang disepakati. |
| **5** | Jika gagal/belum lengkap, data tetap disimpan untuk penelusuran dan sinkronisasi ulang. |

*Catatan: Skema, kanal, autentikasi, tujuan, dan jadwal pertukaran harus disepakati. FR-010 tidak menetapkan desain UI maupun format laporan publik.*

---

## F. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Terkait | Acuan / Catatan |
| :--- | :--- | :--- |
| **Keamanan** | Data donatur dan transaksi dilindungi; hanya data yang disepakati yang disediakan. | NFR-001; aturan akses, retensi, dan kepemilikan perlu konfirmasi. |
| **Keandalan status** | Status yang disediakan harus sesuai hasil verifikasi; pending/gagal tidak dinyatakan berhasil. | NFR-002 dan FR-007. |
| **Integrasi** | Pertukaran data menggunakan kontrak yang disepakati, bukan akses langsung ke basis data kelompok lain. | NFR-003; kontrak integrasi belum final. |
| **Keterlacakan** | Data transaksi memiliki referensi yang memungkinkan pencocokan antarsubsistem. | NFR-005; format referensi perlu disepakati. |
| **Pemulihan kegagalan** | Kegagalan pertukaran dapat ditelusuri dan data dipertahankan untuk sinkronisasi ulang. | NFR-007; logging, retry, dan monitoring perlu konfirmasi. |
| **Kinerja** | Data disediakan sesuai jadwal/frekuensi yang disepakati. | Target waktu, volume transaksi, dan ketersediaan belum ditetapkan. |

---

## G. Kriteria Penerimaan
- [ ] Sistem dapat menyiapkan data hasil penagihan/pembayaran sekurang-kurangnya berupa referensi transaksi, nominal, waktu, dan status terverifikasi.
- [ ] Data dapat ditelusuri menggunakan referensi yang disepakati dan status yang disediakan sesuai hasil verifikasi.
- [ ] Data dikirimkan atau disediakan kepada tujuan yang disepakati sesuai format dan jadwal dalam kontrak data.
- [ ] Jika pertukaran gagal atau data belum lengkap, sistem mencatat kondisi tersebut dan tidak menandai data sebagai berhasil terkirim atau terkonfirmasi.
- [ ] Data transaksi tetap dipertahankan agar dapat digunakan untuk sinkronisasi ulang ketika pengiriman gagal.

*Catatan: Kriteria penerimaan ini merupakan kriteria awal. Pengujian final memerlukan kesepakatan mengenai skema data, tujuan, status, kanal, frekuensi, dan mekanisme sinkronisasi.*

---

## H. Prioritas dan Tingkat Kesulitan

| Komponen | Usulan | Dasar |
| :--- | :--- | :--- |
| **Prioritas MoSCoW** | Must Have — usulan | Kebutuhan penyediaan data untuk administrasi, rekonsiliasi, dan pelaporan terkait BR-010 yang berprioritas Tinggi; perlu persetujuan klien. |
| **Tingkat Kesulitan** | 4 — Hard | Melibatkan penyiapan data lintas kebutuhan, integrasi dengan lebih dari satu tujuan potensial, pemetaan status, keterlacakan, keamanan, dan sinkronisasi saat gagal. |

### Dasar Pertimbangan Penilaian
Skala kesulitan 1–5: **1–2 Easy**, **3 Medium**, dan **4–5 Hard**. FR-010 diusulkan pada tingkat **4 (Hard)** karena memerlukan pertukaran data untuk kebutuhan rekonsiliasi dan pelaporan dengan tujuan serta kontrak yang belum final, termasuk penanganan status, keterlacakan, dan sinkronisasi ulang. Prioritas *Must Have* merupakan usulan berdasarkan BR-010 yang berprioritas Tinggi, bukan persetujuan final klien.

---

## I. Hal yang Perlu Dikonfirmasi kepada Klien / Tim Teknis
1. Data apa saja yang wajib diterima Kelompok 5 untuk rekonsiliasi, dan bagaimana status gagal atau *pending* disampaikan?
2. Apakah pelaporan dilakukan oleh Kelompok 5, modul laporan terpisah, atau keduanya? Siapa pemilik masing-masing proses?
3. Apa tujuan, isi, dan penerima data pelaporan?
4. Apakah data pelaporan disalurkan melalui Kelompok 5 atau langsung ke modul pelaporan?
5. Apa skema data, kanal pertukaran (API atau mekanisme lain), dan metode autentikasi yang digunakan?
6. Kapan pertukaran dilakukan: setiap transaksi, terjadwal, atau berdasarkan permintaan?
7. Apa daftar status final dan bagaimana perubahan status, misalnya *pending* menjadi sukses, dikirimkan setelah data pertama kali disediakan?
8. Siapa yang menangani kegagalan pertukaran dan sinkronisasi ulang? Bagaimana pencegahan data terkirim ganda dilakukan?
9. Apakah transaksi dari tautan pembayaran satu kali FR-014 juga termasuk data yang disediakan FR-010?
10. Apakah data rekonsiliasi, tanda terima FR-008, dan catatan donasi FR-009 merupakan proses pertukaran terpisah?
11. Bagaimana aturan akses, retensi, audit, dan kepemilikan data?
12. Berapa target waktu, volume transaksi, dan tingkat ketersediaan yang diharapkan?

---

## J. Checklist Konfirmasi Client

| ID & Nama Kebutuhan | Prioritas Usulan | Kesulitan Usulan | Tidak Dibutuhkan / Catatan Client |
| :--- | :--- | :--- | :--- |
| **FR-010 — Menyediakan Data untuk Rekonsiliasi dan Pelaporan** | Must Have — usulan | 4 — Hard | |

*Catatan: Isi kolom terakhir apabila kebutuhan tidak diperlukan atau terdapat catatan/perubahan dari klien. Biarkan kosong jika kebutuhan tetap diperlukan.*

---

## K. Catatan dan Status Dokumen
FR-010 menyediakan data transaksi terverifikasi untuk mendukung kebutuhan rekonsiliasi dan pelaporan. FR-010 tidak melakukan pencocokan mutasi rekening atau *settlement* karena hal tersebut merupakan tanggung jawab Kelompok 5; FR-010 juga tidak menentukan atau mempublikasikan laporan publik. Dokumen ini diselaraskan dengan SRS/BRS Fitur 4 versi 1.0 tanggal 14 November 2026. Pemilik modul pelaporan, jalur integrasi, skema, frekuensi, dan aturan sinkronisasi masih memerlukan validasi.  
**Status:** Draft untuk Review dan Validasi Klien; belum menjadi baseline sebelum disetujui.