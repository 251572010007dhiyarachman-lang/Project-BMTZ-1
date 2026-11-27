# FUNCTIONAL REQUIREMENT (FR)

## FR-010 — Menyediakan Data untuk Rekonsiliasi dan Pelaporan

**Sistem Donasi Berulang dan Kanal Pembayaran Digital**

### A. Identitas Kebutuhan

| Elemen | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-010 |
| **Nama Kebutuhan** | Menyediakan Data untuk Rekonsiliasi dan Pelaporan |
| **Aktor/Pihak Terkait** | Sistem; Kelompok 5 (Rekonsiliasi dan Settlement); modul pelaporan (pemiliknya masih perlu dikonfirmasi). |
| **Tujuan** | Menyiapkan dan menyediakan data hasil penagihan/pembayaran—meliputi referensi transaksi, nominal, waktu, dan status terverifikasi—kepada Kelompok 5 dan/atau modul pelaporan sesuai kontrak data agar data dapat dicocokkan dan dilaporkan. |
| **Prioritas** | Belum ditentukan. |
| **Status Kebutuhan** | Dasar kebutuhan penyediaan data tersedia pada SRS Draft v0.2. Detail pemilik pelaporan, skema data, kanal, dan frekuensi pertukaran masih memerlukan konfirmasi. |

### B. Deskripsi Functional Requirement

Ketika data hasil penagihan/pembayaran telah tersedia dan status transaksi telah ditetapkan melalui proses verifikasi, sistem harus menyiapkan data transaksi yang diperlukan untuk rekonsiliasi dan pelaporan. Data tersebut sekurang-kurangnya memuat referensi transaksi, nominal, waktu, dan status terverifikasi. Sistem kemudian mengirimkan atau menyediakan data kepada Kelompok 5 dan/atau modul pelaporan sesuai kontrak data yang telah disepakati.

Apabila pertukaran data gagal atau data yang diperlukan belum lengkap, sistem harus mencatat kondisi tersebut dan tidak menandai data sebagai berhasil terkirim atau terkonfirmasi. Data transaksi tetap dipertahankan agar dapat digunakan dalam proses sinkronisasi ulang.

#### B.1 Pemicu dan Kondisi Awal

| Elemen | Ketentuan |
| :--- | :--- |
| **Pemicu** | Data hasil penagihan/pembayaran tersedia. |
| **Kondisi awal** | Kontrak data dengan Kelompok 5 atau modul pelaporan telah disepakati. Status transaksi telah ditetapkan melalui proses verifikasi (FR-007). |
| **Hasil yang diharapkan** | Data transaksi disediakan kepada tujuan yang disepakati dengan status pengiriman yang dapat ditelusuri. |

#### B.2 Alur Utama

1. Sistem mengenali tersedianya data hasil penagihan/pembayaran sebagai pemicu proses.
2. Sistem memastikan kontrak data dengan Kelompok 5 dan/atau modul pelaporan telah disepakati.
3. Sistem menyiapkan data transaksi yang mencakup referensi transaksi, nominal, waktu, dan status terverifikasi. Data untuk kebutuhan Kelompok 5 dapat mencakup referensi gateway dan referensi pencocokan sesuai SRS Bab 2.3.
4. Sistem mengirimkan atau menyediakan data kepada tujuan sesuai kontrak data yang berlaku.
5. Sistem menyediakan informasi status pertukaran agar hasil pengiriman dapat ditelusuri.

> **Catatan:** Langkah memastikan kontrak data merupakan penjabaran dari kondisi awal FR-010 pada SRS. Cara pemicu dijalankan (misalnya setiap transaksi atau terjadwal), kanal pengiriman, skema rinci, serta frekuensi pertukaran belum ditetapkan dan harus dikonfirmasi.

#### B.3 Alur Alternatif dan Penanganan Kondisi Khusus

