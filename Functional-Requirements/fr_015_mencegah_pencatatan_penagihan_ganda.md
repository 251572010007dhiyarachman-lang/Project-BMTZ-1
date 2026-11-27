# FUNCTIONAL REQUIREMENT

## FR-015 — MENCEGAH PENCATATAN/PENAGIHAN GANDA

**Sistem Donasi Berulang dan Kanal Pembayaran Digital**

### Riwayat dan Status Dokumen

| Atribut | Keterangan |
| :--- | :--- |
| **ID / Nama** | FR-015 — Mencegah Pencatatan/Penagihan Ganda |
| **Versi sumber** | Draft Awal v0.1 |
| **Versi dokumen** | 1.0 |
| **Acuan** | SRS Draft v0.2, tanggal 26 Oktober 2026 |
| **Status** | Rumusan dan struktur kebutuhan telah difinalisasi berdasarkan materi yang tersedia. Strategi idempotensi, kontrak API, dan parameter operasional yang belum tersedia tetap ditandai perlu konfirmasi. |

> *Catatan: “Final” pada dokumen ini berarti finalisasi rumusan kebutuhan berdasarkan sumber yang diberikan, bukan pernyataan bahwa seluruh rancangan teknis atau kontrak integrasi telah disetujui.*

### 1. Identitas Kebutuhan

| Elemen | Uraian |
| :--- | :--- |
| **ID kebutuhan** | FR-015 |
| **Nama** | Mencegah Pencatatan/Penagihan Ganda |
| **Aktor utama** | Sistem; Payment Gateway Artivisi, kelompok 1, kelompok 5, dan modul tanda terima sebagai pihak yang bertukar data |
| **Interaksi donatur** | Tidak ada interaksi langsung; FR-015 berjalan di balik proses lain. |
| **Tujuan** | Memastikan permintaan atau hasil transaksi yang diterima lebih dari sekali, atau proses terjadwal yang berjalan ulang, tidak menghasilkan pencatatan atau penagihan ganda. |
| **Prioritas** | Belum ditentukan dalam SRS. |
| **Pemicu** | Permintaan atau hasil transaksi diterima lebih dari sekali, atau scheduler berjalan ulang. |
| **Kondisi awal** | Referensi unik dan strategi idempotensi telah disepakati. |

### 2. Deskripsi Kebutuhan Fungsional

Sistem harus menggunakan kunci idempotensi atau referensi transaksi sesuai kontrak yang disepakati ketika permintaan atau hasil transaksi diterima lebih dari sekali, atau ketika proses terjadwal (*scheduler*) berjalan ulang. Pemrosesan ulang tidak boleh menghasilkan penagihan atau pencatatan donasi ganda.

Apabila sistem mendeteksi referensi duplikat, sistem tidak membuat catatan donasi kedua dan mencatat kejadian duplikat agar dapat ditelusuri. Mekanisme ini berlaku sebagai perlindungan lintas fungsi dan tidak menggantikan proses penagihan, verifikasi transaksi, pengiriman catatan donasi, tanda terima, atau rekonsiliasi yang diatur pada FR lain.

### 3. Ruang Lingkup dan Batasan

**Termasuk dalam ruang lingkup:**
* Mengidentifikasi permintaan atau hasil transaksi yang diterima lebih dari sekali, termasuk pemrosesan ulang oleh *scheduler*.
* Menggunakan kunci idempotensi atau referensi transaksi sesuai kontrak.
* Mencegah pembuatan catatan donasi kedua ketika referensi duplikat terdeteksi.
* Mencatat kejadian duplikat untuk kebutuhan penelusuran.
* Mendukung pengiriman ulang yang aman dan pemulihan proses integrasi sesuai kontrak yang disepakati.

**Batasan:**
* FR-015 bersifat lintas fungsi dan tidak menggantikan FR yang mengatur proses terkait.
* Penagihan melalui gateway dirinci pada FR-006.
* Verifikasi status transaksi dirinci pada FR-007.
* Data tanda terima dirinci pada FR-008.
* Pengiriman catatan donasi ke kelompok 1 dirinci pada FR-009.
* Data rekonsiliasi dan pelaporan dirinci pada FR-010.
* Rancangan teknis idempotensi pada gateway dan API kelompok lain belum disepakati dan tidak ditetapkan oleh FR-015.

