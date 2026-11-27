SOFTWARE REQUIREMENTS
SPECIFICATION (SRS)

Sistem Donasi Berulang dan Kanal Pembayaran Digital

Organisasi/Proyek: Baitulmal Tazkia
Fitur: Fitur 4
Versi: 1.0 – Revisi untuk Validasi
Status: Draft Final untuk Review dan Validasi
Tanggal: 14 November 2026

Dokumen kerja – belum menjadi baseline sebelum disetujui pihak berwenang

# Dokumen

| Versi | Tanggal | Perubahan | Status |

| --- | --- | --- | --- |

| 0.1 | 25 Oktober 2026 | Draft awal berdasarkan workbook dan ringkasan rapat | Draft |

| 0.2 | 26 Oktober 2026 | Penambahan alur, kebutuhan fungsional, dan pertukaran data | Review internal |

| 1.0 | 14 November 2026 | Revisi ruang lingkup, aktor, dan hubungan Fitur 4, 6, dan 12 | Untuk validasi |

## Keterangan Status Kebutuhan

| Status | Makna |

| --- | --- |

| [DASAR TERSEDIA] | Kebutuhan memiliki dasar dari dokumen proyek, hasil diskusi, atau alur sementara yang diberikan. |

| [PERLU KLARIFIKASI] | Detail kebutuhan masih harus dikonfirmasi kepada PIC atau pihak terkait. |

| [DI LUAR RUANG LINGKUP] | Fungsi menjadi tanggung jawab fitur lain dan tidak dikerjakan langsung oleh Fitur 4. |

# 1. Pendahuluan

## 1.1 Tujuan Dokumen

Dokumen Software Requirements Specification (SRS) ini menjelaskan kebutuhan perangkat lunak untuk Sistem Donasi Berulang dan Kanal Pembayaran Digital pada Baitulmal Tazkia.

Dokumen ini digunakan sebagai acuan bagi pihak klien, Business Analyst, pengembang, penguji, serta pihak terkait dalam memahami fungsi sistem, alur proses, batas tanggung jawab, kebutuhan fungsional, dan kebutuhan nonfungsional.

## 1.2 Ruang Lingkup Sistem

Sistem Donasi Berulang dan Kanal Pembayaran Digital merupakan bagian dari Fitur 4 yang berfokus pada pengelolaan kesediaan donasi berulang, pengaturan nominal dan jadwal donasi, pemrosesan atau pemantauan pembayaran digital, pencatatan status transaksi, serta penyediaan data transaksi untuk kebutuhan fitur terkait.

Ruang lingkup sistem meliputi:

Menampilkan informasi kampanye yang dapat dipilih oleh donatur.

Menyediakan pilihan donasi berulang.

Mengatur nominal, jadwal, periode, dan peruntukan donasi.

Menyimpan kesediaan donasi dan jadwal donatur.

Mendukung proses pembayaran atau penagihan melalui kanal pembayaran digital sesuai metode yang disetujui.

Memverifikasi dan memperbarui status transaksi.

Mengirimkan pengingat atau pemberitahuan terkait pembayaran sesuai mekanisme yang disepakati.

Mendukung jeda dan pembatalan donasi berulang.

Menyediakan tautan pembayaran satu kali jika fitur tersebut digunakan.

Menyediakan data transaksi yang dibutuhkan untuk integrasi dengan fitur terkait.

Fitur 4 berhubungan dengan Fitur 6 dan Fitur 12 dalam konteks koordinasi sistem. Namun, proses pencatatan donasi luring dan pengelolaan relawan tetap menjadi tanggung jawab fitur masing-masing.

## 1.3 Tujuan Sistem

Tujuan pengembangan sistem ini adalah:

Memudahkan donatur dalam mendaftarkan dan mengelola donasi berulang.

Membantu proses pembayaran donasi melalui kanal digital.

Menyediakan informasi status pembayaran yang akurat.

Mengurangi risiko kesalahan pencatatan dan transaksi ganda.

Menyediakan data transaksi yang dapat digunakan oleh fitur terkait.

Mendukung pengelolaan donasi secara lebih terstruktur dan terdokumentasi.

## 1.4 Istilah dan Singkatan

| Istilah | Pengertian |

| --- | --- |

| SRS | Software Requirements Specification |

| FR | Functional Requirement |

| NFR | Non-Functional Requirement |

| Donatur | Pihak yang memberikan donasi |

