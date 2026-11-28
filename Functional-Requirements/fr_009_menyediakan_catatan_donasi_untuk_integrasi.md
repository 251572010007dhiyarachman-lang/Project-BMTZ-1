# BAITULMAL TAZKIA
## SISTEM DONASI BERULANG DAN KANAL PEMBAYARAN DIGITAL

### FUNCTIONAL REQUIREMENT (FR)
# FR-009: MENYEDIAKAN CATATAN DONASI UNTUK INTEGRASI

**Versi:** 1.0 | **Status:** Draft untuk Review dan Validasi Klien | **Tanggal:** 25 November 2026  
**Acuan:** SRS dan BRS Fitur 4 versi 1.0, tanggal acuan 14 November 2026.

---

## A. Identitas Kebutuhan

| Informasi | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-009 |
| **Nama Kebutuhan** | Menyediakan Catatan Donasi untuk Integrasi |
| **Aktor Utama** | Sistem Fitur 4; modul/pihak penerima catatan donasi yang ditetapkan oleh Baitulmal Tazkia (pemilik tujuan perlu dikonfirmasi). |
| **Tujuan** | Menyusun dan mengirim catatan donasi dari transaksi yang telah memenuhi syarat pencatatan, mencatat respons penerimaan, serta menyediakan jejak penelusuran jika integrasi gagal. |
| **Pemicu** | Status transaksi telah diverifikasi berhasil melalui FR-007 dan data memenuhi syarat untuk dicatat sebagai donasi. |
| **Kondisi Awal** | Referensi transaksi tersedia; skema dan kontrak pertukaran data dengan modul penerima telah disepakati. |
| **Prioritas Usulan** | Must Have — usulan, perlu persetujuan Baitulmal Tazkia. |
| **Tingkat Kesulitan Usulan** | 4 — Hard |
| **Status** | Draft untuk review dan validasi; pemilik modul penerima, kontrak API, payload, dan aturan pemulihan belum ditetapkan. |

> **Catatan validasi:** Dokumen FR-009 sebelumnya menyebut Kelompok 1 sebagai penerima. Namun, SRS Fitur 4 versi 1.0 belum menetapkan pemilik tujuan integrasi secara final. Karena itu, dokumen ini menggunakan istilah “modul/pihak penerima yang disepakati” dan tidak menetapkan kelompok tertentu.

---

## B. Deskripsi Functional Requirement

Ketika transaksi telah diverifikasi berhasil melalui FR-007 dan memenuhi syarat pencatatan donasi, sistem Fitur 4 menyiapkan catatan donasi berdasarkan skema data yang disepakati. Sistem kemudian mengirimkan atau menyediakan catatan tersebut kepada modul penerima melalui mekanisme integrasi yang telah disetujui, serta mencatat respons dan status pertukarannya. Jika pengiriman gagal, sistem mencatat kegagalan dan mempertahankan referensi transaksi agar dapat ditelusuri serta dipulihkan. Pengiriman ulang tidak boleh menghasilkan catatan donasi ganda.

### B.1 Batasan Ruang Lingkup
* FR-009 mencakup penyiapan data/payload, pengiriman atau penyediaan data, pencatatan respons, dan keterlacakan kegagalan integrasi.
* Pencatatan penerimaan donasi dan pengelolaan akun pada modul penerima berada di luar tanggung jawab FR-009.
* Verifikasi status transaksi mengacu pada FR-007; penyediaan data tanda terima pada FR-008; penyediaan data rekonsiliasi/pelaporan pada FR-010.
* Pemrosesan pembayaran melalui gateway berada pada FR-006. Pencegahan transaksi/catatan ganda mengikuti kebutuhan FR-015.
* FR-009 tidak menetapkan kelompok penerima, endpoint, metode API, atau skema database sebelum disepakati.

---

## C. Proses Bisnis

| Tahap | Aktor | Aktivitas | Dasar / Catatan |
| :---: | :--- | :--- | :--- |
| **1** | Sistem Fitur 4 | Mengenali transaksi yang telah diverifikasi berhasil melalui FR-007. | Dasar tersedia pada SRS; kriteria pemicu rinci perlu konfirmasi. |
| **2** | Sistem Fitur 4 | Memastikan skema/kontrak pertukaran data yang disepakati tersedia. | Kondisi awal; rincian kontrak belum final. |
| **3** | Sistem Fitur 4 | Menyusun catatan donasi sesuai field dan format yang disepakati. | Dasar tersedia; field wajib dan format perlu konfirmasi. |
| **4** | Sistem Fitur 4 | Mengirimkan atau menyediakan catatan kepada modul penerima yang telah ditetapkan. | Mekanisme, tujuan, autentikasi, dan timeout perlu konfirmasi. |
| **5** | Modul penerima / Sistem Fitur 4 | Menerima respons dan mencatat status pertukaran. | Struktur respons dan pemetaan sukses/gagal perlu konfirmasi. |
| **6** | Sistem Fitur 4 | Jika gagal, mencatat kegagalan dan mempertahankan referensi untuk penelusuran/pemulihan. | Aturan retry, batas percobaan, dan PIC perlu konfirmasi. |
| **7** | Sistem Fitur 4 | Mencegah pengiriman ulang dengan referensi yang sama membentuk catatan ganda. | Selaras FR-015; mekanisme idempotensi perlu konfirmasi. |