| Kode | Kondisi | Perilaku Sistem |
| :--- | :--- | :--- |
| **ALT-01** | Pertukaran data gagal. | Sistem mencatat kegagalan dan tidak menandai data sebagai berhasil terkirim atau terkonfirmasi. Data transaksi tetap dipertahankan untuk sinkronisasi ulang. |
| **ALT-02** | Data yang diperlukan belum lengkap. | Sistem mencatat bahwa data belum lengkap dan tidak menandai data sebagai berhasil terkirim atau terkonfirmasi. |
| **ALT-03** | Status transaksi adalah gagal atau pending. | Sistem menyediakan status sesuai hasil verifikasi. Status gagal atau pending tidak boleh dinyatakan sebagai transaksi berhasil. Cara penyampaian dan daftar status final perlu dikonfirmasi. |
| **ALT-04** | Status transaksi berubah setelah data disediakan. | Mekanisme penyampaian perubahan status, termasuk perubahan dari pending menjadi sukses, belum ditentukan dan perlu dikonfirmasi. |

#### B.4 Batasan Ruang Lingkup

* FR-010 hanya mencakup penyiapan dan penyediaan data transaksi untuk kebutuhan rekonsiliasi dan pelaporan.
* Pencocokan mutasi rekening dan proses *settlement* merupakan tanggung jawab Kelompok 5, bukan tanggung jawab subsistem Donasi Berulang dan Kanal Pembayaran Digital.
* Pemilik dan bentuk modul pelaporan belum dipastikan.
* Verifikasi status transaksi dibahas pada FR-007.
* Penyediaan data tanda terima dibahas pada FR-008.
* Pengiriman catatan donasi ke Kelompok 1 dibahas pada FR-009.
* Pemrosesan pembayaran melalui *payment gateway* dibahas pada FR-006.

### C. Data yang Disediakan

*SRS Draft v0.2 menyebut unsur data yang diperlukan, tetapi belum menetapkan nama field basis data, tipe data, format, dan aturan validasi final. Tabel berikut merupakan daftar kebutuhan data untuk divalidasi, bukan rancangan skema basis data final.*

| No. | Elemen Data | Keterangan / Validasi Awal | Status |
| :--- | :--- | :--- | :--- |
| 1 | **Referensi transaksi** | Harus dapat digunakan untuk menelusuri dan mencocokkan transaksi antarsubsistem. | Format dan aturan keunikan perlu dikonfirmasi. |
| 2 | **Referensi gateway** | Mengacu pada referensi yang diberikan Payment Gateway Artivisi. | Nama dan format field perlu dikonfirmasi. |
| 3 | **Nominal** | Sesuai hasil penagihan/pembayaran. | Format dan kewajiban field perlu dikonfirmasi. |
| 4 | **Waktu transaksi** | Mengacu pada waktu hasil penagihan/pembayaran. | Format, zona waktu, dan jenis waktu perlu dikonfirmasi. |
| 5 | **Status transaksi** | Sesuai hasil verifikasi; status sukses, gagal, dan pending dibedakan. | Daftar status final dan pemetaan status perlu dikonfirmasi (OQ-007). |
| 6 | **Referensi pencocokan** | Mendukung proses pencocokan yang dilakukan Kelompok 5. | Bentuk dan sumber referensi perlu dikonfirmasi. |
| 7 | **Status pengiriman data** | Menunjukkan apakah data terkirim, gagal, atau belum lengkap. | Nilai status dan cara pencatatannya perlu dikonfirmasi. |

> *Tipe data untuk seluruh elemen di atas belum ditentukan dalam SRS Draft v0.2.*

### D. Gambaran UI / Pertukaran Data

*FR-010 merupakan fungsi pertukaran data antarsubsistem, bukan fitur yang secara langsung digunakan oleh donatur. Karena itu, gambaran berikut adalah sketsa tekstual untuk menjelaskan elemen data dan catatan pertukaran, bukan desain UI final.*

#### D.1 Contoh susunan data hasil penagihan