| Payment Gateway | Layanan pihak ketiga untuk memproses pembayaran |

| API | Application Programming Interface |

| Transaksi | Catatan aktivitas pembayaran donasi |

| Recurring Donation | Donasi yang dilakukan secara berulang berdasarkan jadwal tertentu |

| Consent | Persetujuan donatur terhadap mekanisme donasi atau pembayaran |

| Webhook | Mekanisme pengiriman informasi status transaksi dari layanan eksternal |

| Retry | Percobaan ulang proses pembayaran atau pengiriman data |

## 1.5 Referensi

Workbook Proyek Sistem Informasi Baitulmal Tazkia – Fitur 4: Donasi Berulang dan Kanal Pembayaran Digital.

Dokumen Fitur 6 – Penerimaan Donasi Luring.

Dokumen Fitur 12 – Relawan dan Operasional Acara.

Ringkasan rapat pengembangan sistem donasi dan CRM.

Dokumentasi Payment Gateway Artivisi, apabila telah tersedia dan disetujui.

Dokumen acuan integrasi antarf fitur.

# 2. Gambaran Umum Sistem

## 2.1 Gambaran Produk

Sistem Donasi Berulang dan Kanal Pembayaran Digital merupakan subsistem yang membantu donatur melakukan pendaftaran donasi berulang serta mengelola proses pembayaran digital.

Sistem menyimpan informasi kesediaan donasi, nominal, jadwal, peruntukan, dan status transaksi. Sistem juga berkomunikasi dengan layanan pembayaran untuk memperoleh informasi hasil pembayaran sesuai mekanisme integrasi yang disepakati.

Sistem tidak boleh menyatakan transaksi berhasil hanya karena donatur telah memulai pembayaran. Status berhasil harus didasarkan pada informasi transaksi yang telah diverifikasi.

## 2.2 Aktor dan Pihak Terkait

| Aktor/Pihak | Tanggung Jawab |

| --- | --- |

| Donatur | Memilih program, menentukan nominal dan jadwal, memberikan persetujuan, serta melakukan pembayaran. |

| Staf Internal Baitulmal Tazkia | Mengelola dan memantau data donasi serta transaksi sesuai hak akses. |

| Sistem Fitur 4 | Mengelola kesediaan donasi berulang, jadwal, status, dan data pembayaran digital. |

| Payment Gateway Artivisi | Memproses pembayaran digital dan memberikan informasi status transaksi sesuai kemampuan layanan. |

| Fitur 6 – Penerimaan Donasi Luring | Mengelola pencatatan donasi yang diterima secara langsung oleh petugas. |

| Fitur 12 – Relawan dan Operasional Acara | Mengelola data relawan, jadwal, penugasan, dan operasional kegiatan. |

## 2.3 Hubungan dan Batas Tanggung Jawab Antarf Fitur

### A. Hubungan Fitur 4 dengan Fitur 6

Fitur 6 menangani penerimaan donasi luring yang dilakukan oleh petugas. Berdasarkan alur sementara yang diberikan, prosesnya adalah:

Petugas menerima donasi uang.

Petugas menginput data donatur dan transaksi.

Data yang dicatat meliputi nama, nomor telepon, jenis donasi, kanal, dan jumlah donasi.

Data transaksi dan kuitansi disimpan secara digital.

Bukti donasi dikirim melalui WhatsApp.

Proses tersebut merupakan alur Fitur 6 dan bukan fungsi utama Fitur 4.

Fitur 4 berfokus pada donasi berulang dan pembayaran digital. Apabila terdapat kebutuhan pertukaran data antara kedua fitur, mekanisme dan format integrasinya harus disepakati terlebih dahulu.

Status integrasi Fitur 4 dan Fitur 6: [PERLU KLARIFIKASI].

### B. Hubungan Fitur 4 dengan Fitur 12

Fitur 12 mengelola relawan dan operasional acara, termasuk pendaftaran relawan, ketersediaan waktu, penyusunan sesi acara, penugasan, dan pencatatan kehadiran.

Hubungan Fitur 4 dan Fitur 12 berada pada koordinasi operasional apabila kegiatan donasi melibatkan petugas atau relawan. Fitur 4 tidak mengambil alih fungsi pengelolaan relawan, jadwal kegiatan, maupun penugasan petugas.

Status integrasi langsung Fitur 4 dan Fitur 12: [PERLU KLARIFIKASI].

## 2.4 Batasan dan Asumsi

