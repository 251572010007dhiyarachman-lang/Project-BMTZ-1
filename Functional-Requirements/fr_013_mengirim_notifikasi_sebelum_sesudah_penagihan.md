# FUNCTIONAL REQUIREMENT

## FR-013 — MENGIRIM NOTIFIKASI SEBELUM/SESUDAH PENAGIHAN

**Sistem Donasi Berulang dan Kanal Pembayaran Digital**

| Informasi Dokumen | Keterangan |
| :--- | :--- |
| **Organisasi** | Baitulmal Tazkia |
| **ID Kebutuhan** | FR-013 |
| **Versi Dokumen** | 1.0 |
| **Tanggal acuan** | 26 Oktober 2026 (SRS Draft v0.2) |
| **Status** | Finalisasi kebutuhan berdasarkan SRS; keputusan kanal, waktu, dan cakupan masih memerlukan validasi klien |
| **Prioritas** | Belum ditetapkan dalam SRS Draft v0.2 |

### 1. Identitas dan Tujuan Kebutuhan

| Elemen | Uraian |
| :--- | :--- |
| **Nama kebutuhan** | Mengirim Notifikasi Sebelum/Sesudah Penagihan |
| **Aktor utama** | Sistem; donatur sebagai penerima notifikasi; kelompok 11 (Hubungan Donatur dan Komunikasi) sebagai penerima status minimum jika dibutuhkan. |
| **Tujuan** | Memberi tahu donatur sebelum dan sesudah penagihan sesuai aturan yang disetujui, serta meneruskan status minimum ke kelompok komunikasi jika dibutuhkan. |
| **Pemicu** | Aturan notifikasi telah disepakati dan peristiwa yang relevan terjadi. |
| **Kondisi awal** | Kanal komunikasi dan data kontak tersedia sesuai izin. |
| **Batasan** | FR-013 membahas notifikasi terkait penagihan. Pengingat pembayaran manual dirinci pada FR-005; pemrosesan penagihan melalui gateway pada FR-006; verifikasi status transaksi pada FR-007; dan data tanda terima pada FR-008. Hubungan FR-013 dengan FR-005 belum diputuskan. FR-013 tidak menetapkan status berhasil/gagal transaksi dan tidak mengambil alih konten serta penjadwalan komunikasi berkala yang menurut SRS berada pada kelompok 11. |

### 2. Deskripsi Functional Requirement

Apabila aturan notifikasi telah disepakati dan peristiwa yang relevan terjadi, sistem harus memicu notifikasi kepada donatur sesuai peristiwa yang disepakati. Workbook SRS menyebut pemberitahuan sebelum penarikan dan setelah penagihan berhasil, sedangkan ringkasan rapat menyebut pengingat. Sistem juga meneruskan status minimum ke kelompok komunikasi apabila dibutuhkan. Apabila notifikasi gagal dikirim, sistem mencatat hasil pengiriman jika kanal mendukung. Kegagalan notifikasi tidak boleh mengubah status transaksi.

### 3. Proses Bisnis

**Aktor:** Sistem, donatur sebagai penerima notifikasi, dan kelompok 11 sebagai penerima status minimum. Status transaksi ditetapkan melalui FR-007.

| No. | Aktivitas | Dasar / Status |
| :--- | :--- | :--- |
| 1 | Peristiwa yang relevan terjadi dan aturan notifikasi telah disepakati. Workbook menyebut peristiwa sebelum penarikan dan setelah berhasil. | Tertulis di SRS; daftar peristiwa final perlu dikonfirmasi |
| 2 | Sistem memastikan kanal komunikasi dan data kontak tersedia sesuai izin. | Disimpulkan dari kondisi awal SRS; sumber kontak dan bentuk izin perlu dikonfirmasi |
| 3 | Sistem memicu dan mengirim notifikasi sesuai peristiwa yang disepakati. | Tertulis di SRS; waktu, kanal, dan isi pesan perlu dikonfirmasi |
| 4 | Untuk notifikasi setelah berhasil, sistem hanya mengirim setelah transaksi terverifikasi berhasil. | Disimpulkan dari NFR-002 dan FR-007 |
| 5 | Sistem meneruskan status minimum ke kelompok komunikasi jika dibutuhkan. | Tertulis di SRS; data minimum, kanal, dan frekuensi sinkronisasi perlu dikonfirmasi (OQ-008) |

#### 3.1 Alur Alternatif: Notifikasi Gagal Terkirim

* Sistem mencatat hasil pengiriman apabila kemampuan kanal mendukung pencatatan.
* Status transaksi tidak berubah hanya karena notifikasi gagal dikirim.
* Pengiriman ulang dan penanganan ketika kanal tidak mendukung pencatatan hasil mengikuti aturan yang harus disepakati.

> *Catatan: SRS belum menetapkan mekanisme retry maupun penanganan kegagalan di luar pencatatan yang didukung kanal.*

#### 3.2 Alur Alternatif: Penagihan Otomatis Tidak Digunakan

