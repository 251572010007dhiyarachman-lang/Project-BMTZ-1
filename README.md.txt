# Sistem Donasi Berulang dan Kanal Pembayaran Digital

**Baitulmal Tazkia – Fitur 4**

## 1. Deskripsi Proyek

Sistem Donasi Berulang dan Kanal Pembayaran Digital merupakan bagian dari proyek Sistem Informasi Baitulmal Tazkia yang berfokus pada pengelolaan donasi berulang dan proses pembayaran melalui kanal digital.

Sistem ini membantu donatur mendaftarkan donasi berulang, menentukan nominal dan jadwal donasi, serta memantau status pembayaran. Sistem juga menyediakan data transaksi yang telah diverifikasi untuk kebutuhan fitur terkait.

Dokumen ini dibuat sebagai README untuk memberikan gambaran umum mengenai proyek dan menjadi panduan awal bagi pihak yang terlibat dalam pengembangan sistem.

## 2. Tujuan Sistem

Sistem ini dikembangkan dengan tujuan:

- Memudahkan donatur dalam mendaftarkan dan mengelola donasi berulang.
- Membantu proses pembayaran donasi melalui kanal digital.
- Menyediakan informasi status pembayaran yang akurat.
- Mengurangi risiko kesalahan pencatatan dan transaksi ganda.
- Menyediakan data transaksi untuk kebutuhan fitur terkait.
- Mendukung pengelolaan donasi yang lebih terstruktur dan terdokumentasi.

## 3. Ruang Lingkup Sistem

### Fitur yang termasuk dalam ruang lingkup

1. Menampilkan informasi kampanye donasi.
2. Menyediakan pilihan donasi berulang.
3. Mengatur nominal, jadwal, periode, dan peruntukan donasi.
4. Menyimpan kesediaan donasi dan jadwal donatur.
5. Mendukung proses pembayaran melalui kanal digital.
6. Memverifikasi dan memperbarui status transaksi.
7. Mengirimkan pengingat dan pemberitahuan pembayaran sesuai mekanisme yang disepakati.
8. Mendukung jeda dan pembatalan donasi berulang.
9. Menyediakan data transaksi untuk kebutuhan integrasi dengan fitur terkait.
10. Menyediakan tautan pembayaran satu kali apabila disetujui dan didukung oleh payment gateway.

### Fitur di luar ruang lingkup

- Pencatatan penerimaan donasi luring oleh petugas.
- Pengelolaan antrean donasi luring.
- Pengelolaan data relawan.
- Penyusunan jadwal acara.
- Penugasan relawan.

Fungsi tersebut menjadi tanggung jawab fitur lain dalam proyek.

## 4. Aktor dan Pihak Terkait

| Aktor | Tanggung Jawab |
|---|---|
| Donatur | Memilih program, menentukan nominal dan jadwal, memberikan persetujuan, serta melakukan pembayaran. |
| Staf Internal Baitulmal Tazkia | Mengelola dan memantau data donasi serta transaksi sesuai hak akses. |
| Sistem Fitur 4 | Mengelola kesediaan donasi berulang, jadwal, status, dan data pembayaran digital. |
| Payment Gateway Artivisi | Memproses pembayaran digital dan memberikan informasi status transaksi sesuai kemampuan layanan. |
| Fitur 6 – Penerimaan Donasi Luring | Mengelola pencatatan donasi yang diterima secara langsung oleh petugas. |
| Fitur 12 – Relawan dan Operasional Acara | Mengelola data relawan dan operasional kegiatan. |

## 5. Alur Utama Sistem

Alur utama donasi berulang secara umum adalah:

1. Donatur membuka halaman informasi kampanye.
2. Sistem menampilkan informasi program donasi.
3. Donatur memilih opsi donasi berulang.
4. Donatur mengisi nominal, jadwal, periode, dan peruntukan donasi.
5. Sistem memvalidasi data yang dimasukkan.
6. Donatur memberikan persetujuan terhadap kesediaan donasi.
7. Sistem menyimpan kesediaan donasi dan jadwal.
8. Sistem menjalankan mekanisme pembayaran sesuai metode yang disepakati.
9. Payment Gateway Artivisi memproses pembayaran apabila digunakan.
10. Sistem menerima dan memverifikasi status transaksi.
11. Sistem memperbarui catatan transaksi.
12. Sistem menyediakan data transaksi terverifikasi untuk kebutuhan fitur terkait.

**Catatan:** Mekanisme pembayaran berulang, baik melalui pengingat pembayaran manual maupun autodebit, masih memerlukan konfirmasi dari pihak terkait.

## 6. Kebutuhan Fungsional

Sistem memiliki 15 kebutuhan fungsional yang tercantum dalam dokumen SRS.

| ID | Kebutuhan Fungsional |
|---|---|
| FR-001 | Menampilkan Halaman Kampanye |
| FR-002 | Memilih Donasi Berulang |
| FR-003 | Mengatur Nominal, Jadwal, dan Peruntukan |
| FR-004 | Menyimpan Kesediaan Donasi dan Jadwal |
| FR-005 | Mengirim Pengingat Pembayaran |
| FR-006 | Memproses Pembayaran melalui Gateway |
| FR-007 | Memverifikasi dan Memperbarui Status Transaksi |
| FR-008 | Menyediakan Data untuk Tanda Terima |
| FR-009 | Menyediakan Catatan Donasi untuk Integrasi |
| FR-010 | Menyediakan Data Transaksi untuk Pelaporan dan Rekonsiliasi |
| FR-011 | Menjeda Donasi Berulang |
| FR-012 | Membatalkan Donasi Berulang |
| FR-013 | Mengirim Pemberitahuan Status Donasi |
| FR-014 | Membuat Tautan Pembayaran Satu Kali |
| FR-015 | Mencegah Transaksi Ganda |

## 7. Kebutuhan Nonfungsional

Sistem memiliki tujuh kebutuhan nonfungsional utama:

- **Keamanan:** Melindungi data donatur dan transaksi dari akses yang tidak berwenang.
- **Keandalan:** Tidak menyatakan transaksi berhasil tanpa status pembayaran yang telah diverifikasi.
- **Integrasi:** Mendukung pertukaran data melalui API atau mekanisme yang disepakati.
- **Kemudahan Penggunaan:** Menyediakan antarmuka yang mudah dipahami oleh donatur dan staf.
- **Konsistensi Data:** Menyediakan referensi transaksi untuk penelusuran dan pencocokan.
- **Tampilan:** Mengikuti arahan identitas visual awal Baitulmal Tazkia, yaitu navy blue dan putih.
- **Pemulihan Kegagalan:** Mencatat kegagalan integrasi dan mencegah kesalahan pencatatan akibat pengiriman ulang.

## 8. Integrasi Sistem

### Payment Gateway Artivisi

Digunakan untuk mendukung proses pembayaran digital dan memberikan informasi status transaksi.

Data yang mungkin dipertukarkan meliputi:

- Referensi transaksi.
- Nominal pembayaran.
- Informasi pembayaran yang diperlukan.
- Status transaksi.
- Waktu transaksi.
- Informasi respons pembayaran.

Detail metode pembayaran, autentikasi, callback/webhook, timeout, dan retry masih perlu disepakati.

### Fitur 6 – Penerimaan Donasi Luring

Fitur 6 bertanggung jawab atas pencatatan donasi yang diterima secara langsung oleh petugas.

Integrasi dengan Fitur 4 masih memerlukan klarifikasi mengenai jenis data, tujuan pertukaran data, sistem sumber data utama, dan mekanisme integrasi.

### Fitur 12 – Relawan dan Operasional Acara

Fitur 12 bertanggung jawab atas pengelolaan relawan dan operasional acara.

Fitur 4 tidak mengambil alih pengelolaan relawan, jadwal kegiatan, maupun penugasan petugas. Detail integrasi langsung masih perlu dikonfirmasi.

## 9. Status Pengembangan

| Keterangan | Detail |
|---|---|
| Nama Proyek | Sistem Donasi Berulang dan Kanal Pembayaran Digital |
| Organisasi | Baitulmal Tazkia |
| Nomor Fitur | Fitur 4 |
| Versi SRS | 1.0 |
| Tanggal Dokumen | 14 November 2026 |
| Status | Draft Final untuk Review dan Validasi |

Dokumen SRS belum menjadi baseline sebelum mendapatkan persetujuan dari pihak yang berwenang.

## 10. Hal yang Masih Memerlukan Konfirmasi

Beberapa keputusan yang masih perlu dikonfirmasi meliputi:

- Mekanisme pembayaran berulang: pengingat manual, autodebit, atau keduanya.
- Metode pembayaran yang didukung oleh Payment Gateway Artivisi.
- Jadwal dan frekuensi pengingat pembayaran.
- Aturan percobaan ulang ketika pembayaran gagal.
- Penanganan status pending atau timeout.
- Kebutuhan integrasi Fitur 4 dengan Fitur 6 dan Fitur 12.
- Pihak yang bertanggung jawab atas pembuatan dan pengiriman tanda terima.
- Mekanisme jeda dan pembatalan donasi.
- Format data, autentikasi, dan mekanisme pertukaran data antarf fitur.

## 11. Referensi

Dokumen yang menjadi acuan dalam penyusunan README ini:

1. Software Requirements Specification (SRS) – Sistem Donasi Berulang dan Kanal Pembayaran Digital, Fitur 4, versi 1.0.
2. Workbook Proyek Sistem Informasi Baitulmal Tazkia – Fitur 4.
3. Dokumen Fitur 6 – Penerimaan Donasi Luring.
4. Dokumen Fitur 12 – Relawan dan Operasional Acara.
5. Ringkasan rapat pengembangan sistem donasi dan CRM.
6. Dokumentasi Payment Gateway Artivisi, apabila telah tersedia dan disetujui.

---

README ini disusun berdasarkan dokumen SRS Fitur 4 versi 1.0 dan berfungsi sebagai gambaran umum proyek. Perubahan kebutuhan, keputusan bisnis, serta detail integrasi harus mengikuti hasil validasi dan persetujuan pihak terkait.