Sistem dikembangkan untuk mendukung proses donasi berulang dan kanal pembayaran digital.

Pengelolaan penerimaan donasi luring merupakan tanggung jawab Fitur 6.

Pengelolaan relawan dan operasional acara merupakan tanggung jawab Fitur 12.

Pemrosesan pembayaran digital dilakukan melalui layanan Payment Gateway Artivisi sesuai metode yang didukung.

Sistem hanya dapat menggunakan metode pembayaran yang telah dikonfirmasi ketersediaannya.

Pertukaran data antarf fitur harus menggunakan mekanisme integrasi yang disepakati.

Detail teknis API, autentikasi, payload, dan penanganan kesalahan masih perlu dikonfirmasi.

Mekanisme pembayaran berulang, apakah melalui pengingat pembayaran manual atau autodebit, harus ditetapkan oleh pihak terkait.

# 3. Alur Proses Sistem

## 3.1 Alur Utama Donasi Berulang

Donatur membuka halaman informasi kampanye.

Sistem menampilkan informasi program donasi.

Donatur memilih opsi donasi berulang apabila tersedia.

Donatur memasukkan nominal donasi, jadwal, periode, dan peruntukan.

Sistem memvalidasi data yang dimasukkan.

Donatur memberikan persetujuan terhadap kesediaan donasi sesuai ketentuan.

Sistem menyimpan data kesediaan donasi dan jadwal.

Sistem menjalankan mekanisme pembayaran sesuai metode yang telah disepakati.

Payment Gateway Artivisi memproses pembayaran apabila metode tersebut digunakan.

Sistem menerima informasi status pembayaran.

Sistem memverifikasi status transaksi dan memperbarui catatan transaksi.

Sistem menyediakan data transaksi yang telah terverifikasi untuk kebutuhan fitur terkait.

Donatur dapat melihat informasi status donasi sesuai fasilitas yang tersedia.

Catatan: Mekanisme pengingat pembayaran manual dan penagihan otomatis/autodebit masih harus dikonfirmasi. Keduanya tidak dianggap sebagai satu mekanisme yang sama.

## 3.2 Alur Alternatif Pembayaran

### A. Pembayaran Berhasil

Donatur menyelesaikan pembayaran.

Payment Gateway mengirimkan status transaksi.

Sistem memverifikasi informasi pembayaran.

Sistem memperbarui status transaksi menjadi berhasil.

Sistem menyimpan referensi dan waktu transaksi.

### B. Pembayaran Gagal

Proses pembayaran tidak berhasil.

Sistem menerima atau memperoleh informasi kegagalan.

Sistem memperbarui status transaksi menjadi gagal.

Sistem menampilkan informasi kegagalan kepada donatur atau staf sesuai hak akses.

Proses pembayaran berikutnya mengikuti aturan yang telah disepakati.

### C. Pembayaran Pending atau Timeout

Sistem menerima status pending atau tidak memperoleh respons final.

Sistem tidak langsung menganggap transaksi berhasil atau gagal.

Sistem menunggu atau melakukan pemeriksaan status kembali sesuai mekanisme yang disepakati.

Sistem memperbarui status setelah memperoleh hasil yang dapat diverifikasi.

## 3.3 Alur Penerimaan Donasi Luring sebagai Konteks Integrasi

Alur sementara Fitur 6 yang menjadi konteks koordinasi adalah:

Petugas menerima donasi uang
↓
Input data donatur dan transaksi
↓
Data dan kuitansi disimpan secara digital
↓
Bukti donasi dikirim melalui WhatsApp

Data yang dicatat pada proses tersebut meliputi nama donatur, nomor telepon, jenis donasi, kanal penerimaan, dan jumlah donasi.

Alur ini tidak dimasukkan sebagai alur utama Fitur 4 karena pencatatan penerimaan donasi luring merupakan tanggung jawab Fitur 6. Apabila transaksi dari Fitur 6 perlu digunakan bersama dengan data Fitur 4, mekanisme pertukaran data harus ditentukan melalui kesepakatan antarf fitur.

## 3.4 Diagram Alur Konseptual Fitur 4

Donatur
   |
   v
Membuka Halaman Kampanye
   |
   v
Memilih Donasi Berulang
   |
   v
Mengisi Nominal, Jadwal,
Periode, dan Peruntukan
   |
   v
Validasi Data dan Persetujuan
   |
   v
Menyimpan Kesediaan Donasi
   |
   v
Proses Pembayaran
   |
   v
