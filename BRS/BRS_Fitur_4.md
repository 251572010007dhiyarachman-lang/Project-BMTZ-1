BUSINESS REQUIREMENTS SPECIFICATION (BRS)

Sistem Donasi Berulang dan Kanal Pembayaran Digital

Baitulmal Tazkia – Fitur 4

| Informasi Dokumen | Keterangan |

| --- | --- |

| Nama Sistem | Sistem Donasi Berulang dan Kanal Pembayaran Digital |

| Organisasi | Baitulmal Tazkia |

| Fitur | Fitur 4 |

| Versi | 1.0 |

| Status | Draft Final untuk Review dan Validasi |

| Tanggal | 14 November 2026 |

# 1. PENDAHULUAN

## 1.1 Latar Belakang

Baitulmal Tazkia membutuhkan sistem yang dapat mendukung pengelolaan donasi secara lebih terstruktur, khususnya untuk donasi berulang dan penggunaan kanal pembayaran digital.

Dalam proses donasi, donatur perlu memperoleh kemudahan untuk menentukan nominal, jadwal, periode, dan peruntukan donasi. Selain itu, proses pembayaran perlu didukung dengan pencatatan transaksi dan informasi status pembayaran yang jelas.

Oleh karena itu, Fitur 4 – Donasi Berulang dan Kanal Pembayaran Digital dikembangkan untuk membantu proses pendaftaran donasi berulang, pengelolaan kesediaan donasi, pemrosesan pembayaran digital, serta penyediaan informasi transaksi bagi kebutuhan organisasi.

## 1.2 Tujuan Dokumen

Dokumen Business Requirements Specification (BRS) ini bertujuan untuk:

Menjelaskan kebutuhan bisnis dalam pengelolaan donasi berulang dan pembayaran digital.

Mengidentifikasi permasalahan dan peluang perbaikan proses bisnis.

Menentukan tujuan dan ruang lingkup bisnis Fitur 4.

Mengidentifikasi stakeholder yang terlibat.

Menjelaskan proses bisnis yang diharapkan.

Menetapkan kebutuhan bisnis dan aturan bisnis.

Menentukan kriteria keberhasilan pengembangan fitur.

Menjadi acuan dalam penyusunan dan validasi dokumen SRS.

## 1.3 Ruang Lingkup Bisnis

Ruang lingkup bisnis Fitur 4 meliputi:

Pengelolaan pendaftaran donasi berulang.

Pengaturan nominal dan jadwal donasi.

Pencatatan kesediaan dan persetujuan donatur.

Dukungan pembayaran melalui kanal digital.

Pemantauan dan pencatatan status pembayaran.

Pengiriman pengingat atau pemberitahuan pembayaran sesuai mekanisme yang disepakati.

Pengelolaan jeda dan pembatalan donasi berulang.

Penyediaan informasi transaksi untuk kebutuhan administrasi dan fitur terkait.

Fitur ini tidak mencakup pengelolaan utama penerimaan donasi luring oleh petugas maupun pengelolaan relawan dan operasional acara.

# 2. GAMBARAN UMUM BISNIS

## 2.1 Kondisi Bisnis Saat Ini

Pengelolaan donasi membutuhkan proses pencatatan yang terstruktur agar informasi donatur, kesediaan donasi, nominal, jadwal, dan status pembayaran dapat dipantau dengan baik.

Dalam pengembangan sistem Baitulmal Tazkia, kebutuhan pengelolaan donasi tidak hanya mencakup transaksi satu kali, tetapi juga donasi yang dilakukan secara berulang berdasarkan kesediaan donatur.

Proses pembayaran digital juga memerlukan dukungan layanan pembayaran eksternal agar transaksi dapat diproses dan statusnya dapat diketahui.

Detail kondisi operasional saat ini, termasuk metode pencatatan yang telah berjalan, tingkat penggunaan pembayaran digital, serta kendala aktual, masih perlu divalidasi kepada pihak Baitulmal Tazkia.

## 2.2 Permasalahan Bisnis

Permasalahan atau kebutuhan bisnis yang menjadi dasar pengembangan Fitur 4 meliputi:

Pengelolaan donasi berulang: Diperlukan mekanisme untuk menyimpan kesediaan donasi dan jadwal donatur.

Pengaturan donasi: Donatur perlu memiliki pilihan untuk menentukan nominal, periode, jadwal, dan peruntukan donasi.

