# BAITULMAL TAZKIA
## SISTEM DONASI BERULANG DAN KANAL PEMBAYARAN DIGITAL

### FUNCTIONAL REQUIREMENT (FR)
# FR-011: MENJEDA DONASI BERULANG

**Versi:** 1.0 | **Status:** Draft untuk Review dan Validasi Klien | **Tanggal:** 25 November 2026  
**Acuan:** SRS dan BRS Fitur 4 versi 1.0, tanggal acuan 14 November 2026.

---

## A. Identitas Kebutuhan

| Informasi | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-011 |
| **Nama Kebutuhan** | Menjeda Donasi Berulang |
| **Aktor Utama** | Donatur; staf internal Baitulmal Tazkia atau pihak berwenang sesuai hak akses; Sistem Fitur 4. |
| **Tujuan** | Memungkinkan donatur atau pihak berwenang mengubah status kesediaan donasi berulang menjadi dijeda sesuai aturan yang ditetapkan organisasi. |
| **Pemicu** | Donatur atau pihak berwenang memilih tindakan jeda pada kesediaan donasi berulang yang masih aktif. |
| **Kondisi Awal** | Data kesediaan donasi berulang tersedia dan dapat diidentifikasi; pengguna memiliki hak untuk melakukan tindakan jeda. |
| **Prioritas Usulan** | Should Have — usulan, mengikuti BR-008 yang berprioritas Sedang; perlu persetujuan klien. |
| **Tingkat Kesulitan Usulan** | 3 — Medium |
| **Status** | Draft untuk review dan validasi; ketentuan waktu jeda, dampak pada jadwal/tagihan berjalan, dan mekanisme aktivasi kembali belum ditetapkan. |

---

## B. Deskripsi Functional Requirement

Sistem memungkinkan donatur atau pihak berwenang menjeda kesediaan donasi berulang sesuai aturan yang disepakati. Ketika tindakan jeda diajukan oleh pengguna yang memiliki hak akses, sistem memeriksa kesediaan donasi yang dipilih, memvalidasi kewenangan, kemudian memperbarui status kesediaan menjadi dijeda dan menyimpan informasi perubahan untuk keperluan penelusuran. Selama status dijeda, pelaksanaan donasi berikutnya mengikuti kebijakan jeda yang ditetapkan Baitulmal Tazkia.

* **Pemicu:** Permintaan jeda atas kesediaan donasi berulang.
* **Kondisi Awal:** Data kesediaan tersedia dan pengguna berwenang.
* **Hasil yang Diharapkan:** Status kesediaan tercatat sebagai dijeda sesuai kebijakan.

### B.1 Batasan Ruang Lingkup
* FR-011 hanya membahas tindakan menjeda kesediaan donasi berulang dan pencatatan perubahan statusnya.
* FR-011 tidak membatalkan kesediaan donasi secara permanen; pembatalan dibahas pada FR-012.
* Pengaturan nominal, jadwal, dan peruntukan awal berada pada FR-003; penyimpanan kesediaan berada pada FR-004.
* Pemberitahuan perubahan status, apabila disetujui, berkaitan dengan FR-013.
* FR-011 tidak menetapkan autodebit, penghentian mandat pembayaran di gateway, atau pembatalan transaksi yang sedang diproses sebelum mekanismenya dikonfirmasi.

---

## C. Proses Bisnis

| Tahap | Aktor | Aktivitas | Dasar / Catatan |
| :---: | :--- | :--- | :--- |
| **1** | Donatur / pihak berwenang | Memilih kesediaan donasi berulang yang akan dijeda. | Pengelolaan kesediaan tercantum pada SRS/BRS; tampilan dan akses perlu konfirmasi. |
| **2** | Sistem Fitur 4 | Memeriksa keberadaan kesediaan dan hak akses pengguna. | Penjabaran kebutuhan keamanan; aturan peran perlu konfirmasi. |
| **3** | Donatur / pihak berwenang | Mengonfirmasi permintaan jeda sesuai mekanisme yang disediakan. | Konfirmasi tindakan dan alasan jeda belum ditetapkan. |
| **4** | Sistem Fitur 4 | Memperbarui status kesediaan menjadi dijeda. | Sesuai FR-011; nama status final perlu disepakati. |
| **5** | Sistem Fitur 4 | Menyimpan waktu dan referensi perubahan status. | Usulan keterlacakan; format data perlu konfirmasi. |
| **6** | Sistem Fitur 4 | Menerapkan aturan jeda pada jadwal donasi berikutnya sesuai kebijakan. | Kapan jeda berlaku dan perlakuan tagihan berjalan perlu konfirmasi. |