### C.1 Alur Alternatif dan Kondisi Khusus
* **Transaksi belum terverifikasi berhasil:** Catatan donasi tidak dikirim; sistem menunggu hasil sah dari FR-007.
* **API atau mekanisme integrasi gagal:** Sistem mencatat kegagalan dan referensi pengiriman; data sumber tetap dipertahankan.
* **Referensi transaksi pernah dikirim:** Sistem tidak membuat pengiriman yang menghasilkan catatan ganda dan mencatat kejadian untuk penelusuran.
* **Catatan yang sudah diterima perlu dikoreksi, dibatalkan, atau direversal:** Mekanisme penanganannya belum ditentukan dan perlu konfirmasi.

---

## D. Data, Tipe Data, dan Validasi

| Elemen Data Usulan | Tujuan / Validasi Awal | Status |
| :--- | :--- | :--- |
| **Referensi donasi/transaksi** | Menghubungkan catatan dengan transaksi sumber; kandidat kunci unik/idempotensi. | Format dan keunikan perlu konfirmasi. |
| **Nominal** | Harus sesuai nominal transaksi yang telah diverifikasi. | Tipe, mata uang, presisi, dan kewajiban field perlu konfirmasi. |
| **Waktu transaksi** | Mengacu pada waktu transaksi yang sah. | Format dan zona waktu perlu konfirmasi. |
| **Identitas donatur** | Hanya data minimum yang disepakati dalam kontrak. | Field yang boleh dikirim perlu konfirmasi. |
| **Peruntukan** | Mengacu pada pilihan peruntukan donasi. | Kode/daftar nilai dan sifat wajib perlu konfirmasi. |
| **Status transaksi** | Konsisten dengan hasil verifikasi FR-007. | Daftar status dan pemetaan perlu konfirmasi. |
| **Respons penerima** | Mencatat hasil penerimaan untuk setiap upaya pertukaran. | Struktur, kode, dan pesan respons perlu konfirmasi. |
| **Status/keterangan kegagalan** | Mendukung penelusuran dan pemulihan integrasi. | Format log, retensi, dan hak akses perlu konfirmasi. |

*Catatan: Daftar di atas merupakan rancangan elemen informasi untuk divalidasi, bukan kontrak API, JSON final, atau rancangan basis data.*

---

## E. Gambaran Integrasi / Mockup Konseptual

*FR-009 merupakan proses pertukaran data antarsubsistem, bukan halaman yang digunakan langsung oleh donatur. Ilustrasi alur:*

| Urutan | Proses |
| :---: | :--- |
| **1** | Transaksi terverifikasi berhasil pada FR-007. |
| **2** | Sistem menyusun catatan donasi berdasarkan skema yang disepakati. |
| **3** | Sistem mengirim/menyediakan catatan kepada modul penerima yang telah ditetapkan. |
| **4** | Sistem mencatat respons dan status pengiriman. |
| **5** | Jika gagal, sistem menyimpan referensi dan status untuk penelusuran/pemulihan. |

> **Contoh elemen payload:** Referensi transaksi, nominal, waktu transaksi, identitas donatur minimum, peruntukan, dan status terverifikasi. Nilai, nama field, serta format hanya ditetapkan setelah kontrak integrasi disepakati.

---

## F. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Terkait | Acuan / Catatan |
| :--- | :--- | :--- |
| **Keamanan dan privasi** | Data donatur/transaksi dibatasi pada informasi yang disetujui dan dilindungi dari akses tidak berwenang. | NFR-001; akses, enkripsi, retensi, dan dasar pemrosesan perlu konfirmasi. |
| **Keandalan status** | Hanya transaksi yang telah terverifikasi berhasil yang menjadi pemicu pengiriman catatan donasi. | NFR-002 dan FR-007. |
| **Integrasi** | Pertukaran data menggunakan kontrak/mekanisme yang disepakati, bukan akses langsung ke basis data modul lain. | NFR-003; endpoint, autentikasi, dan format belum final. |
| **Keterlacakan** | Referensi transaksi dan hasil pengiriman dapat ditelusuri. | NFR-005; format referensi dan korelasi log perlu disepakati. |
| **Pemulihan dan duplikasi** | Kegagalan dapat ditelusuri; pengiriman ulang tidak membentuk catatan ganda. | NFR-007 dan FR-015; aturan retry/idempotensi perlu konfirmasi. |