Pemantauan pembayaran: Diperlukan informasi status transaksi yang dapat dipantau dan diverifikasi.

Pencatatan transaksi: Informasi pembayaran perlu disimpan agar dapat ditelusuri.

Komunikasi dengan donatur: Diperlukan pengingat dan pemberitahuan terkait jadwal maupun status pembayaran.

Integrasi pembayaran: Diperlukan dukungan layanan Payment Gateway untuk memproses pembayaran digital.

Konsistensi data: Data transaksi perlu tersedia untuk mendukung proses administrasi, rekonsiliasi, dan pelaporan.

## 2.3 Peluang Perbaikan Bisnis

Pengembangan Fitur 4 diharapkan memberikan peluang perbaikan berupa:

Mempermudah donatur dalam melakukan donasi berulang.

Membantu organisasi mengelola jadwal dan kesediaan donasi.

Meningkatkan keteraturan pencatatan transaksi.

Mempermudah pemantauan status pembayaran.

Mengurangi risiko kesalahan pencatatan dan transaksi ganda.

Mendukung ketersediaan data transaksi untuk proses bisnis terkait.

Meningkatkan kemudahan komunikasi informasi donasi kepada donatur.

# 3. STAKEHOLDER DAN PIHAK TERKAIT

## 3.1 Identifikasi Stakeholder

| Stakeholder | Peran dan Kepentingan |

| --- | --- |

| Donatur | Pihak yang memberikan donasi dan menggunakan fasilitas donasi berulang serta pembayaran digital. |

| Staf Internal Baitulmal Tazkia | Pihak yang memantau dan mengelola informasi donasi serta transaksi sesuai kewenangan. |

| Manajemen Baitulmal Tazkia | Pihak yang berkepentingan terhadap kelancaran proses donasi dan ketersediaan informasi transaksi. |

| Tim Pengembang Sistem | Pihak yang menganalisis, merancang, membangun, dan menguji sistem. |

| Payment Gateway Artivisi | Penyedia layanan pembayaran digital yang mendukung pemrosesan transaksi. |

| Tim Fitur 6 – Penerimaan Donasi Luring | Pihak yang mengelola proses penerimaan donasi secara langsung oleh petugas. |

| Tim Fitur 12 – Relawan dan Operasional Acara | Pihak yang mengelola relawan dan operasional kegiatan. |

## 3.2 Kepentingan Stakeholder

Donatur membutuhkan proses donasi yang mudah, informasi jadwal yang jelas, serta informasi status pembayaran.

Staf internal membutuhkan data donasi dan transaksi yang terorganisasi.

Manajemen membutuhkan informasi yang dapat mendukung pemantauan aktivitas donasi.

Tim pengembang membutuhkan kebutuhan bisnis yang jelas sebagai dasar pengembangan sistem.

Payment Gateway Artivisi membutuhkan proses pertukaran informasi pembayaran sesuai ketentuan layanan.

Tim Fitur 6 dan Fitur 12 membutuhkan batas tanggung jawab dan mekanisme koordinasi yang jelas apabila terdapat kebutuhan integrasi.

# 4. PROSES BISNIS

## 4.1 Proses Bisnis yang Diharapkan

Proses bisnis utama Fitur 4 adalah pengelolaan donasi berulang melalui kanal pembayaran digital.

Alur proses bisnis yang diharapkan:

Donatur mengakses informasi kampanye.

Donatur memilih program yang menyediakan pilihan donasi berulang.

Donatur menentukan nominal, jadwal, periode, dan peruntukan donasi.

Donatur memberikan persetujuan atas kesediaan donasi.

Sistem mencatat kesediaan donasi dan jadwal yang telah ditentukan.

Sistem menjalankan mekanisme pembayaran sesuai metode yang disepakati.

Payment Gateway Artivisi memproses transaksi apabila digunakan.

Sistem memperoleh informasi status pembayaran.

Sistem memperbarui catatan transaksi berdasarkan status yang telah diverifikasi.

Informasi transaksi disediakan untuk kebutuhan administrasi dan fitur terkait.

Donatur memperoleh informasi terkait status donasi sesuai mekanisme komunikasi yang berlaku.

## 4.2 Proses Alternatif Pembayaran

### A. Pembayaran Berhasil

Donatur menyelesaikan pembayaran.