Payment Gateway Artivisi
   |
   v
Penerimaan Status Transaksi
   |
   v
Verifikasi Status Pembayaran
   |
   v
Memperbarui Data Transaksi
   |
   v
Menyediakan Data untuk
Fitur Terkait

# 4. Kebutuhan Fungsional (Functional Requirements)

| ID | Nama Kebutuhan | Deskripsi |

| --- | --- | --- |

| FR-001 | Menampilkan Halaman Kampanye | Sistem menyediakan halaman informasi kampanye yang dapat diakses donatur. |

| FR-002 | Memilih Donasi Berulang | Sistem menyediakan pilihan donasi berulang pada program yang mendukung fitur tersebut. |

| FR-003 | Mengatur Nominal, Jadwal, dan Peruntukan | Sistem memungkinkan donatur menentukan nominal, jadwal, periode, dan peruntukan donasi. |

| FR-004 | Menyimpan Kesediaan Donasi dan Jadwal | Sistem menyimpan informasi kesediaan donasi, persetujuan, dan jadwal donatur. |

| FR-005 | Mengirim Pengingat Pembayaran | Sistem menyediakan mekanisme pengingat pembayaran sesuai jadwal dan kanal komunikasi yang disetujui. |

| FR-006 | Memproses Pembayaran melalui Gateway | Sistem menghubungkan proses pembayaran dengan Payment Gateway Artivisi sesuai metode yang didukung. |

| FR-007 | Memverifikasi dan Memperbarui Status Transaksi | Sistem menerima dan memverifikasi status transaksi sebelum memperbarui catatan pembayaran. |

| FR-008 | Menyediakan Data untuk Tanda Terima | Sistem menyediakan informasi transaksi terverifikasi yang diperlukan untuk proses tanda terima sesuai kesepakatan pemilik modul. |

| FR-009 | Menyediakan Catatan Donasi untuk Integrasi | Sistem menyediakan catatan transaksi donasi untuk sistem penerima yang telah disepakati. Pihak penerima dan kontrak integrasi masih perlu dikonfirmasi. |

| FR-010 | Menyediakan Data Transaksi untuk Pelaporan dan Rekonsiliasi | Sistem menyediakan data transaksi yang diperlukan oleh pihak terkait sesuai batas akses dan kontrak data yang disepakati. |

| FR-011 | Menjeda Donasi Berulang | Sistem memungkinkan donatur atau pihak berwenang menjeda kesediaan donasi sesuai aturan yang disepakati. |

| FR-012 | Membatalkan Donasi Berulang | Sistem memungkinkan pembatalan kesediaan donasi sesuai ketentuan yang berlaku. |

| FR-013 | Mengirim Pemberitahuan Status Donasi | Sistem menyediakan informasi atau pemberitahuan terkait status donasi dan pembayaran sesuai mekanisme komunikasi yang disetujui. |

| FR-014 | Membuat Tautan Pembayaran Satu Kali | Sistem menyediakan pembuatan tautan pembayaran satu kali apabila fungsi tersebut disetujui dan didukung gateway. |

| FR-015 | Mencegah Transaksi Ganda | Sistem menggunakan referensi transaksi atau mekanisme idempotensi agar pemrosesan ulang tidak menghasilkan pencatatan transaksi ganda. |

## 4.1 Keterangan Kebutuhan Fungsional

FR-001 sampai FR-004 merupakan fungsi utama dalam pendaftaran donasi berulang.

FR-005 dan FR-006 bergantung pada keputusan mekanisme pembayaran yang digunakan.

FR-007 diperlukan untuk menjaga keakuratan status transaksi.

FR-008 sampai FR-010 berhubungan dengan penyediaan data bagi kebutuhan proses lain dan memerlukan kesepakatan pemilik layanan.

FR-011 dan FR-012 berkaitan dengan pengelolaan status kesediaan donasi.

FR-013 berkaitan dengan pemberitahuan kepada donatur.

FR-014 bergantung pada dukungan layanan Payment Gateway.

FR-015 diperlukan untuk mengurangi risiko pencatatan atau penagihan ganda.

# 5. Kebutuhan Nonfungsional (Non-Functional Requirements)

| ID | Aspek | Kebutuhan |

| --- | --- | --- |

| NFR-001 | Keamanan | Sistem harus melindungi data donatur dan transaksi dari akses yang tidak berwenang. |

| NFR-002 | Keandalan | Sistem tidak boleh menyatakan transaksi berhasil tanpa status pembayaran yang telah diverifikasi. |

