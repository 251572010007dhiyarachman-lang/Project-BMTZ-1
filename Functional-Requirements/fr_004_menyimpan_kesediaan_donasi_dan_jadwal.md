# FUNCTIONAL REQUIREMENT

## FR-004 — Menyimpan Kesediaan Donasi dan Jadwal

**Sistem Donasi Berulang dan Kanal Pembayaran Digital | Baitulmal Tazkia**

### A. Identitas Kebutuhan

| Elemen | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-004 |
| **Nama Kebutuhan** | Menyimpan Kesediaan Donasi dan Jadwal |
| **Aktor Utama** | Calon donatur / donatur |
| **Tujuan** | Menyimpan kesediaan donasi berulang beserta jadwal dan data pendaftaran yang diperlukan, serta memberikan hasil pendaftaran kepada donatur. |
| **Prioritas** | Belum ditentukan. |
| **Status** | Draft untuk presentasi; belum menjadi persyaratan final klien. Bukti persetujuan (consent) dan rincian data yang disimpan masih perlu klarifikasi. |
| **Acuan** | FR-004 versi 0.1 Draft Awal dan SRS Draft v0.2 (tanggal acuan 26 Oktober 2026). |

### B. Deskripsi Functional Requirement

Setelah donatur mengirim pendaftaran yang lengkap, sistem menyimpan kesediaan donasi berulang beserta jadwalnya. Data yang disimpan mencakup identitas referensi, nominal, jadwal, peruntukan, status, dan bukti persetujuan sesuai aturan yang disetujui. Sistem kemudian memberikan hasil pendaftaran kepada donatur. Apabila penyimpanan gagal, sistem tidak menampilkan pendaftaran sukses dan kegagalan dicatat agar dapat ditelusuri.

* **Pemicu:** Donatur mengirim pendaftaran yang lengkap.
* **Kondisi awal:** Data wajib dan persetujuan yang disyaratkan tersedia.

### C. Ruang Lingkup dan Batasan

**Termasuk dalam FR-004:**
* Menerima pendaftaran donasi berulang yang lengkap dari donatur.
* Menyimpan identitas referensi, nominal, jadwal, peruntukan, status, dan bukti persetujuan sesuai aturan yang disetujui.
* Memberikan hasil pendaftaran kepada donatur.
* Menangani kegagalan penyimpanan tanpa menampilkan status sukses dan mencatat kegagalan agar dapat ditelusuri.

**Tidak termasuk dalam FR-004:**
* Pengisian dan validasi nominal, periode/jadwal, dan peruntukan (FR-003).
* Pengingat, penagihan, atau pembayaran melalui payment gateway.
* Notifikasi, jeda, dan pembatalan donasi berulang.
* Pengiriman data ke kelompok lain (diatur pada FR terpisah dalam SRS).
* Autentikasi donatur, karena tidak dicantumkan sebagai bagian FR-004 pada SRS.

### D. Proses Bisnis

*Data pendaftaran diasumsikan telah divalidasi pada FR-003. Label menunjukkan asal informasi: “Tertulis di SRS”, “Disimpulkan dari SRS”, atau “Perlu Konfirmasi”.*

| No. | Aktor | Aktivitas | Dasar |
| :--- | :--- | :--- | :--- |
| 1 | Donatur | Mengirim pendaftaran yang lengkap. | Tertulis di SRS; titik pengiriman perlu konfirmasi. |
| 2 | Sistem | Memastikan data wajib dan persetujuan yang disyaratkan tersedia. | Disimpulkan dari kondisi awal FR-004 dan Bab 3.1 SRS; cara/tempat persetujuan perlu konfirmasi. |
| 3 | Sistem | Menyimpan identitas referensi, nominal, jadwal, peruntukan, status, dan bukti persetujuan sesuai aturan yang disetujui. | Tertulis di SRS; aturan penyimpanan dan rincian data perlu konfirmasi. |
| 4 | Sistem | Memberikan hasil pendaftaran kepada donatur. | Tertulis di SRS; bentuk tampilan hasil perlu konfirmasi. |

**Alur alternatif — penyimpanan gagal:**
* Sistem tidak menampilkan pendaftaran sukses.
* Sistem mencatat kegagalan agar dapat ditelusuri.
* Pesan kegagalan kepada donatur dan kemungkinan mengulang pendaftaran belum ditentukan.
* Penanganan jika persetujuan yang disyaratkan belum tersedia saat pendaftaran dikirim belum ditentukan.