### 4. Alur Proses Bisnis

| No. | Langkah | Dasar |
| :--- | :--- | :--- |
| 1 | Permintaan atau hasil transaksi diterima lebih dari sekali, atau scheduler berjalan ulang. | Tertulis di SRS sebagai pemicu; termasuk ALT-08 dan ALT-04. |
| 2 | Sistem memastikan referensi unik dan strategi idempotensi telah disepakati. | Disimpulkan dari kondisi awal SRS. |
| 3 | Sistem menggunakan kunci atau referensi transaksi sesuai kontrak. | Tertulis di SRS. |
| 4 | Pemrosesan ulang tidak menghasilkan penagihan atau pencatatan ganda. | Tertulis di SRS. |

#### 4.1 Alur Alternatif dan Penanganan Kondisi

| Kondisi | Perilaku Sistem | Hal yang Perlu Dikonfirmasi |
| :--- | :--- | :--- |
| **Referensi duplikat terdeteksi** | Sistem tidak membuat catatan donasi kedua dan mencatat kejadian untuk penelusuran. | Respons kepada pemanggil dan format log kejadian. |
| **Status pembayaran pending, terlambat, atau tidak diterima** | Sistem tidak menyatakan berhasil atau gagal tanpa dasar, melakukan pemeriksaan ulang sesuai kontrak, dan menghindari pencatatan ganda. | Status gateway, batas waktu tunggu, dan mekanisme pemeriksaan ulang (OQ-005). |
| **Pengiriman gagal dan perlu dikirim ulang** | Pengiriman ulang ke kelompok 1 harus mencegah duplikasi; referensi disimpan untuk pemulihan. | Mekanisme pemulihan, retry, monitoring, dan penanggung jawab. |
| **Scheduler berjalan ulang** | Pemrosesan ulang tidak menghasilkan penagihan atau pencatatan ganda. | Mekanisme penguncian/koordinasi scheduler dan deteksi tagihan terlewat. |

### 5. Data dan Validasi

*SRS Draft v0.2 belum menetapkan nama field, tipe data, maupun aturan validasi terperinci untuk FR-015. Daftar berikut merupakan data konseptual untuk dibahas, bukan rancangan skema basis data final.*

| Data Konseptual | Tipe Data | Aturan Awal | Status |
| :--- | :--- | :--- | :--- |
| **Referensi transaksi unik** | Belum ditentukan | Unik dan dapat dicocokkan antarsubsistem. | Konfirmasi format dan cakupan; SRS OQ-006. |
| **Kunci idempotensi** | Belum ditentukan | Digunakan agar pemrosesan ulang tidak menghasilkan pencatatan ganda. | Konfirmasi bentuk kunci dan pihak pembuat. |
| **Cakupan penerapan** | Belum ditentukan | Mencakup permintaan tagihan, hasil gateway, dan pengiriman ke kelompok/modul terkait sesuai kontrak. | Konfirmasi titik penerapan. |
| **Status pemrosesan** | Belum ditentukan | Membedakan pemrosesan baru dan pemrosesan ulang. | Konfirmasi daftar status. |
| **Catatan kejadian duplikat** | Belum ditentukan | Kejadian duplikat dicatat untuk penelusuran. | Konfirmasi isi, lokasi penyimpanan, dan pihak yang dapat mengakses. |
| **Masa simpan kunci/referensi** | Belum ditentukan | Belum ditetapkan dalam SRS. | Konfirmasi periode retensi; OQ-013. |

### 6. Rancangan Antarmuka dan Pencatatan

*FR-015 berjalan di balik proses lain dan tidak memiliki tampilan langsung untuk donatur. Sketsa berikut merupakan representasi konseptual informasi teknis yang diperlukan untuk penelusuran, bukan rancangan layar final.*