Layanan pembayaran memberikan informasi transaksi.

Sistem memverifikasi informasi pembayaran.

Status transaksi diperbarui menjadi berhasil.

Data transaksi disimpan untuk kebutuhan administrasi.

### B. Pembayaran Gagal

Proses pembayaran tidak berhasil.

Sistem memperoleh informasi kegagalan transaksi.

Status transaksi diperbarui menjadi gagal.

Donatur atau staf memperoleh informasi sesuai fasilitas yang tersedia.

Tindak lanjut pembayaran mengikuti aturan yang telah ditetapkan.

### C. Pembayaran Pending

Sistem menerima informasi bahwa transaksi masih dalam proses atau belum memperoleh status akhir.

Sistem mempertahankan status transaksi sebagai pending.

Sistem melakukan pemeriksaan status sesuai mekanisme yang disepakati.

Status diperbarui setelah hasil pembayaran dapat diverifikasi.

## 4.3 Proses Pengelolaan Donasi Berulang

Donatur dapat mengelola kesediaan donasi berulang sesuai ketentuan yang berlaku.

Pengelolaan tersebut meliputi:

Melihat informasi kesediaan donasi.

Melihat nominal dan jadwal donasi.

Menjeda donasi berulang.

Membatalkan donasi berulang.

Memperoleh pemberitahuan terkait perubahan status donasi.

Ketentuan waktu jeda, pembatalan, dan pengaruhnya terhadap transaksi yang sedang diproses masih perlu dikonfirmasi.

## 4.4 Hubungan dengan Proses Bisnis Fitur 6

Fitur 6 – Penerimaan Donasi Luring memiliki alur sementara sebagai berikut:

Petugas menerima donasi uang.

Petugas menginput data donatur dan transaksi.

Data yang dicatat meliputi nama, nomor telepon, jenis donasi, kanal, dan jumlah.

Data dan kuitansi disimpan secara digital.

Bukti donasi dikirim melalui WhatsApp.

Alur tersebut merupakan proses bisnis Fitur 6, bukan proses utama Fitur 4.

Fitur 4 berfokus pada donasi berulang dan pembayaran digital. Jika diperlukan pertukaran data antara kedua fitur, mekanisme integrasinya perlu disepakati oleh pihak terkait.

## 4.5 Hubungan dengan Proses Bisnis Fitur 12

Fitur 12 – Relawan dan Operasional Acara berfokus pada pengelolaan relawan dan kegiatan operasional.

Fitur 4 tidak bertanggung jawab atas pendaftaran relawan, pengaturan jadwal kegiatan, penugasan relawan, maupun pencatatan kehadiran.

Koordinasi antara Fitur 4 dan Fitur 12 dapat dilakukan apabila terdapat kebutuhan operasional yang melibatkan kegiatan donasi. Bentuk integrasi langsung masih perlu dikonfirmasi.

# 5. KEBUTUHAN BISNIS

## 5.1 Daftar Kebutuhan Bisnis

| ID | Kebutuhan Bisnis | Prioritas |

| --- | --- | --- |

| BR-001 | Organisasi membutuhkan fasilitas untuk mendukung donasi berulang. | Tinggi |

| BR-002 | Donatur membutuhkan kemampuan menentukan nominal donasi. | Tinggi |

| BR-003 | Donatur membutuhkan kemampuan menentukan jadwal dan periode donasi. | Tinggi |

| BR-004 | Sistem harus menyimpan kesediaan dan persetujuan donatur. | Tinggi |

| BR-005 | Organisasi membutuhkan dukungan pembayaran melalui kanal digital. | Tinggi |

| BR-006 | Organisasi membutuhkan informasi status pembayaran yang dapat diverifikasi. | Tinggi |

| BR-007 | Sistem perlu menyediakan informasi pengingat dan pemberitahuan pembayaran. | Sedang |

| BR-008 | Donatur membutuhkan fasilitas untuk menjeda atau membatalkan donasi berulang. | Sedang |

| BR-009 | Organisasi membutuhkan pencatatan transaksi yang terstruktur dan dapat ditelusuri. | Tinggi |

| BR-010 | Data transaksi perlu tersedia untuk mendukung kebutuhan administrasi, rekonsiliasi, dan pelaporan. | Tinggi |

| BR-011 | Sistem perlu mengurangi risiko pencatatan transaksi ganda. | Tinggi |

