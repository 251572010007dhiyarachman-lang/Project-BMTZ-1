# FUNCTIONAL REQUIREMENT (FR)

## FR-011 — Menjeda Donasi Berulang

**Sistem Donasi Berulang dan Kanal Pembayaran Digital**

### A. Identitas Kebutuhan

| Elemen | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-011 |
| **Nama Kebutuhan** | Menjeda Donasi Berulang |
| **Aktor Utama** | Donatur dan sistem. |
| **Tujuan** | Memungkinkan donatur menjeda donasi berulang yang dapat dikelola tanpa perlu menghubungi staf, dengan status jeda dan waktu berlakunya yang dapat ditelusuri. |
| **Prioritas** | Belum ditentukan. |
| **Status Kebutuhan** | Dasar kebutuhan fitur jeda tersedia pada SRS Draft v0.2. Aturan waktu efektif jeda, jangka waktu, dan mekanisme melanjutkan kembali masih memerlukan klarifikasi. |

### B. Deskripsi Functional Requirement

Ketika donatur memilih fitur jeda pada donasi berulang yang dapat dikelola, sistem harus menerima permintaan tersebut dan memvalidasi hak akses donatur sebelum melakukan perubahan. Jika permintaan memenuhi ketentuan, sistem mengubah status atau jadwal donasi sesuai aturan jeda yang telah disetujui. Sistem juga harus mencatat status jeda dan waktu berlakunya agar perubahan tersebut dapat ditelusuri.

Apabila penagihan sudah berjalan ketika donatur mengajukan permintaan jeda, sistem harus memeriksa status penagihan dan menerapkan aturan waktu efektif jeda yang berlaku. Sistem menampilkan hasil sesuai aturan tersebut dan tidak menjanjikan bahwa transaksi yang sudah diproses dapat dibatalkan.

#### B.1 Pemicu dan Kondisi Awal

| Elemen | Ketentuan |
| :--- | :--- |
| **Pemicu** | Donatur memilih jeda pada donasi berulang yang dapat dikelola. |
| **Kondisi awal** | Fitur jeda dan autentikasi donatur tersedia. Donasi berulang telah terdaftar melalui FR-004. |
| **Hasil yang diharapkan** | Permintaan jeda diproses setelah hak akses donatur divalidasi; status jeda dan waktu berlakunya dapat ditelusuri. |

#### B.2 Alur Utama

1. Donatur memilih fitur jeda pada donasi berulang yang dapat dikelola.
2. Sistem memastikan fitur jeda dan autentikasi donatur tersedia.
3. Sistem menerima permintaan jeda dan memvalidasi hak akses donatur terhadap donasi yang dipilih.
4. Jika hak akses valid, sistem mengubah status atau jadwal donasi sesuai aturan jeda yang telah disetujui.
5. Sistem mencatat status jeda dan waktu berlakunya agar perubahan dapat ditelusuri.

> **Catatan:** Langkah memastikan fitur dan autentikasi tersedia merupakan penjabaran dari kondisi awal FR-011. Kriteria donasi yang dapat dikelola, mekanisme autentikasi, aturan mulai berlakunya jeda, jangka waktu jeda, dan cara melanjutkan kembali belum ditetapkan secara rinci dalam SRS Draft v0.2.

#### B.3 Alur Alternatif dan Kondisi Khusus

| Kode | Kondisi | Perilaku Sistem |
| :--- | :--- | :--- |
| **ALT-01** | Penagihan sudah berjalan saat permintaan jeda diajukan. | Sistem memeriksa status penagihan dan aturan waktu efektif jeda sebelum mengubah jadwal. Sistem menampilkan hasil sesuai aturan yang berlaku dan tidak menjanjikan pembatalan transaksi yang sudah diproses. |
| **ALT-02** | Hak akses donatur tidak valid. | Sistem tidak mengubah status atau jadwal donasi. Pesan yang ditampilkan dan mekanisme penanganan lebih lanjut perlu dikonfirmasi. |
| **ALT-03** | Donasi tidak termasuk donasi yang dapat dikelola. | Sistem tidak mengubah status atau jadwal donasi. Kriteria donasi yang dapat dikelola serta pesan kepada donatur perlu dikonfirmasi. |