### E. Field, Tipe Data, dan Validasi

*SRS Draft v0.2 menyebut unsur data yang disimpan, tetapi belum menetapkan tipe data maupun aturan validasi rinci. Nama field berikut adalah usulan untuk pembahasan, bukan nama kolom basis data atau keputusan final.*

| Field Usulan | Tujuan / Isi | Tipe Data | Validasi / Status |
| :--- | :--- | :--- | :--- |
| **Identitas / referensi pendaftaran** | ID atau referensi pendaftaran yang dapat ditelusuri. | Belum ditentukan. | Makna identitas referensi dan formatnya perlu konfirmasi; SRS mensyaratkan ID/referensi yang jelas. |
| **Nominal donasi** | Nominal yang telah diisi pada FR-003. | Belum ditentukan. | Mengikuti data yang telah divalidasi pada FR-003; detail perlu konfirmasi. |
| **Jadwal / periode donasi** | Jadwal atau periode dari FR-003. | Belum ditentukan. | Mengikuti data yang telah divalidasi pada FR-003; detail perlu konfirmasi. |
| **Peruntukan donasi** | Peruntukan yang dipilih pada FR-003. | Belum ditentukan. | Mengikuti data yang telah divalidasi pada FR-003; detail perlu konfirmasi. |
| **Status pendaftaran** | Status awal pendaftaran. | Belum ditentukan. | Pendaftaran berhasil memiliki status awal yang jelas; nilai status perlu konfirmasi. |
| **Bukti persetujuan (consent)** | Bukti kesediaan donatur. | Belum ditentukan. | Disimpan sesuai aturan yang disetujui; bentuk dan aturan perlu konfirmasi. |
| **Catatan kegagalan penyimpanan** | Informasi untuk menelusuri kegagalan. | Belum ditentukan. | Kegagalan dicatat agar dapat ditelusuri; isi dan bentuk catatan perlu konfirmasi. |

### F. UI Mockup

*Mockup berikut adalah wireframe konseptual berdasarkan sumber FR-004. Susunan elemen, isi pesan, bentuk persetujuan, dan informasi ringkasan masih perlu dikonfirmasi. Arah visual awal: navy blue dan putih (SRS NFR-006).*

**Contoh kondisi ketika penyimpanan berhasil:**
```text
+-----------------------------------------------------------------------+
| BAITULMAL TAZKIA — Hasil Pendaftaran Donasi Berulang                  |
+-----------------------------------------------------------------------+
| Pesan hasil pendaftaran : [Pendaftaran berhasil disimpan — teks perlu |
|                           dikonfirmasi]                               |
| Referensi pendaftaran   : [ID / referensi pendaftaran]                |
| Status                  : [Status awal pendaftaran]                   |
| Ringkasan donasi        : [Nominal, jadwal, dan peruntukan — jika     |
|                           disepakati]                                 |
+-----------------------------------------------------------------------+
```
*Catatan: sistem memberikan hasil pendaftaran kepada donatur. Format ID, status awal, redaksi pesan, dan ringkasan yang ditampilkan belum ditetapkan.*

**Contoh kondisi ketika penyimpanan gagal:**
```text
+-----------------------------------------------------------------------+
| BAITULMAL TAZKIA — Hasil Pendaftaran Donasi Berulang                  |
+-----------------------------------------------------------------------+
| Pesan hasil   : [Pendaftaran belum berhasil disimpan — teks perlu     |
|                 dikonfirmasi]                                         |
| Status        : Tidak menampilkan status pendaftaran sukses.          |
| Tindak lanjut : [Apakah donatur dapat mencoba kembali? Perlu          |
|                 konfirmasi.]                                          |
+-----------------------------------------------------------------------+
```
*Catatan: kegagalan penyimpanan dicatat agar dapat ditelusuri. Bentuk pesan kepada donatur dan opsi mencoba kembali belum ditentukan.*