| BR-012 | Sistem perlu mendukung pertukaran data dengan layanan dan fitur terkait sesuai kesepakatan. | Tinggi |

## 5.2 Prioritas Kebutuhan

Prioritas kebutuhan bisnis dibagi menjadi:

Tinggi: Kebutuhan utama yang diperlukan agar proses bisnis donasi berulang dan pembayaran digital dapat berjalan.

Sedang: Kebutuhan pendukung yang meningkatkan kemudahan pengelolaan donasi.

Rendah: Kebutuhan tambahan yang dapat dipertimbangkan pada pengembangan berikutnya.

Penetapan prioritas akhir tetap mengikuti persetujuan pihak Baitulmal Tazkia.

# 6. ATURAN BISNIS

## 6.1 Aturan Donasi Berulang

Donatur harus memilih program yang mendukung donasi berulang.

Nominal donasi harus ditentukan sebelum kesediaan donasi disimpan.

Jadwal dan periode donasi harus dicatat dengan jelas.

Kesediaan donasi harus berdasarkan persetujuan donatur.

Perubahan atau pembatalan donasi mengikuti ketentuan yang ditetapkan organisasi.

## 6.2 Aturan Pembayaran

Pembayaran digital diproses melalui metode yang didukung oleh layanan pembayaran.

Transaksi tidak boleh dinyatakan berhasil sebelum statusnya diverifikasi.

Transaksi dengan status pending tidak boleh langsung dianggap berhasil atau gagal.

Informasi transaksi harus memiliki referensi yang dapat ditelusuri.

Pemrosesan ulang harus memperhatikan pencegahan transaksi ganda.

## 6.3 Aturan Pengingat dan Pemberitahuan

Donatur dapat menerima pengingat atau pemberitahuan terkait donasi sesuai mekanisme yang disetujui.

Informasi pemberitahuan harus sesuai dengan status transaksi yang tercatat.

Frekuensi dan waktu pengiriman pengingat harus ditentukan oleh organisasi.

## 6.4 Aturan Batas Tanggung Jawab

Fitur 4 bertanggung jawab terhadap pengelolaan donasi berulang dan kanal pembayaran digital.

Fitur 6 bertanggung jawab terhadap proses penerimaan dan pencatatan donasi luring.

Fitur 12 bertanggung jawab terhadap pengelolaan relawan dan operasional acara.

Integrasi antarf fitur hanya dilakukan berdasarkan kebutuhan dan kesepakatan yang telah ditentukan.

# 7. KEBUTUHAN NONFUNGSIONAL DAN KUALITAS BISNIS

| ID | Aspek | Kebutuhan |

| --- | --- | --- |

| BNFR-001 | Keamanan Data | Informasi donatur dan transaksi harus dilindungi dari akses yang tidak berwenang. |

| BNFR-002 | Keandalan Transaksi | Informasi status transaksi harus akurat dan dapat diverifikasi. |

| BNFR-003 | Kemudahan Penggunaan | Proses donasi harus mudah dipahami oleh donatur. |

| BNFR-004 | Konsistensi Data | Data donasi dan transaksi harus tersimpan secara terstruktur. |

| BNFR-005 | Keterlacakan | Informasi transaksi harus dapat ditelusuri berdasarkan referensi transaksi. |

| BNFR-006 | Integrasi | Sistem harus mendukung pertukaran data dengan layanan terkait sesuai kesepakatan. |

| BNFR-007 | Ketersediaan Informasi | Informasi status donasi dan pembayaran harus dapat diakses oleh pihak yang berwenang. |

# 8. BATASAN, ASUMSI, DAN KETERGANTUNGAN

## 8.1 Batasan

Fitur 4 berfokus pada donasi berulang dan kanal pembayaran digital.

Penerimaan donasi luring bukan tanggung jawab utama Fitur 4.

Pengelolaan relawan dan operasional acara bukan tanggung jawab Fitur 4.

Sistem bergantung pada kemampuan layanan pembayaran eksternal untuk memproses transaksi.

Sistem hanya dapat menggunakan metode pembayaran yang telah dikonfirmasi dan disetujui.

## 8.2 Asumsi

Donatur memiliki akses ke sistem untuk melakukan pendaftaran donasi.

Organisasi menyediakan informasi program donasi yang dapat dipilih.

Organisasi menetapkan ketentuan nominal, jadwal, dan periode donasi.