> *Aturan waktu efektif jeda, khususnya ketika penagihan sedang berjalan, mengacu pada SRS OQ-012 dan ALT-07. Sistem tidak boleh mengasumsikan bahwa transaksi yang sudah diproses oleh penyedia pembayaran dapat dihentikan.*

#### B.4 Batasan Ruang Lingkup

* FR-011 hanya membahas proses menjeda donasi berulang.
* Pembatalan donasi berulang dibahas pada FR-012.
* Penyimpanan kesediaan donasi dan jadwal awal dibahas pada FR-004.
* Pemrosesan penagihan melalui *payment gateway* dibahas pada FR-006.
* Pengingat dan notifikasi dibahas pada FR-005 dan FR-013.
* FR-011 tidak menetapkan perubahan nominal atau peruntukan donasi.
* Konten komunikasi kepada donatur tidak ditetapkan dalam FR-011; SRS Bab 6 menempatkan hal tersebut pada Kelompok 11.

### C. Data yang Digunakan dan Validasi

*SRS Draft v0.2 belum menetapkan nama field basis data, tipe data, maupun aturan validasi rinci untuk FR-011. Tabel berikut memuat elemen data yang tersirat dari kebutuhan jeda. Nama field merupakan usulan untuk pembahasan, bukan nama kolom basis data final.*

| No. | Field / Elemen Data Usulan | Keterangan atau Validasi Awal | Status |
| :--- | :--- | :--- | :--- |
| 1 | **Referensi donasi berulang** | Mengidentifikasi donasi berulang yang dipilih dan dapat dikelola oleh donatur yang sah. | Format referensi perlu dikonfirmasi. |
| 2 | **Identitas/hak akses donatur** | Hak akses harus divalidasi sebelum status atau jadwal donasi diubah. | Mekanisme autentikasi dan sumber identitas perlu dikonfirmasi. |
| 3 | **Permintaan jeda** | Permintaan diproses hanya jika donasi dapat dikelola dan aturan efektif jeda terpenuhi. | Aturan waktu efektif perlu dikonfirmasi (OQ-012). |
| 4 | **Status donasi** | Status dapat berubah menjadi jeda sesuai aturan yang disetujui. SRS Bab 2.3 menyebut status aktif/jeda/batal jika fitur disepakati. | Daftar status final dan transisinya perlu dikonfirmasi. |
| 5 | **Waktu berlaku jeda** | Waktu mulai berlakunya jeda harus dapat ditelusuri. | Aturan penentuan waktu perlu dikonfirmasi. |
| 6 | **Jangka waktu jeda** | SRS belum menetapkan apakah jeda memiliki batas waktu atau tidak. | Perlu konfirmasi. |
| 7 | **Jadwal setelah jeda** | Perlu ditentukan apakah periode penagihan dilewati, digeser, atau dilanjutkan dengan aturan tertentu. | Perlu konfirmasi. |

> *Tipe data untuk seluruh elemen di atas belum ditentukan dalam SRS Draft v0.2.*

### D. Gambaran UI / Mockup

*Sketsa berikut merupakan gambaran tekstual awal, bukan desain antarmuka final. Elemen, label, teks konfirmasi, dan aturan yang ditampilkan perlu divalidasi dengan pihak Baitulmal Tazkia.*

#### D.1 Donatur memilih jeda pada donasi berulang