| Elemen | Contoh Isi |
| :--- | :--- |
| **Referensi transaksi** | `[referensi transaksi]` |
| **Referensi gateway** | `[referensi gateway]` |
| **Nominal** | `[nominal]` |
| **Waktu transaksi** | `[waktu transaksi]` |
| **Status transaksi** | `[sukses / gagal / pending — daftar final perlu dikonfirmasi]` |
| **Referensi pencocokan** | `[referensi pencocokan]` |

#### D.2 Contoh catatan pertukaran data

| Elemen | Contoh Isi |
| :--- | :--- |
| **Referensi transaksi** | `[referensi transaksi]` |
| **Tujuan data** | `[Kelompok 5 / modul pelaporan]` |
| **Status pengiriman** | `[terkirim / gagal / belum lengkap — nilai final perlu dikonfirmasi]` |

> *Skema, kanal, autentikasi, dan jadwal pertukaran harus disepakati dengan Kelompok 5 dan pemilik modul pelaporan. Arahan tampilan navy blue dan putih pada NFR-006 berlaku untuk antarmuka pengguna; ketentuan tersebut tidak otomatis menentukan tampilan atau format pertukaran data antarsubsistem.*

### E. Non-Functional Requirement Terkait

| Aspek | Kebutuhan | Acuan dan Catatan |
| :--- | :--- | :--- |
| **Keamanan** | Data donatur dan transaksi dilindungi sesuai kebijakan yang disetujui. Data yang disediakan dibatasi pada data yang disepakati dalam kontrak. | NFR-001; kebijakan akses, retensi, dan detail perlindungan perlu dikonfirmasi (OQ-013). |
| **Keandalan status** | Status yang disediakan harus sesuai hasil verifikasi. Status gagal atau pending tidak dinyatakan berhasil. | NFR-002 dan ALT-02. |
| **Integrasi** | Pertukaran data dilakukan menggunakan kontrak yang disepakati dan tidak melalui akses langsung ke basis data kelompok lain. | NFR-003; kontrak integrasi belum final. |
| **Keterlacakan** | Data transaksi memiliki referensi yang memungkinkan pencocokan antarsubsistem. | NFR-005; format referensi perlu disepakati. |
| **Pemulihan kegagalan integrasi** | Kegagalan pertukaran dapat ditelusuri dan data dipertahankan untuk sinkronisasi ulang. | NFR-007 dan ALT-05; target pemulihan, logging, retry, dan monitoring perlu dikonfirmasi. |
| **Kinerja** | Data disediakan sesuai jadwal atau frekuensi yang disepakati. | Target waktu respons, volume transaksi, dan ketersediaan belum ditetapkan (OQ-014). |

### F. Kriteria Penerimaan

*FR-010 dapat dinyatakan memenuhi kebutuhan apabila kondisi berikut dapat dibuktikan setelah kontrak data disepakati:*

* [ ] Sistem dapat menyiapkan data hasil penagihan/pembayaran yang sekurang-kurangnya mencakup referensi transaksi, nominal, waktu, dan status terverifikasi.
* [ ] Data dapat ditelusuri menggunakan referensi yang disepakati dan status yang disediakan sesuai hasil verifikasi.
* [ ] Data dikirimkan atau disediakan kepada tujuan yang disepakati sesuai format dan jadwal dalam kontrak data.
* [ ] Jika pertukaran gagal atau data belum lengkap, sistem mencatat kondisi tersebut dan tidak menandai data sebagai berhasil terkirim atau terkonfirmasi.
* [ ] Data transaksi tetap dipertahankan agar dapat digunakan untuk sinkronisasi ulang ketika pengiriman gagal.

> *Kriteria penerimaan ini merupakan kriteria awal berdasarkan SRS Draft v0.2. Pengujian final memerlukan kesepakatan mengenai skema data, status, kanal, frekuensi, dan mekanisme sinkronisasi.*

### G. Hal yang Masih Perlu Dikonfirmasi

| No. | Pertanyaan Klarifikasi | Acuan |
| :--- | :--- | :--- |
| 1 | Data apa saja yang wajib diterima Kelompok 5 untuk rekonsiliasi, dan bagaimana status gagal atau pending disampaikan? | OQ-007 |
| 2 | Apakah pelaporan dilakukan oleh Kelompok 5, modul laporan terpisah, atau keduanya? Siapa pemilik masing-masing proses? | OQ-010 |
| 3 | Apa tujuan, isi, dan penerima laporan? Apakah data pelaporan disalurkan melalui Kelompok 5 atau langsung ke modul pelaporan? | Perlu keputusan pihak terkait |
| 4 | Apa skema data, kanal pertukaran (API atau mekanisme lain), serta metode autentikasi yang digunakan? | Kontrak integrasi |
| 5 | Kapan pertukaran data dilakukan: setiap transaksi, terjadwal, atau berdasarkan permintaan? | Frekuensi pertukaran |
| 6 | Apa daftar status final dan bagaimana perubahan status, misalnya pending menjadi sukses, dikirimkan setelah data pertama kali disediakan? | OQ-007 |
| 7 | Siapa yang menangani kegagalan pertukaran dan sinkronisasi ulang? Bagaimana mencegah data terkirim ganda? | ALT-05; FR-015 |
| 8 | Apakah donasi melalui tautan pembayaran satu kali (FR-014) juga termasuk data yang disediakan oleh FR-010? | Batas cakupan |
| 9 | Apakah data rekonsiliasi, tanda terima (FR-008), dan catatan donasi untuk Kelompok 1 (FR-009) dikirim dalam satu kejadian atau terpisah? | Integrasi antarmodul |
| 10 | Bagaimana aturan akses, retensi, dan kepemilikan data? | OQ-013 |
| 11 | Berapa target waktu, volume transaksi, dan tingkat ketersediaan yang diharapkan? | OQ-014 |

### H. Ringkasan untuk Presentasi

* FR-010 menjelaskan bagaimana sistem menyediakan data hasil penagihan/pembayaran untuk kebutuhan rekonsiliasi dan pelaporan. Setelah status transaksi diverifikasi melalui FR-007, sistem menyiapkan referensi transaksi, nominal, waktu, dan status, kemudian mengirimkan atau menyediakan data tersebut kepada Kelompok 5 dan/atau modul pelaporan sesuai kontrak data. Jika pengiriman gagal atau data belum lengkap, kondisi dicatat dan data tidak dianggap berhasil terkirim; data tetap dipertahankan untuk sinkronisasi ulang.
* FR-010 tidak melakukan rekonsiliasi mutasi rekening atau *settlement* karena hal tersebut merupakan tanggung jawab Kelompok 5. FR-010 juga tidak menggantikan proses verifikasi transaksi (FR-007), penyediaan tanda terima (FR-008), pengiriman catatan donasi ke Kelompok 1 (FR-009), maupun pemrosesan pembayaran melalui gateway (FR-006).
* *Dasar penyusunan:* SRS Draft v0.2, khususnya FR-010 Bab 4, alur konseptual Bab 3.1, hubungan subsistem dengan Kelompok 5 dan modul pelaporan pada Bab 2.3, ALT-02 dan ALT-05 Bab 3.2, Bab 6, serta NFR-001, NFR-002, NFR-003, NFR-005, NFR-007, OQ-007, OQ-010, OQ-013, dan OQ-014.

### I. Catatan Status Dokumen

Dokumen ini merupakan versi finalisasi penulisan FR-010 berdasarkan informasi yang tersedia pada SRS Draft v0.2 dan dokumen FR-010 awal. Dokumen belum dapat dianggap sebagai persetujuan final kebutuhan oleh klien karena pertanyaan klarifikasi pada Bagian G belum seluruhnya dijawab. Setelah keputusan diperoleh, bagian terkait perlu diperbarui dan divalidasi bersama pihak yang bertanggung jawab.

| Disusun oleh | Ditinjau oleh | Disetujui oleh |
| :--- | :--- | :--- |
| **Tim/Analis Kebutuhan**<br>Nama: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_<br>Tanggal: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | <br>Nama: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_<br>Peran: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_<br>Tanggal: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | <br>Nama: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_<br>Jabatan: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_<br>Tanggal: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |