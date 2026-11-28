# BAITULMAL TAZKIA
## SISTEM DONASI BERULANG DAN KANAL PEMBAYARAN DIGITAL

### FUNCTIONAL REQUIREMENT (FR)
# FR-003: MENGATUR NOMINAL, JADWAL, DAN PERUNTUKAN

**Versi:** 1.0 | **Status:** Draft untuk Review dan Validasi Klien | **Tanggal:** 25 November 2026  
**Acuan:** SRS dan BRS Fitur 4 versi 1.0, tanggal acuan 14 November 2026.

---

## A. Identitas Kebutuhan

| Informasi | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-003 |
| **Nama Kebutuhan** | Mengatur Nominal, Jadwal, dan Peruntukan |
| **Aktor Utama** | Calon donatur / donatur |
| **Tujuan** | Memungkinkan donatur menentukan nominal, jadwal, periode, dan peruntukan donasi berulang serta memastikan isian lengkap dan sesuai format sebelum diteruskan ke proses penyimpanan kesediaan donasi. |
| **Pemicu** | Donatur memilih program yang mendukung donasi berulang dan masuk ke tahap pengaturan donasi. |
| **Kondisi Awal** | Program/kampanye menyediakan pilihan donasi berulang; bidang pengaturan tersedia untuk ditampilkan. |
| **Prioritas Usulan** | Must Have — usulan, perlu persetujuan Baitulmal Tazkia. |
| **Tingkat Kesulitan Usulan** | 3 — Medium |
| **Status** | Draft untuk review dan validasi; belum menjadi baseline implementasi. |

---

## B. Deskripsi Functional Requirement

Setelah donatur memilih program yang mendukung donasi berulang, sistem menampilkan bidang nominal, jadwal/periode, dan peruntukan. Donatur mengisi atau memilih nilai pada bidang tersebut. Sistem memeriksa kelengkapan dan format isian. Jika data valid, sistem mengizinkan donatur melanjutkan ke FR-004. Jika ada isian wajib kosong atau nilai tidak sesuai, sistem menolak kelanjutan proses dan menampilkan pesan perbaikan yang dapat dipahami. Nilai nominal, pilihan periode, daftar peruntukan, dan aturan rinci belum ditetapkan dalam SRS/BRS.

### 1. Format Outline dan Batasan
* Sistem menampilkan bidang nominal donasi.
* Sistem menampilkan bidang jadwal/periode donasi.
* Sistem menampilkan bidang peruntukan donasi.
* Donatur mengisi atau memilih nilai pada bidang yang tersedia.
* Sistem memvalidasi kelengkapan dan format data.
* Data valid dapat diteruskan ke FR-004; data tidak valid harus diperbaiki.

> **Batasan:** FR-003 hanya mencakup pengisian dan validasi nominal, jadwal/periode, dan peruntukan. Pemilihan program/opsi donasi berulang termasuk FR-002. Penyimpanan kesediaan, jadwal, dan persetujuan termasuk FR-004. Pembayaran, pengingat, notifikasi, jeda, dan pembatalan berada pada FR lain.

### 2. Proses Bisnis

| Tahap | Aktivitas | Dasar / Catatan |
| :---: | :--- | :--- |
| **1** | Donatur telah memilih program yang mendukung donasi berulang. | Tertulis di SRS; tahap pemilihan termasuk FR-002. |
| **2** | Sistem menampilkan bidang nominal, jadwal/periode, dan peruntukan. | Tertulis di SRS. |
| **3** | Donatur mengisi atau memilih nilai pada bidang yang tersedia. | Tertulis di SRS; bentuk input perlu konfirmasi. |
| **4** | Sistem memvalidasi kelengkapan dan format isian. | Tertulis di SRS; aturan rinci perlu konfirmasi. |
| **5** | Jika data valid, sistem mengizinkan proses dilanjutkan ke FR-004. | Tertulis secara konseptual; aksi/tombol lanjut perlu konfirmasi. |

> **Alur Alternatif:** Apabila bidang wajib kosong atau format/nilai tidak sesuai, sistem menampilkan pesan perbaikan dan tidak mengizinkan proses dilanjutkan sampai data diperbaiki. Jenis bidang wajib, batas nilai, dan isi pesan masih perlu konfirmasi.

### 3. Field, Tipe Data, dan Validasi

| Field | Tipe Data | Validasi / Aturan Awal | Status |
| :--- | :--- | :--- | :--- |
| **Nominal donasi** | Belum ditentukan | Kelengkapan dan format diperiksa; batas minimum/maksimum belum ditetapkan. | Perlu konfirmasi: pilihan atau isian bebas, batas nilai, mata uang. |
| **Jadwal/periode donasi** | Belum ditentukan | Kelengkapan dan format diperiksa. | Perlu konfirmasi: daftar periode, frekuensi, tanggal mulai. |
| **Peruntukan donasi** | Belum ditentukan | Kelengkapan dan format diperiksa. | Perlu konfirmasi: daftar peruntukan dan pengelola daftar. |
| **Pesan validasi** | Teks | Pesan jelas dan membantu memperbaiki isian. | Perlu konfirmasi isi dan bentuk pesan. |