### G. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Awal | Catatan |
| :--- | :--- | :--- |
| **Keamanan** | Data donatur dilindungi sesuai kebijakan yang disetujui. Data kartu atau nomor rekening mentah tidak ditetapkan untuk disimpan tanpa dasar dan desain keamanan yang disetujui. | Detail kebijakan, akses, retensi, dan kepemilikan basis data perlu klarifikasi (SRS OQ-013). |
| **Keandalan status** | Sistem tidak menampilkan pendaftaran berhasil jika penyimpanan gagal. | Selaras dengan prinsip NFR-002 SRS. |
| **Keterlacakan** | Pendaftaran memiliki referensi yang memungkinkan penelusuran; kegagalan penyimpanan dapat ditelusuri. | Format referensi perlu disepakati (NFR-005). |
| **Kinerja** | Hasil pendaftaran dapat ditampilkan dalam waktu yang wajar. | Target waktu respons belum ditetapkan (OQ-014). |
| **Kemudahan penggunaan** | Hasil pendaftaran dan pesan kegagalan jelas dan mudah dipahami. | Kriteria uji perlu klarifikasi (NFR-004). |
| **Tampilan** | Antarmuka mengikuti arahan awal rapat: navy blue dan putih. | Disesuaikan dengan identitas resmi organisasi (NFR-006). |

### H. Kriteria Penerimaan Awal

* [ ] Sistem menyimpan identitas referensi, nominal, jadwal, peruntukan, status, dan bukti persetujuan sesuai aturan yang disetujui.
* [ ] Pendaftaran yang berhasil mempunyai ID/referensi dan status awal yang jelas.
* [ ] Sistem memberikan hasil pendaftaran kepada donatur.
* [ ] Jika penyimpanan gagal, sistem tidak menampilkan pendaftaran sukses dan kegagalan dicatat agar dapat ditelusuri.
* [ ] Kegagalan penyimpanan tidak menghasilkan status sukses palsu.

> *Kriteria ini masih bersifat awal dan perlu diperbarui setelah aturan bisnis dikonfirmasi.*

### I. Hal yang Perlu Dikonfirmasi

| No. | Pertanyaan / Keputusan | Status |
| :--- | :--- | :--- |
| 1 | Apakah persetujuan satu kali untuk autodebit cukup, dan apa persyaratan persetujuan untuk setiap metode pembayaran? (OQ-002) | Belum dikonfirmasi |
| 2 | Apa bentuk bukti persetujuan yang disimpan, serta kapan dan di mana donatur memberikannya (FR-003, FR-004, atau tahap lain)? | Belum dikonfirmasi |
| 3 | Apa yang dimaksud identitas referensi: ID pendaftaran, identitas donatur, atau keduanya? Data donatur apa yang disimpan? | Belum dikonfirmasi |
| 4 | Apa nilai status awal pendaftaran? Apakah daftar status mengikuti status aktif, jeda, dan batal yang disebut SRS? | Belum dikonfirmasi |
| 5 | Bagaimana format ID/referensi agar dapat dicocokkan antarsubsistem? (NFR-005) | Belum dikonfirmasi |
| 6 | Apa saja yang ditampilkan pada hasil pendaftaran, bagaimana pesan kegagalan disampaikan, dan apakah donatur dapat mengulang pendaftaran? | Belum dikonfirmasi |
| 7 | Bagaimana kegagalan penyimpanan dicatat, dan siapa yang menelusurinya? | Belum dikonfirmasi |
| 8 | Apakah pendaftaran ganda oleh donatur yang sama perlu dicegah? | Belum dikonfirmasi |
| 9 | Bagaimana aturan akses, retensi, dan kepemilikan basis data untuk data pendaftaran? (OQ-013) | Belum dikonfirmasi |

### J. Catatan untuk Presentasi

* FR-004 berjalan setelah pengisian dan validasi data pada FR-003.
* Fokus FR-004 adalah menyimpan kesediaan donasi berulang dan jadwal, beserta data pendaftaran dan bukti persetujuan sesuai aturan yang disetujui.
* Setelah penyimpanan, sistem memberikan hasil pendaftaran kepada donatur.
* Jika penyimpanan gagal, sistem tidak boleh menampilkan status sukses palsu dan kegagalan harus dapat ditelusuri.
* FR-004 tidak mencakup pengingat, penagihan/pembayaran gateway, notifikasi, jeda/pembatalan, atau pengiriman data ke kelompok lain.
* Dokumen ini dirapikan untuk bahan presentasi; belum menjadi baseline kebutuhan dan belum disetujui klien.

*— Akhir Dokumen FR-004 —*