| NFR-003 | Integrasi | Sistem harus mendukung pertukaran data melalui API atau mekanisme integrasi yang disepakati. |

| NFR-004 | Kemudahan Penggunaan | Antarmuka sistem harus mudah dipahami dan digunakan oleh donatur maupun staf. |

| NFR-005 | Konsistensi Data | Data transaksi harus memiliki referensi yang dapat digunakan untuk penelusuran dan pencocokan. |

| NFR-006 | Tampilan | Antarmuka mengikuti arahan identitas visual awal Baitulmal Tazkia, yaitu navy blue dan putih, dengan penyesuaian terhadap identitas resmi organisasi. |

| NFR-007 | Pemulihan Kegagalan | Sistem harus dapat mencatat dan menelusuri kegagalan integrasi serta mencegah kesalahan pencatatan transaksi akibat pengiriman ulang. |

## 5.1 Keamanan dan Hak Akses

Data donatur hanya dapat diakses oleh pihak yang memiliki hak akses.

Informasi transaksi harus dijaga kerahasiaannya.

Sistem harus membedakan hak akses donatur dan staf internal.

Informasi pembayaran sensitif tidak boleh disimpan tanpa kebutuhan dan dasar keamanan yang disetujui.

# 6. Batas Ruang Lingkup Sistem

| Kategori | Ruang Lingkup |

| --- | --- |

| Masuk Ruang Lingkup Fitur 4 | Pendaftaran donasi berulang, pengaturan nominal dan jadwal, penyimpanan kesediaan donasi, proses pembayaran digital, verifikasi status transaksi, pengingat, jeda dan pembatalan donasi, serta penyediaan data transaksi. |

| Perlu Konfirmasi | Metode pembayaran berulang, pengingat manual atau autodebit, aturan retry, status pending, detail API, pengiriman tanda terima, tautan pembayaran satu kali, dan integrasi dengan fitur lain. |

| Di Luar Ruang Lingkup Fitur 4 | Pencatatan penerimaan donasi luring oleh petugas, pengelolaan antrean donasi luring, pengelolaan data relawan, penyusunan jadwal acara, dan penugasan relawan. |

# 7. Kebutuhan Integrasi

## 7.1 Integrasi dengan Payment Gateway Artivisi

Data yang mungkin dipertukarkan meliputi referensi transaksi, nominal pembayaran, informasi pembayaran yang diperlukan, status transaksi, waktu transaksi, dan informasi respons pembayaran.

Detail metode pembayaran, autentikasi, callback/webhook, kode respons, timeout, dan retry harus disepakati dengan penyedia gateway.

## 7.2 Integrasi dengan Fitur 6 – Penerimaan Donasi Luring

Fitur 6 menangani pencatatan donasi yang diterima petugas secara langsung. Sistem Fitur 6 mencatat identitas donatur, jenis donasi, kanal, dan nominal, menyimpan data serta kuitansi secara digital, kemudian mengirim bukti donasi melalui WhatsApp.

Fitur 4 tidak mengambil alih proses pencatatan tersebut.

Apabila dibutuhkan pertukaran data antara Fitur 4 dan Fitur 6, hal yang perlu ditentukan meliputi jenis data yang dipertukarkan, tujuan pertukaran data, sistem sumber data utama, mekanisme integrasi, waktu sinkronisasi, serta penanganan data duplikat atau gagal dikirim.

Status: [PERLU KLARIFIKASI].

## 7.3 Integrasi dengan Fitur 12 – Relawan dan Operasional Acara

Fitur 12 mengelola data relawan dan operasional acara. Fitur 4 tidak mengelola akun relawan, jadwal kegiatan, maupun penugasan relawan.

Jika kegiatan donasi membutuhkan keterlibatan relawan atau petugas acara, koordinasi dapat dilakukan dengan Fitur 12. Detail pertukaran data atau integrasi langsung belum ditentukan.

Status: [PERLU KLARIFIKASI].

# 8. Risiko dan Kendala

| No. | Risiko/Kendala | Dampak |

| --- | --- | --- |

| 1 | Belum adanya keputusan final mengenai pengingat manual atau autodebit | Alur pembayaran dapat berubah. |

| 2 | Dukungan metode pembayaran gateway belum dikonfirmasi | Beberapa metode pembayaran mungkin tidak dapat digunakan. |