### 4. Mockup Konseptual

```text
+-------------------------------------------------------+
| ATUR DONASI BERULANG                                  |
+-------------------------------------------------------+
| Nominal donasi       : [ pilihan / isian nominal    ] |
| Jadwal/periode       : [ pilihan jadwal / periode   ] |
| Peruntukan           : [ pilihan peruntukan         ] |
|                                                       |
|                    [ LANJUTKAN ]                      |
+-------------------------------------------------------+
```
*Catatan: Mockup ini konseptual, bukan desain UI final. Arahan visual SRS NFR-006 adalah navy blue dan putih.*

### 5. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Terkait | Catatan |
| :--- | :--- | :--- |
| **Keamanan** | Data donatur dilindungi dari akses tidak berwenang. | Mengacu NFR-001 SRS. |
| **Kemudahan penggunaan** | Bidang dan pesan validasi mudah dipahami. | Mengacu NFR-004 SRS. |
| **Tampilan** | Antarmuka mengikuti navy blue dan putih. | Mengacu NFR-006 SRS. |
| **Kinerja** | Validasi ditampilkan dalam waktu wajar. | Target waktu respons belum ditetapkan. |

### 6. Kriteria Penerimaan
- [ ] Sistem menampilkan bidang nominal, jadwal/periode, dan peruntukan setelah donatur memilih donasi berulang.
- [ ] Donatur dapat mengisi atau memilih nilai pada bidang yang tersedia.
- [ ] Sistem memeriksa kelengkapan dan format data.
- [ ] Data valid dapat diteruskan ke FR-004.
- [ ] Data tidak valid/tidak lengkap tidak dapat diteruskan dan sistem menampilkan pesan perbaikan.

### 7. Prioritas dan Tingkat Kesulitan

| Komponen | Usulan | Dasar |
| :--- | :--- | :--- |
| **Prioritas MoSCoW** | Must Have — usulan, perlu persetujuan Baitulmal Tazkia. | Must Have diturunkan dari BR-002 dan BR-003 pada BRS yang berprioritas Tinggi. |
| **Tingkat kesulitan** | 3 — Medium | 3 — Medium karena fungsi berupa penampilan bidang, pengisian, dan validasi, sementara aturan rinci masih perlu disepakati. |

### 8. Dasar Pertimbangan Penilaian
Skala kesulitan 1–5: **1–2 Easy**, **3 Medium**, dan **4–5 Hard**. FR-003 diusulkan pada tingkat **3 (Medium)** karena melibatkan beberapa input dan validasi. Kompleksitas dapat berubah setelah aturan nominal, jadwal, dan peruntukan disepakati. Prioritas *Must Have* merupakan usulan berdasarkan kebutuhan bisnis BR-002 dan BR-003 yang berprioritas Tinggi, bukan persetujuan final klien.

### 9. Hal yang Perlu Dikonfirmasi kepada Klien
1. Apakah nominal dipilih dari daftar atau diisi bebas? Apakah ada batas minimum dan maksimum?
2. Pilihan jadwal/periode apa saja yang tersedia dan kapan tanggal mulai ditentukan?
3. Daftar peruntukan apa saja yang dapat dipilih dan siapa pengelolanya?
4. Apakah pilihan nominal, jadwal, dan peruntukan berbeda menurut program/kampanye atau metode pembayaran?
5. Bidang mana yang wajib diisi dan bagaimana aturan validasinya?
6. Apa isi pesan kesalahan/perbaikan yang diinginkan?
7. Apakah tombol lanjut berada di akhir FR-003 dan meneruskan data ke FR-004?

### 10. Checklist Konfirmasi Client

| ID & Nama Kebutuhan | Prioritas Usulan | Kesulitan Usulan | Tidak Dibutuhkan / Catatan Client |
| :--- | :--- | :--- | :--- |
| **FR-003 — Mengatur Nominal, Jadwal, dan Peruntukan** | Must Have — usulan, perlu persetujuan Baitulmal Tazkia. | 3 — Medium | |

### 11. Catatan dan Status Dokumen
FR-003 berada setelah FR-002 dan sebelum FR-004. Dokumen ini diselaraskan dengan SRS/BRS Fitur 4 versi 1.0 tanggal 14 November 2026. Nilai nominal, pilihan periode, daftar peruntukan, tipe data, dan aturan validasi rinci belum ditetapkan oleh sumber sehingga ditandai perlu dikonfirmasi.  
**Status:** Draft untuk Review dan Validasi Klien.