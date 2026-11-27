# FUNCTIONAL REQUIREMENT

## FR-003 — Mengatur Nominal, Jadwal, dan Peruntukan Donasi

**Sistem Donasi Berulang dan Kanal Pembayaran Digital | Baitulmal Tazkia**

### A. Identitas Kebutuhan

| Elemen | Keterangan |
| :--- | :--- |
| **ID Requirement** | FR-003 |
| **Nama Requirement** | Mengatur Nominal, Jadwal, dan Peruntukan Donasi |
| **Aktor Utama** | Calon Donatur / Donatur |
| **Tujuan** | Memungkinkan donatur mengisi nominal donasi, periode atau jadwal donasi berulang, serta peruntukan dana sebelum melanjutkan proses. |
| **Prioritas** | Belum ditentukan; perlu konfirmasi. |
| **Status** | Draft untuk Presentasi – belum divalidasi dan belum disetujui. |
| **Acuan** | Dokumen FR-003 versi 0.1 Draft Awal dan SRS v0.2. |

### B. Deskripsi Kebutuhan

Setelah donatur memilih opsi donasi berulang pada proses FR-002, sistem menampilkan formulir untuk mengatur nominal donasi, periode atau jadwal donasi, dan peruntukan dana. Donatur mengisi informasi yang diminta. Sistem melakukan pemeriksaan terhadap kelengkapan dan format data. Apabila data dinilai valid, donatur dapat melanjutkan ke proses berikutnya. Apabila data belum lengkap atau tidak sesuai, sistem menolak kelanjutan proses dan menampilkan pesan agar donatur memperbaiki data.

> **Catatan:** Pilihan nilai nominal, daftar jadwal, daftar peruntukan, serta aturan validasinya belum ditetapkan pada dokumen sumber dan harus dikonfirmasi sebelum requirement disahkan.

### C. Ruang Lingkup dan Batasan

**Termasuk dalam FR-003:**
* Menampilkan isian nominal donasi.
* Menampilkan isian periode atau jadwal donasi berulang.
* Menampilkan isian peruntukan donasi.
* Menerima input dari donatur.
* Memeriksa kelengkapan dan kesesuaian format input.
* Menampilkan pesan ketika input belum lengkap atau tidak valid.
* Mengizinkan donatur melanjutkan apabila data dinyatakan valid.

**Tidak termasuk dalam FR-003:**
* Pemilihan opsi donasi berulang dan pemeriksaan ketersediaan fitur pada kampanye (FR-002).
* Penyimpanan persetujuan donatur, jadwal, dan bukti persetujuan (FR-004).
* Autentikasi pengguna.
* Pemrosesan pembayaran.
* Pengiriman pengingat atau notifikasi donasi.
* Pengubahan, penundaan, atau pembatalan donasi berulang.

### D. Alur Proses Bisnis

| No. | Aktor | Aktivitas / Respons Sistem |
| :--- | :--- | :--- |
| 1 | Sistem | Menampilkan formulir pengaturan nominal, jadwal, dan peruntukan setelah donatur memilih donasi berulang pada FR-002. |
| 2 | Donatur | Mengisi nominal donasi. |
| 3 | Donatur | Memilih atau mengisi periode/jadwal donasi sesuai opsi yang nantinya ditetapkan. |
| 4 | Donatur | Memilih atau mengisi peruntukan donasi sesuai opsi yang nantinya ditetapkan. |
| 5 | Sistem | Memeriksa kelengkapan dan format seluruh input. |
| 6a | Sistem | Jika data valid, mengizinkan donatur melanjutkan ke proses berikutnya. |
| 6b | Sistem | Jika data tidak lengkap atau tidak valid, menolak kelanjutan proses dan menampilkan pesan kesalahan yang jelas. |
| 7 | Donatur | Memperbaiki input yang ditandai sistem, kemudian mengirimkan kembali data untuk diperiksa. |

### E. Kebutuhan Data, Tipe Data, dan Validasi

*Tabel berikut merangkum data yang perlu tersedia pada formulir. Tipe data dan aturan validasi yang belum tercantum pada sumber ditandai sebagai belum ditentukan, bukan diasumsikan.*

| Data / Field | Tujuan | Tipe Data | Validasi / Aturan |
| :--- | :--- | :--- | :--- |
| **Nominal donasi** | Menentukan besaran donasi berulang. | Belum ditentukan. | Wajib diisi atau tidak, nominal minimum/maksimum, serta apakah input bebas atau pilihan nominal perlu dikonfirmasi. |
| **Periode / jadwal** | Menentukan frekuensi atau waktu donasi berulang. | Belum ditentukan. | Daftar pilihan, format jadwal, dan batasan periode belum ditentukan. |
| **Peruntukan donasi** | Menentukan alokasi atau tujuan penggunaan dana. | Belum ditentukan. | Daftar peruntukan, apakah pilihan tunggal atau lebih dari satu, serta ketergantungan pada program/kampanye perlu dikonfirmasi. |
| **Pesan kesalahan** | Memberi tahu donatur ketika input tidak lengkap atau tidak sesuai. | Teks. | Pesan harus jelas dan membantu donatur mengetahui bagian yang perlu diperbaiki; redaksi final belum ditentukan. |