| 3 | Status transaksi terlambat diterima | Informasi pembayaran dapat tidak akurat. |

| 4 | Integrasi antarf fitur belum memiliki kontrak final | Pertukaran data dapat mengalami kegagalan. |

| 5 | Pengiriman ulang transaksi tanpa mekanisme idempotensi | Berpotensi menghasilkan pencatatan ganda. |

| 6 | Belum jelasnya pemilik modul tanda terima | Dapat menimbulkan duplikasi tanggung jawab. |

| 7 | Belum ditetapkannya mekanisme integrasi Fitur 4 dan Fitur 6 | Data donasi digital dan luring berpotensi tidak sinkron jika integrasi nantinya dibutuhkan. |

# 9. Pertanyaan Terbuka untuk Validasi

| ID | Pertanyaan | Pihak yang Perlu Mengonfirmasi |

| --- | --- | --- |

| OQ-001 | Apakah donasi berulang menggunakan pengingat pembayaran manual, autodebit, atau keduanya? | PIC/Klien |

| OQ-002 | Metode pembayaran apa saja yang didukung untuk donasi berulang? | Payment Gateway Artivisi |

| OQ-003 | Bagaimana jadwal dan frekuensi pengingat pembayaran ditentukan? | PIC/Klien |

| OQ-004 | Bagaimana aturan percobaan ulang jika pembayaran gagal? | PIC/Klien dan Artivisi |

| OQ-005 | Bagaimana sistem menangani status pending atau timeout? | Artivisi |

| OQ-006 | Apakah Fitur 4 dan Fitur 6 perlu bertukar data transaksi? Jika ya, data apa saja yang dibutuhkan? | PIC Fitur 4 dan Fitur 6 |

| OQ-007 | Apakah kegiatan donasi memerlukan pertukaran data dengan Fitur 12? | PIC Fitur 4 dan Fitur 12 |

| OQ-008 | Siapa yang bertanggung jawab atas pembuatan dan pengiriman tanda terima? | PIC/Klien |

| OQ-009 | Apakah tautan pembayaran satu kali digunakan pada versi sistem ini? | PIC/Klien |

| OQ-010 | Bagaimana aturan jeda dan pembatalan donasi jika pembayaran sedang diproses? | PIC/Klien dan Artivisi |

| OQ-011 | Bagaimana mekanisme penyimpanan dan perlindungan data donatur? | PIC/Klien dan Tim Teknis |

| OQ-012 | Apa format data, autentikasi, dan mekanisme pertukaran data yang digunakan antarf fitur? | PIC dan Tim Teknis terkait |

# 10. Kriteria Penerimaan Sistem

Sistem dapat dinyatakan memenuhi kebutuhan awal apabila:

Donatur dapat mengakses informasi kampanye.

Donatur dapat memilih donasi berulang pada program yang mendukung.

Donatur dapat mengisi nominal, jadwal, periode, dan peruntukan donasi.

Sistem dapat menyimpan kesediaan donasi dan jadwal.

Sistem dapat memproses atau memantau pembayaran sesuai metode yang telah disepakati.

Sistem dapat memperbarui status transaksi berdasarkan informasi yang terverifikasi.

Sistem dapat menangani status pembayaran berhasil, gagal, dan pending.

Sistem dapat menyediakan informasi transaksi yang dibutuhkan untuk integrasi sesuai kesepakatan.

Sistem dapat mengelola jeda dan pembatalan donasi sesuai aturan.

Sistem dapat mencegah pencatatan transaksi ganda berdasarkan mekanisme yang disepakati.

# 11. Penutup

Dokumen SRS Sistem Donasi Berulang dan Kanal Pembayaran Digital ini disusun sebagai acuan kebutuhan perangkat lunak untuk Fitur 4 pada proyek Sistem Informasi Baitulmal Tazkia.

Dokumen telah memperjelas ruang lingkup Fitur 4 serta hubungannya dengan Fitur 6 – Penerimaan Donasi Luring dan Fitur 12 – Relawan dan Operasional Acara.

Alur penerimaan donasi luring yang diberikan menjadi acuan proses Fitur 6 dan tidak dianggap sebagai pengganti alur utama Fitur 4.

Beberapa detail teknis dan keputusan bisnis masih memerlukan validasi dari PIC, klien, dan pihak terkait. Oleh karena itu, dokumen ini berstatus draft final untuk validasi dan baru dapat ditetapkan sebagai baseline setelah memperoleh persetujuan pihak yang berwenang.