### C.1 Alur Alternatif dan Kondisi Khusus
* **Kesediaan tidak ditemukan atau tidak dapat diakses:** Sistem tidak mengubah status dan menampilkan informasi yang sesuai.
* **Pengguna tidak memiliki kewenangan:** Permintaan jeda ditolak dan status kesediaan tetap.
* **Kesediaan sudah dijeda atau dibatalkan:** Sistem tidak membuat perubahan status yang tidak diperlukan dan memberikan informasi sesuai aturan.
* **Terdapat pembayaran/tagihan yang sedang diproses:** Perlakuannya mengikuti keputusan organisasi dan ketentuan gateway; sistem tidak boleh menganggap transaksi otomatis batal.
* **Permintaan jeda gagal disimpan:** Status lama dipertahankan dan kegagalan dicatat untuk penelusuran.

---

## D. Data, Tipe Data, dan Validasi

| Elemen Data Usulan | Tujuan / Validasi Awal | Status |
| :--- | :--- | :--- |
| **ID kesediaan donasi** | Mengidentifikasi kesediaan donasi berulang yang akan dijeda. | Wajib tersedia; format perlu konfirmasi. |
| **ID donatur** | Menghubungkan kesediaan dengan pemiliknya dan validasi hak akses. | Penggunaan dan format perlu konfirmasi. |
| **Status kesediaan** | Membedakan aktif, dijeda, dan dibatalkan sesuai daftar status final. | Daftar nilai/status perlu konfirmasi. |
| **Waktu permintaan jeda** | Mencatat kapan permintaan diajukan. | Format dan zona waktu perlu konfirmasi. |
| **Waktu efektif jeda** | Menentukan kapan jeda mulai berlaku. | Aturan penetapan perlu konfirmasi. |
| **Pelaku perubahan** | Mencatat donatur atau staf/pihak berwenang yang melakukan tindakan. | Kebutuhan audit dan format perlu konfirmasi. |
| **Alasan jeda** | Informasi tambahan jika organisasi mewajibkan alasan. | Opsional/wajib dan daftar alasan perlu konfirmasi. |

*Catatan: Elemen di atas merupakan usulan kebutuhan informasi, bukan skema basis data final.*

---

## E. Mockup Konseptual

*SRS tidak menetapkan desain layar khusus untuk FR-011. Gambaran konseptual pada halaman pengelolaan donasi berulang dapat memuat:*

| Elemen Tampilan | Keterangan |
| :--- | :--- |
| **Informasi kesediaan** | Program, nominal, jadwal, periode, dan status donasi berulang. |
| **Tindakan jeda** | Pilihan untuk mengajukan jeda pada kesediaan yang memenuhi syarat. |
| **Konfirmasi** | Ringkasan tindakan dan informasi dampak jeda sesuai kebijakan. |
| **Status terbaru** | Informasi bahwa kesediaan telah dijeda atau permintaan gagal. |

*Catatan: Tampilan, istilah status, dan apakah donatur dapat melakukan jeda mandiri atau melalui staf perlu dikonfirmasi. Jika dibuat antarmuka, arahan visual SRS adalah navy blue dan putih.*

---

## F. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Terkait | Acuan / Catatan |
| :--- | :--- | :--- |
| **Keamanan dan hak akses** | Hanya donatur pemilik kesediaan atau pihak berwenang yang dapat mengajukan jeda. | NFR-001; autentikasi dan matriks peran perlu konfirmasi. |
| **Konsistensi data** | Status kesediaan harus diperbarui secara konsisten dan tidak menimbulkan status ganda yang bertentangan. | NFR-005; aturan transisi status perlu disepakati. |
| **Keterlacakan** | Perubahan status dapat ditelusuri berdasarkan identitas kesediaan dan waktu perubahan. | NFR-005; detail audit log perlu konfirmasi. |
| **Kemudahan penggunaan** | Tindakan jeda dan dampaknya disampaikan secara mudah dipahami. | NFR-004; detail UI perlu konfirmasi. |

---