| Elemen Tampilan | Contoh Isi |
| :--- | :--- |
| **Identitas organisasi** | Baitulmal Tazkia |
| **Judul halaman** | Kelola Donasi Berulang |
| **Referensi** | `[referensi donasi]` |
| **Informasi donasi** | Nominal: `[nominal]` \| Jadwal: `[jadwal]` \| Peruntukan: `[peruntukan]` |
| **Status saat ini** | `[aktif]` |
| **Tombol tindakan** | `[Jeda donasi]` |
| **Konfirmasi** | `[Konfirmasi jeda — teks dan aturan efektif perlu dikonfirmasi]` |

#### D.2 Hasil permintaan jeda

| Kondisi | Informasi yang Ditampilkan |
| :--- | :--- |
| **Permintaan jeda diterima** | Status: `[jeda]` \| Berlaku sejak: `[waktu berlaku]` |
| **Penagihan sedang berjalan** | Pesan hasil sesuai aturan efektif jeda. Sistem tidak menjanjikan transaksi yang sudah diproses dapat dibatalkan. |

> *Arahan awal rapat untuk tampilan antarmuka adalah navy blue dan putih (NFR-006). Penerapan visual akhir harus disesuaikan dengan identitas resmi organisasi.*

### E. Non-Functional Requirement Terkait

| Aspek | Kebutuhan | Acuan dan Catatan |
| :--- | :--- | :--- |
| **Keamanan** | Hanya donatur yang berhak dapat menjeda donasi. Hak akses divalidasi sebelum status diubah dan data donatur dilindungi sesuai kebijakan yang disepakati. | NFR-001; detail autentikasi, akses, dan retensi perlu diklarifikasi (OQ-013). |
| **Keandalan status** | Sistem tidak menjanjikan transaksi yang sudah diproses dapat dihentikan dan tidak mengubah status pembayaran yang telah ditetapkan. | NFR-002 dan ALT-07. |
| **Keterlacakan** | Status jeda dan waktu berlakunya dapat ditelusuri. | Kriteria penerimaan FR-011; format referensi mengacu pada NFR-005 dan perlu disepakati. |
| **Kemudahan penggunaan** | Donatur dapat menjeda donasi tanpa menghubungi staf dengan instruksi yang jelas dan mudah dipahami. | Workbook/SRS FR-011 dan NFR-004; kriteria pengujian perlu diklarifikasi. |
| **Tampilan** | Antarmuka mengikuti arahan awal rapat, yaitu navy blue dan putih. | NFR-006; disesuaikan dengan identitas resmi organisasi. |
| **Integrasi** | Status jeda yang dibutuhkan Kelompok 11 disediakan melalui kontrak data yang disepakati. | NFR-003 dan Bab 2.3; kanal, payload, dan frekuensi sinkronisasi perlu diklarifikasi (OQ-008). |

### F. Kriteria Penerimaan

*FR-011 dapat dinyatakan memenuhi kebutuhan apabila kondisi berikut dapat dibuktikan:*

* [ ] Status jeda dan waktu mulai berlakunya dapat ditelusuri.
* [ ] Permintaan jeda hanya diproses setelah hak akses donatur divalidasi.
* [ ] Jika penagihan sudah berjalan, sistem menampilkan hasil sesuai aturan waktu efektif jeda tanpa menjanjikan pembatalan transaksi yang sudah diproses.
* [ ] Permintaan dari donatur yang tidak berhak tidak mengubah status atau jadwal donasi.
* [ ] Perubahan status atau jadwal dilakukan sesuai aturan jeda yang telah disepakati.

> *Kriteria penerimaan ini disusun berdasarkan SRS Draft v0.2. Kriteria mengenai waktu efektif, jangka waktu jeda, dan cara melanjutkan kembali perlu diperbarui setelah aturan bisnis dikonfirmasi.*

### G. Hal yang Masih Perlu Dikonfirmasi