#### 6.1 Referensi Pemrosesan

| Elemen | Keterangan |
| :--- | :--- |
| **Referensi transaksi unik** | Referensi yang dapat dicocokkan antar-sistem. |
| **Kunci idempotensi** | Kunci untuk mengenali permintaan/pemrosesan ulang; bentuknya perlu dikonfirmasi. |
| **Titik penerapan** | Permintaan tagihan, hasil gateway, pengiriman catatan ke kelompok 1, atau pertukaran data dengan modul lain sesuai kontrak. |
| **Status pemrosesan** | Contoh konseptual: pemrosesan baru atau pemrosesan ulang; nilai final perlu disepakati. |

#### 6.2 Catatan Kejadian Duplikat

| Elemen | Keterangan |
| :--- | :--- |
| **Referensi transaksi** | Referensi yang terdeteksi duplikat. |
| **Waktu kejadian** | Waktu duplikasi terdeteksi. |
| **Sumber** | Contoh sumber: gateway, scheduler, atau pengiriman ulang. |
| **Tindakan sistem** | Catatan donasi kedua tidak dibuat. |
| **Akses** | Pengguna/tim yang dapat melihat catatan perlu ditentukan. |

> *Field, format catatan, lokasi penyimpanan, dan pihak yang melakukan penelusuran harus dikonfirmasi bersama tim teknis, gateway, dan kelompok terkait. Arahan visual navy blue dan putih tidak menjadi persyaratan UI untuk FR ini karena tidak ada antarmuka donatur.*

### 7. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Terkait | Acuan / Catatan |
| :--- | :--- | :--- |
| **Keandalan status** | Pemrosesan ulang tidak membuat transaksi tercatat ganda dan tidak membuat transaksi dianggap berhasil tanpa hasil terverifikasi. | NFR-002; ALT-02. |
| **Keterlacakan** | Kejadian duplikat dicatat; referensi memungkinkan pencocokan antara subsistem donasi, gateway, penerimaan donasi, dan rekonsiliasi. | NFR-005; format referensi perlu disepakati. |
| **Pemulihan kegagalan integrasi** | Kegagalan pertukaran data dapat ditelusuri dan tidak menyebabkan transaksi tercatat ganda. | NFR-007; target pemulihan, logging, retry, dan monitoring perlu diklarifikasi. |
| **Integrasi** | Penggunaan kunci atau referensi mengikuti kontrak API yang disepakati. | NFR-003; kontrak belum final. |
| **Keamanan** | Catatan kejadian dan referensi dilindungi sesuai kebijakan; tidak memuat data kartu atau nomor rekening mentah. | NFR-001; akses dan retensi perlu diklarifikasi (OQ-013). |
| **Kinerja** | Pemeriksaan duplikasi dilakukan dalam waktu wajar tanpa menghambat pemrosesan. | Target waktu respons dan volume belum ditetapkan (OQ-014). |

### 8. Kriteria Penerimaan

* [ ] Pengiriman ulang atau event duplikat tidak menghasilkan transaksi tercatat dua kali dalam pengujian sesuai kontrak.
* [ ] Jika referensi duplikat terdeteksi, sistem tidak membuat catatan donasi kedua.
* [ ] Kejadian duplikat dicatat agar dapat ditelusuri.
* [ ] Pemrosesan ulang oleh scheduler tidak menghasilkan penagihan atau pencatatan ganda.
* [ ] Status pembayaran pending, terlambat, atau belum diterima tidak dinyatakan berhasil atau gagal tanpa dasar hasil terverifikasi.
* [ ] Pengiriman ulang yang sah dapat diproses tanpa menghasilkan pencatatan ganda, sesuai aturan kontrak yang disepakati.

> *Skenario uji terperinci, termasuk bentuk kunci, respons duplikat, dan kontrak API, harus disepakati sebelum kriteria ini dijadikan dasar pengujian integrasi final.*

### 9. Hal yang Perlu Dikonfirmasi