## G. Kriteria Penerimaan
- [ ] Donatur atau pihak berwenang dapat memilih kesediaan donasi berulang yang valid untuk dijeda.
- [ ] Sistem memvalidasi hak akses sebelum mengubah status.
- [ ] Sistem memperbarui status kesediaan menjadi dijeda sesuai aturan yang disepakati.
- [ ] Sistem menyimpan informasi perubahan sehingga dapat ditelusuri.
- [ ] Kesediaan yang tidak ditemukan, tidak dapat diakses, atau sudah dibatalkan tidak diubah secara keliru.
- [ ] Dampak jeda terhadap jadwal/tagihan berikutnya mengikuti kebijakan yang telah disetujui.

*Catatan: Kriteria penerimaan final bergantung pada keputusan mengenai waktu efektif jeda, jadwal pembayaran, dan perlakuan transaksi yang sedang diproses.*

---

## H. Prioritas dan Tingkat Kesulitan

| Komponen | Usulan | Dasar |
| :--- | :--- | :--- |
| **Prioritas MoSCoW** | Should Have — usulan | BR-008 pada BRS memiliki prioritas Sedang; fasilitas jeda mendukung pengelolaan donasi tetapi aturan operasionalnya masih perlu ditetapkan. |
| **Tingkat Kesulitan** | 3 — Medium | Melibatkan perubahan status, validasi hak akses, pencatatan perubahan, dan dampak pada jadwal berikutnya; kompleksitas bergantung pada mekanisme pembayaran yang dipilih. |

### Dasar Pertimbangan Penilaian
Skala kesulitan 1–5: **1–2 Easy**, **3 Medium**, dan **4–5 Hard**. FR-011 diusulkan pada tingkat **3 (Medium)** karena proses utamanya berupa perubahan status kesediaan dengan validasi hak akses dan pencatatan perubahan. Kompleksitas dapat meningkat apabila jeda harus mengubah penjadwalan penagihan atau instruksi pada gateway. Penilaian dan prioritas ini merupakan usulan, bukan persetujuan final klien.

---

## I. Hal yang Perlu Dikonfirmasi kepada Klien
1. Siapa yang boleh menjeda donasi berulang: donatur sendiri, staf, atau keduanya?
2. Apakah jeda berlaku langsung atau mulai pada periode/tagihan berikutnya?
3. Apa yang terjadi pada tagihan yang sudah dibuat, sedang diproses, atau berstatus *pending* ketika jeda diajukan?
4. Apakah donatur wajib mengisi alasan jeda?
5. Apakah jeda memiliki batas waktu atau dapat berlangsung sampai donatur mengaktifkannya kembali?
6. Bagaimana mekanisme mengaktifkan kembali donasi yang dijeda, dan apakah aktivasi kembali termasuk ruang lingkup Fitur 4?
7. Apakah jeda perlu diteruskan ke Payment Gateway Artivisi atau hanya mengubah jadwal pada sistem Fitur 4?
8. Informasi apa yang perlu ditampilkan dan apakah perubahan status memicu pemberitahuan melalui FR-013?
9. Apakah staf memerlukan riwayat jeda dan hak untuk mengubah status?

---

## J. Checklist Konfirmasi Client

| ID & Nama Kebutuhan | Prioritas Usulan | Kesulitan Usulan | Tidak Dibutuhkan / Catatan Client |
| :--- | :--- | :--- | :--- |
| **FR-011 — Menjeda Donasi Berulang** | Should Have — usulan | 3 — Medium | |

*Catatan: Isi kolom terakhir apabila kebutuhan tidak diperlukan atau terdapat catatan/perubahan dari klien. Biarkan kosong jika kebutuhan tetap diperlukan.*

---

## K. Catatan dan Status Dokumen
FR-011 diturunkan dari kebutuhan SRS untuk memungkinkan donatur atau pihak berwenang menjeda kesediaan donasi sesuai aturan yang disepakati, serta BR-008 pada BRS. Dokumen ini tidak menetapkan bahwa jeda otomatis membatalkan tagihan yang sedang berjalan atau menghentikan mandat autodebit. Ketentuan waktu efektif, pihak yang berwenang, aktivasi kembali, dan dampak pada transaksi berjalan masih memerlukan validasi.  
**Status:** Draft untuk Review dan Validasi Klien; belum menjadi baseline sebelum disetujui.