Layanan Payment Gateway Artivisi menyediakan dokumentasi integrasi yang diperlukan.

Pihak terkait memberikan persetujuan atas mekanisme pertukaran data.

## 8.3 Ketergantungan

Ketersediaan dan kemampuan Payment Gateway Artivisi.

Keputusan organisasi mengenai mekanisme pembayaran berulang.

Ketersediaan informasi kampanye dari fitur yang mengelolanya.

Kesepakatan integrasi dengan fitur terkait.

Kebijakan organisasi mengenai pengingat, jeda, dan pembatalan donasi.

# 9. KRITERIA KEBERHASILAN BISNIS

Pengembangan Fitur 4 diharapkan berhasil apabila:

Donatur dapat melakukan pendaftaran donasi berulang.

Donatur dapat menentukan nominal dan jadwal donasi.

Kesediaan dan persetujuan donatur dapat tersimpan dengan baik.

Pembayaran digital dapat diproses melalui metode yang disetujui.

Status transaksi dapat diketahui dan diverifikasi.

Data transaksi dapat tersimpan dan ditelusuri.

Donatur dapat memperoleh informasi terkait status donasi.

Organisasi dapat memantau informasi donasi berulang.

Risiko transaksi ganda dapat diminimalkan.

Data transaksi dapat disediakan untuk kebutuhan proses bisnis terkait.

Target kuantitatif, seperti persentase keberhasilan pembayaran, waktu pemrosesan, atau tingkat kesalahan transaksi, belum ditetapkan dan perlu dikonfirmasi oleh pihak organisasi.

# 10. ISU DAN HAL YANG MEMERLUKAN KONFIRMASI

| ID | Isu atau Pertanyaan | Pihak Terkait |

| --- | --- | --- |

| OQ-001 | Apakah pembayaran berulang menggunakan pengingat pembayaran manual, autodebit, atau keduanya? | PIC/Klien |

| OQ-002 | Metode pembayaran apa saja yang tersedia untuk donasi berulang? | Artivisi |

| OQ-003 | Bagaimana jadwal dan frekuensi pengingat pembayaran ditentukan? | PIC/Klien |

| OQ-004 | Bagaimana aturan percobaan ulang apabila pembayaran gagal? | PIC/Klien dan Artivisi |

| OQ-005 | Bagaimana sistem menangani transaksi pending atau timeout? | Artivisi |

| OQ-006 | Apakah Fitur 4 dan Fitur 6 memerlukan pertukaran data transaksi? | PIC Fitur 4 dan Fitur 6 |

| OQ-007 | Apakah Fitur 4 memerlukan integrasi dengan Fitur 12? | PIC Fitur 4 dan Fitur 12 |

| OQ-008 | Siapa yang bertanggung jawab terhadap pembuatan dan pengiriman tanda terima? | PIC/Klien |

| OQ-009 | Apakah tautan pembayaran satu kali termasuk kebutuhan versi awal? | PIC/Klien |

| OQ-010 | Bagaimana ketentuan jeda dan pembatalan donasi berulang? | PIC/Klien |

| OQ-011 | Bagaimana kebijakan perlindungan dan penyimpanan data donatur? | PIC/Klien |

| OQ-012 | Bagaimana mekanisme integrasi dan pertukaran data antarf fitur? | Tim Teknis dan PIC terkait |

# 11. PENUTUP

Dokumen Business Requirements Specification (BRS) Sistem Donasi Berulang dan Kanal Pembayaran Digital disusun sebagai dasar kebutuhan bisnis untuk pengembangan Fitur 4 pada Sistem Informasi Baitulmal Tazkia.

Dokumen ini menjelaskan tujuan bisnis, permasalahan, stakeholder, proses bisnis yang diharapkan, kebutuhan bisnis, aturan bisnis, batasan, serta kriteria keberhasilan sistem.

BRS ini juga memperjelas batas tanggung jawab Fitur 4 dengan Fitur 6 – Penerimaan Donasi Luring dan Fitur 12 – Relawan dan Operasional Acara.

Beberapa keputusan bisnis dan detail integrasi masih memerlukan konfirmasi dari pihak Baitulmal Tazkia dan pihak terkait. Oleh karena itu, dokumen ini berstatus draft final untuk review dan validasi, serta dapat ditetapkan sebagai baseline setelah memperoleh persetujuan pihak yang berwenang.