* SRS menyatakan bahwa cakupan FR-013 bergantung pada keputusan apakah alur penagihan otomatis digunakan.
* Jika hanya pembayaran manual yang diterapkan, notifikasi sebelum penarikan belum tentu relevan.
* Perlu diputuskan apakah notifikasi sebelum penarikan digantikan oleh pengingat pada FR-005 atau tetap menjadi bagian FR-013.
* *Acuan klarifikasi:* SRS OQ-001.

### 4. Data dan Validasi

*SRS Draft v0.2 belum menetapkan field teknis, tipe data, maupun aturan validasi rinci untuk FR-013. Daftar berikut merupakan kebutuhan data konseptual, bukan keputusan skema basis data.*

| Data yang Diperlukan | Kegunaan / Validasi | Status |
| :--- | :--- | :--- |
| **Peristiwa pemicu** | Menentukan kondisi yang memicu pengiriman notifikasi; hanya peristiwa yang telah disepakati yang diproses. | Daftar peristiwa final perlu dikonfirmasi |
| **Waktu notifikasi** | Menentukan waktu pengiriman sebelum atau sesudah penagihan sesuai aturan. | Selisih waktu dan jadwal perlu dikonfirmasi (OQ-003) |
| **Kanal pengiriman** | Menentukan media komunikasi yang digunakan. | Kanal belum ditetapkan (OQ-003) |
| **Kontak dan izin donatur** | Memastikan kontak tersedia dan notifikasi dikirim sesuai izin. | Sumber kontak dan bentuk izin perlu dikonfirmasi |
| **Isi pesan notifikasi** | Memuat informasi yang akan diterima donatur dan dapat diuji setelah spesifikasi ditetapkan. | Isi pesan dan pengelola naskah perlu dikonfirmasi (OQ-008) |
| **Status minimum kelompok 11** | Menyediakan informasi minimum yang diperlukan kelompok komunikasi. | Elemen data dan waktu sinkronisasi perlu dikonfirmasi (OQ-008) |
| **Hasil pengiriman** | Mencatat hasil pengiriman jika kanal mendukung. | Format dan nilai status perlu dikonfirmasi |

### 5. Rancangan Antarmuka / Contoh Notifikasi

*FR-013 merupakan fungsi pengiriman pesan. Bentuk antarmuka bergantung pada kanal komunikasi yang belum ditetapkan. Contoh berikut menggambarkan elemen informasi, bukan naskah final.*

#### 5.1 Notifikasi Sebelum Penagihan

| Elemen | Isi |
| :--- | :--- |
| **Identitas** | Identitas resmi Baitulmal Tazkia |
| **Judul** | Pemberitahuan Penagihan Donasi Berulang |
| **Isi pesan** | Sapaan dan kalimat pemberitahuan (teks perlu dikonfirmasi) |
| **Informasi donasi** | Nominal, jadwal penagihan, dan peruntukan |

#### 5.2 Notifikasi Setelah Penagihan Berhasil

| Elemen | Isi |
| :--- | :--- |
| **Identitas** | Identitas resmi Baitulmal Tazkia |
| **Judul** | Pemberitahuan Penagihan Berhasil |
| **Isi pesan** | Sapaan dan kalimat pemberitahuan (teks perlu dikonfirmasi) |
| **Informasi transaksi** | Nominal, waktu transaksi, dan referensi donasi/transaksi |

#### 5.3 Catatan Hasil Pengiriman

| Elemen | Isi |
| :--- | :--- |
| **Peristiwa** | Sebelum / sesudah penagihan |
| **Kanal** | Kanal yang digunakan |
| **Hasil pengiriman** | Terkirim / gagal atau nilai lain yang ditetapkan setelah kanal dipilih |
| **Dampak pada transaksi** | Status transaksi tidak berubah hanya karena notifikasi gagal |

> *Elemen, kanal, susunan pesan, teks, pengguna yang dapat melihat catatan, dan bentuk tampilan harus dikonfirmasi. Arahan awal rapat untuk tampilan adalah navy blue dan putih (NFR-006), sejauh kanal yang dipilih mendukung.*

### 6. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Terkait FR-013 | Acuan |
| :--- | :--- | :--- |
| **Keamanan** | Data kontak dan data donatur dilindungi sesuai kebijakan yang disetujui. Notifikasi hanya dikirim sesuai izin. | NFR-001; OQ-013 |
| **Keandalan status** | Notifikasi tidak mengubah status transaksi. Notifikasi setelah berhasil hanya dikirim berdasarkan hasil transaksi yang telah terverifikasi dari sumber yang disepakati. | NFR-002; FR-007 |
| **Integrasi** | Status minimum untuk kelompok 11 disediakan melalui kontrak integrasi yang disepakati; sistem tidak mengakses basis data kelompok lain secara langsung. | NFR-003; Bab 2.3; OQ-008 |
| **Keterlacakan** | Hasil pengiriman dapat ditelusuri apabila kanal mendukung pencatatan. | NFR-005 |
| **Kemudahan penggunaan** | Isi notifikasi jelas dan mudah dipahami donatur. | NFR-004 |
| **Kinerja** | Notifikasi dikirim sesuai waktu yang disepakati. | OQ-003; OQ-014 |