---

## G. Kriteria Penerimaan
- [ ] Catatan hanya dikirim setelah transaksi memenuhi syarat pencatatan dan statusnya terverifikasi berhasil.
- [ ] Payload mengikuti skema/kontrak yang telah disepakati dengan pemilik modul penerima.
- [ ] Sistem mencatat respons dan status untuk setiap upaya pengiriman.
- [ ] Jika integrasi gagal, sistem mencatat kegagalan dan mempertahankan referensi yang diperlukan untuk penelusuran/pemulihan.
- [ ] Pengiriman ulang dengan referensi yang sama tidak menghasilkan catatan donasi ganda.
- [ ] Transaksi yang belum terverifikasi berhasil tidak dikirim sebagai catatan donasi.

*Catatan: Kriteria ini bersifat awal dan perlu dilengkapi setelah pemilik modul tujuan, kontrak integrasi, serta aturan idempotensi disepakati.*

---

## H. Prioritas dan Tingkat Kesulitan

| Komponen | Usulan | Dasar |
| :--- | :--- | :--- |
| **Prioritas MoSCoW** | Must Have — usulan | Penyediaan data untuk proses bisnis terkait tercantum pada BR-012 dengan prioritas Tinggi; perlu persetujuan Baitulmal Tazkia. |
| **Tingkat Kesulitan** | 4 — Hard | Melibatkan pertukaran data antarsubsistem, kontrak API, validasi payload/respons, keamanan data, pencatatan kegagalan, pemulihan, dan pencegahan duplikasi. |

### Dasar Pertimbangan Penilaian
Skala kesulitan 1–5: **1–2 Easy**, **3 Medium**, dan **4–5 Hard**. FR-009 diusulkan pada tingkat **4 (Hard)** karena bergantung pada integrasi antarsubsistem dan kontrak teknis yang belum final, serta membutuhkan keterlacakan dan pencegahan duplikasi. Prioritas *Must Have* merupakan usulan berdasarkan BR-012 yang berprioritas Tinggi, bukan persetujuan final klien.

---

## I. Hal yang Perlu Dikonfirmasi kepada Klien / Tim Teknis
1. Siapa pemilik modul penerima dan kelompok/pihak mana yang menjadi tujuan integrasi? Dokumen terdahulu menyebut Kelompok 1, tetapi penetapannya belum final.
2. Apa endpoint, metode komunikasi, versi API, autentikasi, dan mekanisme keamanan yang digunakan?
3. Apa field wajib/opsional, tipe data, format tanggal/waktu, mata uang, dan daftar status yang diterima?
4. Referensi unik apa yang digunakan sebagai *correlation ID* atau *idempotency key*?
5. Apa bentuk respons sukses, duplikat, validasi gagal, dan *server error*?
6. Kapan catatan dikirim: segera setelah transaksi berhasil atau melalui proses terjadwal/*batch*?
7. Apakah setiap pembayaran berkala menghasilkan catatan tersendiri? Apakah transaksi dari tautan pembayaran satu kali FR-014 ikut dikirim?
8. Bagaimana aturan *retry*, batas percobaan, monitoring, dan penanggung jawab pemulihan?
9. Bagaimana koreksi, pembatalan, *reversal*, atau perubahan status setelah catatan diterima ditangani?
10. Apakah pertukaran data FR-009 terpisah dari penyediaan tanda terima FR-008 dan data rekonsiliasi/pelaporan FR-010?
11. Bagaimana aturan akses, retensi, audit, dan kepemilikan data donatur yang dipertukarkan?

---

## J. Checklist Konfirmasi Client

| ID & Nama Kebutuhan | Prioritas Usulan | Kesulitan Usulan | Tidak Dibutuhkan / Catatan Client |
| :--- | :--- | :--- | :--- |
| **FR-009 — Menyediakan Catatan Donasi untuk Integrasi** | Must Have — usulan | 4 — Hard | |

*Catatan: Isi kolom terakhir apabila kebutuhan tidak diperlukan atau terdapat catatan/perubahan dari klien. Biarkan kosong jika kebutuhan tetap diperlukan.*

---

## K. Catatan dan Status Dokumen
FR-009 berada setelah verifikasi transaksi pada FR-007. Fungsinya menyediakan catatan donasi kepada modul penerima yang ditetapkan, bukan memproses pembayaran atau mengambil alih pencatatan pada modul penerima. Dokumen ini diselaraskan dengan SRS/BRS Fitur 4 versi 1.0 tanggal 14 November 2026. Pemilik tujuan, skema data, metode integrasi, aturan *retry*, dan idempotensi masih memerlukan validasi.  
**Status:** Draft untuk Review dan Validasi Klien; belum menjadi baseline sebelum disetujui.