### F. Rancangan Tampilan / UI Mockup

*Rancangan pada bagian ini bersifat deskriptif dan belum merupakan desain UI final. Penempatan komponen, label tombol, gaya input, serta redaksi pesan masih perlu disepakati.*

#### F.1 Kondisi Normal
* Sistem menampilkan bagian/formulir pengaturan donasi berulang.
* Formulir memuat input nominal donasi.
* Formulir memuat pilihan atau input periode/jadwal.
* Formulir memuat pilihan atau input peruntukan donasi.
* Tersedia aksi untuk melanjutkan setelah donatur mengisi data.

#### F.2 Kondisi Input Tidak Valid
* Sistem menandai atau menunjukkan bagian yang belum diisi atau tidak sesuai.
* Sistem menampilkan pesan kesalahan yang mudah dipahami.
* Donatur dapat memperbaiki data dan mencoba melanjutkan kembali.

> *Arah visual awal dari pembahasan: kombinasi warna biru navy dan putih (mengacu pada arahan awal NFR-006); penerapan final perlu dikonfirmasi.*

### G. Kebutuhan Non-Fungsional Terkait

| Aspek | Kebutuhan / Arah Awal | Status |
| :--- | :--- | :--- |
| **Keamanan** | Input nominal, jadwal, dan peruntukan perlu diproses secara aman. | Detail kontrol dan kriteria belum ditentukan. |
| **Kinerja** | Sistem diharapkan memberikan respons saat formulir ditampilkan dan divalidasi. | Target waktu respons belum ditentukan. |
| **Usability** | Formulir dan pesan kesalahan perlu mudah dipahami donatur. | Kriteria pengujian usability belum ditentukan. |
| **Antarmuka** | Arah warna awal biru navy dan putih. | Desain dan standar UI final perlu dikonfirmasi. |

### H. Kriteria Penerimaan (Acceptance Criteria)

* [ ] Sistem menampilkan field nominal, periode/jadwal, dan peruntukan setelah donatur masuk ke proses FR-003.
* [ ] Donatur dapat mengisi data yang ditampilkan.
* [ ] Sistem memeriksa kelengkapan dan format data sebelum donatur melanjutkan.
* [ ] Jika data memenuhi aturan yang telah disepakati, sistem mengizinkan donatur melanjutkan ke proses berikutnya.
* [ ] Jika data tidak lengkap atau tidak sesuai, sistem menolak kelanjutan proses dan menampilkan pesan yang jelas.
* [ ] Proses pengaturan pada FR-003 tidak dianggap selesai apabila data yang diwajibkan belum memenuhi aturan.

> **Catatan:** Kriteria penerimaan ini masih bersifat draft. Kriteria rinci baru dapat ditetapkan setelah aturan nominal, jadwal, dan peruntukan disepakati.

### I. Hal yang Memerlukan Konfirmasi

| No. | Pertanyaan / Keputusan yang Dibutuhkan | Status |
| :--- | :--- | :--- |
| 1 | Nominal donasi diisi bebas atau dipilih dari nominal yang tersedia? Apakah ada batas minimum dan maksimum? | Belum dikonfirmasi |
| 2 | Pilihan periode/jadwal apa saja yang tersedia dan bagaimana format pemilihannya? | Belum dikonfirmasi |
| 3 | Siapa yang menetapkan dan mengelola daftar peruntukan donasi? | Belum dikonfirmasi |
| 4 | Apakah peruntukan bergantung pada kampanye/program yang dipilih? | Belum dikonfirmasi |
| 5 | Field mana yang wajib diisi dan apa aturan validasi masing-masing? | Belum dikonfirmasi |
| 6 | Apa redaksi pesan kesalahan yang akan ditampilkan? | Belum dikonfirmasi |
| 7 | Di tahap mana donatur mengirimkan atau mengonfirmasi pengaturan ini? | Belum dikonfirmasi |
| 8 | Apakah peruntukan dapat diubah setelah pengaturan donasi berulang dibuat? | Belum dikonfirmasi |

### J. Catatan untuk Presentasi

* FR-003 menjelaskan pengisian nominal, jadwal/periode, dan peruntukan donasi berulang.
* Validasi data dilakukan sebelum donatur melanjutkan ke proses berikutnya.
* Persetujuan donatur dan penyimpanan bukti persetujuan berada pada FR-004, bukan FR-003.
* Nominal minimum/maksimum, daftar jadwal, daftar peruntukan, tipe data, dan aturan validasi masih menjadi bahan konfirmasi.
* Dokumen ini disusun untuk bahan presentasi dan pembahasan; bukan penanda bahwa kebutuhan telah final atau disetujui klien.

*— Akhir Dokumen FR-003 —*