1. Apa referensi unik dan strategi idempotensi yang disepakati, dan siapa yang membuat kuncinya: subsistem ini atau gateway? (SRS Bab 2.3, OQ-006)
2. Pada titik mana kunci diterapkan: permintaan tagihan ke gateway, penerimaan hasil gateway, pengiriman ke kelompok 1, kelompok 5, dan modul tanda terima? (SRS ALT-04, ALT-08)
3. Apakah gateway mendukung idempotensi untuk permintaan tagihan, dan bagaimana callback atau hasil ganda dikirim? (SRS OQ-001, OQ-005)
4. Apa respons kepada pemanggil saat duplikat terdeteksi: ditolak atau dikembalikan hasil pemrosesan sebelumnya?
5. Bagaimana penanganan referensi yang sama tetapi datanya berbeda, misalnya nominal atau status?
6. Berapa lama kunci atau referensi disimpan agar duplikat tetap dapat terdeteksi? (SRS OQ-013)
7. Bagaimana scheduler dicegah berjalan ganda, dan bagaimana tagihan yang terlewat (tidak tertagih) dideteksi serta dipulihkan? (SRS Bab 8, OQ-004)
8. Bagaimana pengiriman ulang yang sah dan koreksi data dibedakan dari duplikat? (SRS OQ-006)
9. Bagaimana kejadian duplikat dicatat, dan siapa yang bertanggung jawab menelusurinya?
10. Siapa yang menyiapkan skenario dan data contoh untuk pengujian duplikasi sesuai kontrak?
11. Berapa target waktu respons dan volume transaksi yang diharapkan? (SRS OQ-014)

### 10. Ketergantungan dan Relasi dengan FR Lain

| Acuan | Hubungan |
| :--- | :--- |
| **FR-006** | Mengatur proses penagihan melalui gateway; FR-015 mencegah penagihan ganda pada alur tersebut. |
| **FR-007** | Mengatur verifikasi status transaksi; FR-015 menjaga pemrosesan ulang hasil gateway agar tidak membuat catatan ganda. |
| **FR-008** | Mengatur data tanda terima; pertukaran data harus terlindungi dari pemrosesan ganda. |
| **FR-009** | Mengatur pengiriman catatan donasi ke kelompok 1; pengiriman ulang harus aman dari duplikasi. |
| **FR-010** | Mengatur data rekonsiliasi dan pelaporan; referensi transaksi membantu pencocokan. |
| **Payment Gateway Artivisi, kelompok 1, kelompok 5, modul tanda terima** | Pihak/sistem yang bertukar data dan perlu menyepakati referensi, idempotensi, retry, serta penanganan kegagalan. |

### 11. Ringkasan

* FR-015 merupakan kebutuhan lintas fungsi untuk mencegah penagihan atau pencatatan donasi ganda ketika permintaan/hasil transaksi diterima lebih dari sekali atau scheduler berjalan ulang. Sistem menggunakan kunci idempotensi atau referensi transaksi sesuai kontrak, tidak membuat catatan donasi kedua ketika duplikat terdeteksi, dan mencatat kejadian agar dapat ditelusuri.
* Risiko duplikasi telah diidentifikasi dalam SRS Draft v0.2, tetapi implementasi teknis—termasuk bentuk kunci, dukungan gateway, titik penerapan, respons terhadap duplikat, retensi referensi, dan mekanisme pemulihan—masih perlu diklarifikasi. FR-015 tidak menggantikan proses yang diatur pada FR-006 sampai FR-010.

### 12. Referensi

* FR-015 — Mencegah Pencatatan/Penagihan Ganda, Draft Awal v0.1 (5 halaman).
* SRS Draft v0.2, tanggal acuan 26 Oktober 2026: Bab 2.3, Bab 3.2 (ALT-02, ALT-04, ALT-08), Bab 4 (FR-015), Bab 8, FR-006, FR-007, FR-008, FR-009, FR-010, NFR-001, NFR-002, NFR-003, NFR-005, NFR-007, OQ-001, OQ-004, OQ-005, OQ-006, OQ-013, dan OQ-014.