### 7. Kriteria Penerimaan

* [ ] Notifikasi dipicu sesuai peristiwa dan aturan yang telah disetujui.
* [ ] Waktu pengiriman dan isi pesan dapat diuji berdasarkan spesifikasi yang telah ditetapkan.
* [ ] Notifikasi sebelum penagihan hanya dijalankan sesuai keputusan mengenai penggunaan alur penagihan otomatis dan hubungan FR-013 dengan FR-005.
* [ ] Notifikasi setelah berhasil hanya dikirim untuk transaksi yang telah terverifikasi berhasil.
* [ ] Jika notifikasi gagal, sistem mencatat hasil apabila kanal mendukung dan status transaksi tidak berubah.
* [ ] Status minimum diteruskan ke kelompok komunikasi apabila dibutuhkan, sesuai kontrak integrasi yang disepakati.
* [ ] Pengiriman notifikasi hanya dilakukan ke kontak donatur yang tersedia sesuai izin.

> *Catatan: Kriteria terkait kanal, waktu, isi pesan, izin, retry, dan integrasi baru dapat diuji secara rinci setelah keputusan bisnis dan spesifikasi teknis disepakati.*

### 8. Keputusan yang Masih Memerlukan Konfirmasi

*Butir berikut belum diputuskan dalam SRS Draft v0.2 dan perlu divalidasi oleh Baitulmal Tazkia sebelum FR-013 disetujui untuk implementasi.*

1. Apakah alur penagihan otomatis digunakan? Jika tidak, apakah notifikasi sebelum penarikan tetap berlaku? (OQ-001)
2. Apa daftar peristiwa final yang memicu notifikasi? Apakah mencakup penagihan gagal atau pending?
3. Berapa lama sebelum penagihan notifikasi dikirim dan kanal apa yang digunakan? (OQ-003)
4. Apa hubungan FR-013 dengan pengingat pada FR-005: fungsi terpisah atau satu fungsi, dan bagaimana mencegah pesan ganda?
5. Siapa yang menulis isi pesan dan menjadwalkan notifikasi: subsistem ini atau kelompok 11? (OQ-008; Bab 6)
6. Status minimum apa yang dibutuhkan kelompok 11 dan kapan status tersebut disinkronkan? (OQ-008)
7. Dari mana kontak donatur diperoleh dan izin apa yang harus dipenuhi sebelum notifikasi dikirim?
8. Apakah notifikasi gagal dicoba ulang? Bagaimana penanganannya jika kanal tidak mendukung pencatatan hasil?
9. Apakah notifikasi setelah berhasil sama dengan tanda terima FR-008 atau merupakan fungsi terpisah? (OQ-009)
10. Apakah notifikasi dihentikan ketika donasi dijeda atau dibatalkan? (FR-011 dan FR-012)
11. Bagaimana aturan akses, retensi, kepemilikan data, dan target waktu pengiriman ditetapkan? (OQ-013; OQ-014)

### 9. Batasan dan Ketergantungan

* **FR-005:** Pengingat untuk pembayaran manual; hubungan dengan FR-013 masih perlu diputuskan.
* **FR-006:** Pemrosesan penagihan melalui *payment gateway*.
* **FR-007:** Verifikasi status transaksi; menjadi dasar untuk memastikan notifikasi setelah berhasil hanya dikirim setelah transaksi terverifikasi.
* **FR-008:** Data tanda terima; perlu dipastikan apakah notifikasi setelah berhasil terpisah dari tanda terima.
* **FR-011 dan FR-012:** Jeda dan pembatalan donasi berulang; perlu ditentukan dampaknya terhadap notifikasi terjadwal.
* **Kelompok 11:** Penerima status minimum melalui kontrak integrasi yang disepakati.

### 10. Ringkasan untuk Validasi

* FR-013 mengatur pengiriman notifikasi kepada donatur sebelum dan sesudah penagihan berdasarkan peristiwa yang disepakati. Sistem dapat meneruskan status minimum kepada kelompok komunikasi jika dibutuhkan dan mencatat hasil pengiriman apabila kanal mendukung. Kegagalan notifikasi tidak mengubah status transaksi. Notifikasi setelah berhasil hanya boleh dikirim berdasarkan transaksi yang telah terverifikasi berhasil.
* Dokumen ini merupakan versi finalisasi kebutuhan berdasarkan SRS Draft v0.2. Statusnya belum berarti seluruh aturan bisnis telah disetujui klien. Keputusan mengenai penggunaan penagihan otomatis, kanal, waktu, isi pesan, hubungan dengan FR-005/FR-008, izin kontak, dan integrasi kelompok 11 tetap harus divalidasi.

### 11. Referensi

SRS Draft v0.2: Bab 2.3; Bab 4 (FR-013: pemicu, kondisi awal, alur utama, alur alternatif, dan kriteria penerimaan); Bab 6; NFR-001, NFR-002, NFR-003, NFR-004, NFR-005; serta OQ-001, OQ-003, OQ-008, OQ-009, OQ-013, dan OQ-014.