| No. | Pertanyaan Klarifikasi | Acuan |
| :--- | :--- | :--- |
| 1 | Bagaimana jeda berlaku jika penagihan sedang diproses? | OQ-012; ALT-07 |
| 2 | Kapan jeda mulai berlaku: segera, mulai periode berikutnya, atau dengan batas waktu sebelum tanggal penagihan? | OQ-003 |
| 3 | Apakah jeda memiliki jangka waktu tertentu atau tanpa batas? Bagaimana donasi dilanjutkan kembali: otomatis atau oleh donatur? | Belum ditentukan dalam SRS |
| 4 | Donasi dengan status apa saja yang termasuk kategori dapat dikelola oleh donatur? | Aturan bisnis |
| 5 | Bagaimana donatur diautentikasi dan hak aksesnya divalidasi? Apakah menggunakan akun dari Kelompok 1? | Integrasi/autentikasi |
| 6 | Bagaimana jadwal setelah jeda diperlakukan: penagihan pada periode jeda dilewati, digeser, atau diatur dengan cara lain? | Aturan bisnis |
| 7 | Apakah pengingat dan notifikasi (FR-005 dan FR-013) dihentikan selama donasi dalam status jeda? | Integrasi antarfungsi |
| 8 | Apakah perubahan status perlu diteruskan ke Payment Gateway Artivisi untuk metode yang mendukung penagihan otomatis? | OQ-001; OQ-002 |
| 9 | Status apa yang dibutuhkan Kelompok 11 dan kapan status jeda disinkronkan? | OQ-008 |
| 10 | Apakah staf internal dapat menjeda donasi atas permintaan donatur? | Aturan operasional |
| 11 | Bagaimana aturan akses, retensi, dan kepemilikan data riwayat jeda serta target waktu respons? | OQ-013; OQ-014 |

### H. Ringkasan untuk Presentasi

* FR-011 menjelaskan fitur untuk menjeda donasi berulang oleh donatur. Setelah donasi berulang terdaftar melalui FR-004, donatur dapat memilih fitur jeda pada donasi yang dapat dikelola tanpa harus menghubungi staf. Sistem memvalidasi hak akses donatur, kemudian mengubah status atau jadwal sesuai aturan yang disetujui dan mencatat waktu berlakunya.
* Jika penagihan sudah berjalan ketika permintaan jeda diajukan, sistem harus memeriksa status penagihan dan aturan waktu efektif jeda. Sistem tidak boleh menjanjikan bahwa transaksi yang sudah diproses dapat dibatalkan. FR-011 hanya membahas jeda, bukan pembatalan donasi, pemrosesan pembayaran melalui gateway, atau pengingat dan notifikasi.
* *Dasar penyusunan:* SRS Draft v0.2, bagian FR-011 pada Bab 4, ALT-07 pada Bab 3.2, hubungan subsistem dengan Kelompok 11 pada Bab 2.3, serta NFR-001, NFR-002, NFR-003, NFR-004, NFR-005, NFR-006, OQ-003, OQ-008, OQ-012, OQ-013, dan OQ-014. Langkah memastikan fitur/autentikasi tersedia dan pencatatan status/waktu berlakunya merupakan penjabaran dari kondisi awal serta kriteria penerimaan SRS, bukan keputusan tambahan.

### I. Catatan Status Dokumen

Dokumen ini merupakan finalisasi penulisan FR-011 berdasarkan dokumen FR-011 awal dan SRS Draft v0.2. Finalisasi ini merapikan struktur, istilah, alur, dan kriteria penerimaan tanpa menetapkan aturan bisnis yang belum disepakati. Dokumen belum dapat dianggap sebagai persetujuan final klien sampai pertanyaan klarifikasi pada Bagian G ditinjau dan divalidasi oleh pihak terkait.

| Disusun oleh | Ditinjau oleh | Disetujui oleh |
| :--- | :--- | :--- |
| **Tim/Analis Kebutuhan**<br>Nama: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_<br>Tanggal: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | <br>Nama: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_<br>Peran: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_<br>Tanggal: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | <br>Nama: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_<br>Jabatan: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_<br>Tanggal: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |