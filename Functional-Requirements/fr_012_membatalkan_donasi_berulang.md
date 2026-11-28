# BAITULMAL TAZKIA
## SISTEM DONASI BERULANG DAN KANAL PEMBAYARAN DIGITAL

### FUNCTIONAL REQUIREMENT (FR)
# FR-012: MEMBATALKAN DONASI BERULANG

**Versi:** 1.0 | **Status:** Draft untuk Review dan Validasi Klien | **Tanggal:** 25 November 2026  
**Acuan:** SRS dan BRS Fitur 4 versi 1.0, tanggal acuan 14 November 2026.

---

## A. Identitas Kebutuhan

| Informasi | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-012 |
| **Nama Kebutuhan** | Membatalkan Donasi Berulang |
| **Aktor Utama** | Donatur; staf internal Baitulmal Tazkia atau pihak berwenang sesuai hak akses; Sistem Fitur 4. |
| **Tujuan** | Memungkinkan pembatalan kesediaan donasi berulang sesuai ketentuan yang ditetapkan organisasi dan mencatat perubahan statusnya. |
| **Pemicu** | Donatur atau pihak berwenang mengajukan pembatalan atas kesediaan donasi berulang. |
| **Kondisi Awal** | Data kesediaan donasi tersedia dan dapat diidentifikasi; pengguna memiliki hak untuk melakukan pembatalan. |
| **Prioritas Usulan** | Should Have — usulan, mengikuti BR-008 yang berprioritas Sedang; perlu persetujuan klien. |
| **Tingkat Kesulitan Usulan** | 3 — Medium |
| **Status** | Draft untuk review dan validasi; sifat pembatalan, waktu efektif, dampak terhadap transaksi berjalan, dan konsekuensi pada gateway belum ditetapkan. |

---

## B. Deskripsi Functional Requirement

Sistem memungkinkan donatur atau pihak berwenang membatalkan kesediaan donasi berulang sesuai ketentuan yang berlaku. Ketika permintaan pembatalan diajukan, sistem memeriksa kesediaan donasi yang dipilih dan kewenangan pengguna. Jika memenuhi ketentuan, sistem memperbarui status kesediaan menjadi dibatalkan dan menyimpan informasi perubahan untuk keperluan penelusuran. Pembatalan mengatur keberlanjutan kesediaan donasi berulang; perlakuan terhadap transaksi yang telah dibuat, sedang diproses, atau telah berhasil mengikuti kebijakan organisasi dan ketentuan layanan pembayaran yang perlu dikonfirmasi.

* **Pemicu:** Permintaan pembatalan kesediaan donasi berulang.
* **Kondisi Awal:** Kesediaan tersedia dan pengguna berwenang.
* **Hasil yang Diharapkan:** Status pembatalan tercatat dan dapat ditelusuri.

### B.1 Batasan Ruang Lingkup
* FR-012 membahas pembatalan kesediaan donasi berulang, bukan pengembalian dana atas transaksi yang telah berhasil.
* Menjeda donasi sementara dibahas pada FR-011 dan tidak sama dengan pembatalan.
* Pengaturan kesediaan awal berada pada FR-003/FR-004; pemberitahuan perubahan status, apabila disetujui, berkaitan dengan FR-013.
* FR-012 tidak mengasumsikan adanya autodebit atau pembatalan otomatis pada Payment Gateway Artivisi sebelum dukungan dan prosedurnya dikonfirmasi.
* Transaksi yang telah berhasil, *pending*, atau sedang diproses tidak otomatis dihapus atau dibatalkan oleh perubahan status kesediaan.

---

## C. Proses Bisnis

| Tahap | Aktor | Aktivitas | Dasar / Catatan |
| :---: | :--- | :--- | :--- |
| **1** | Donatur / pihak berwenang | Memilih kesediaan donasi berulang yang akan dibatalkan. | Pengelolaan kesediaan tercantum pada SRS/BRS; tampilan dan akses perlu konfirmasi. |
| **2** | Sistem Fitur 4 | Memeriksa keberadaan kesediaan dan hak akses pengguna. | Penjabaran kebutuhan keamanan; aturan peran perlu konfirmasi. |
| **3** | Donatur / pihak berwenang | Mengonfirmasi permintaan pembatalan sesuai mekanisme yang disediakan. | Konfirmasi dan kemungkinan alasan pembatalan perlu konfirmasi. |
| **4** | Sistem Fitur 4 | Memvalidasi bahwa kesediaan memenuhi ketentuan pembatalan. | Ketentuan pembatalan ditetapkan organisasi. |
| **5** | Sistem Fitur 4 | Memperbarui status kesediaan menjadi dibatalkan. | Sesuai FR-012; nama status dan sifat final perlu konfirmasi. |
| **6** | Sistem Fitur 4 | Menyimpan waktu dan pelaku perubahan serta referensi kesediaan. | Usulan keterlacakan; format data perlu konfirmasi. |
| **7** | Sistem Fitur 4 / pihak terkait | Menerapkan dampak pembatalan pada jadwal berikutnya dan proses pembayaran sesuai aturan yang disepakati. | Waktu efektif dan mekanisme gateway belum ditetapkan. |

### C.1 Alur Alternatif dan Kondisi Khusus
* **Kesediaan tidak ditemukan atau tidak dapat diakses:** Sistem tidak mengubah status dan memberikan informasi yang sesuai.
* **Pengguna tidak memiliki kewenangan:** Pembatalan ditolak dan status kesediaan tetap.
* **Kesediaan sudah dibatalkan:** Sistem tidak mengulang perubahan yang tidak diperlukan dan memberikan informasi sesuai aturan.
* **Terdapat transaksi yang sedang diproses atau berstatus pending:** Sistem mempertahankan catatan transaksi dan menerapkan perlakuan sesuai kebijakan yang dikonfirmasi.
* **Transaksi telah berhasil sebelum pembatalan:** Pembatalan kesediaan tidak otomatis membatalkan transaksi atau memicu pengembalian dana.
* **Permintaan pembatalan gagal disimpan:** Status sebelumnya dipertahankan dan kegagalan dicatat.

---

## D. Data, Tipe Data, dan Validasi

| Elemen Data Usulan | Tujuan / Validasi Awal | Status |
| :--- | :--- | :--- |
| **ID kesediaan donasi** | Mengidentifikasi kesediaan donasi yang dibatalkan. | Wajib tersedia; format perlu konfirmasi. |
| **ID donatur** | Memastikan kesediaan terkait dengan pemiliknya. | Penggunaan dan format perlu konfirmasi. |
| **Status kesediaan** | Membedakan aktif, dijeda, dan dibatalkan. | Daftar nilai/status final perlu konfirmasi. |
| **Waktu permintaan pembatalan** | Mencatat kapan pembatalan diajukan. | Format dan zona waktu perlu konfirmasi. |
| **Waktu efektif pembatalan** | Menentukan kapan pembatalan mulai berlaku. | Aturan penetapan perlu konfirmasi. |
| **Pelaku perubahan** | Mencatat donatur atau staf/pihak berwenang yang melakukan tindakan. | Kebutuhan audit dan format perlu konfirmasi. |
| **Alasan pembatalan** | Informasi tambahan jika organisasi mewajibkan alasan. | Opsional/wajib dan daftar alasan perlu konfirmasi. |
| **Referensi transaksi terkait** | Membantu mengidentifikasi transaksi yang sudah dibuat/berjalan sebelum pembatalan. | Cakupan dan relasi data perlu konfirmasi. |

*Catatan: Elemen di atas merupakan usulan kebutuhan informasi, bukan skema basis data final.*

---

## E. Mockup Konseptual

*SRS tidak menetapkan desain layar khusus untuk FR-012. Gambaran konseptual pada halaman pengelolaan donasi berulang dapat memuat:*

| Elemen Tampilan | Keterangan |
| :--- | :--- |
| **Informasi kesediaan** | Program, nominal, jadwal, periode, dan status donasi berulang. |
| **Tindakan pembatalan** | Pilihan untuk mengajukan pembatalan pada kesediaan yang memenuhi syarat. |
| **Konfirmasi pembatalan** | Ringkasan kesediaan yang akan dibatalkan dan informasi dampaknya sesuai kebijakan. |
| **Status terbaru** | Informasi bahwa kesediaan telah dibatalkan atau permintaan gagal. |

*Catatan: Tampilan, istilah status, dan apakah pembatalan dapat dilakukan mandiri oleh donatur atau harus melalui staf perlu dikonfirmasi. Jika dibuat antarmuka, arahan visual SRS adalah navy blue dan putih.*

---

## F. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Terkait | Acuan / Catatan |
| :--- | :--- | :--- |
| **Keamanan dan hak akses** | Hanya donatur pemilik kesediaan atau pihak berwenang yang dapat mengajukan pembatalan. | NFR-001; autentikasi dan matriks peran perlu konfirmasi. |
| **Konsistensi data** | Status pembatalan harus konsisten dan tidak menghapus riwayat transaksi. | NFR-005; aturan retensi dan relasi data perlu disepakati. |
| **Keterlacakan** | Pembatalan dapat ditelusuri berdasarkan ID kesediaan, waktu, dan pelaku perubahan. | NFR-005; detail audit log perlu konfirmasi. |
| **Keandalan transaksi** | Pembatalan kesediaan tidak boleh mengubah transaksi menjadi gagal atau membatalkan transaksi berhasil tanpa proses yang sah. | NFR-002; aturan transaksi berjalan perlu konfirmasi. |

---

## G. Kriteria Penerimaan
- [ ] Donatur atau pihak berwenang dapat memilih kesediaan donasi berulang yang valid untuk dibatalkan.
- [ ] Sistem memvalidasi hak akses dan ketentuan pembatalan sebelum mengubah status.
- [ ] Sistem memperbarui status kesediaan menjadi dibatalkan dan menyimpan waktu serta pelaku perubahan.
- [ ] Riwayat transaksi yang telah terjadi tetap dapat ditelusuri.
- [ ] Kesediaan yang tidak ditemukan, tidak dapat diakses, atau sudah dibatalkan tidak diubah secara keliru.
- [ ] Dampak pembatalan terhadap jadwal berikutnya dan transaksi yang sedang diproses mengikuti kebijakan yang telah disetujui.
- [ ] Pembatalan kesediaan tidak otomatis diperlakukan sebagai pengembalian dana transaksi yang telah berhasil.

*Catatan: Kriteria penerimaan final bergantung pada keputusan mengenai sifat pembatalan, waktu efektif, dan perlakuan terhadap transaksi berjalan.*

---

## H. Prioritas dan Tingkat Kesulitan

| Komponen | Usulan | Dasar |
| :--- | :--- | :--- |
| **Prioritas MoSCoW** | Should Have — usulan | BR-008 pada BRS memiliki prioritas Sedang dan menggabungkan kebutuhan jeda atau pembatalan donasi berulang; perlu persetujuan klien. |
| **Tingkat Kesulitan** | 3 — Medium | Melibatkan validasi hak akses, perubahan status, penyimpanan riwayat, dan pengaturan dampak pada jadwal/transaksi berikutnya. |

### Dasar Pertimbangan Penilaian
Skala kesulitan 1–5: **1–2 Easy**, **3 Medium**, dan **4–5 Hard**. FR-012 diusulkan pada tingkat **3 (Medium)** karena proses utamanya berupa validasi dan perubahan status kesediaan. Kompleksitas dapat meningkat jika pembatalan harus disinkronkan dengan layanan pembayaran atau mengubah tagihan yang sudah dibuat. Prioritas dan tingkat kesulitan ini merupakan usulan, bukan persetujuan final klien.

---

## I. Hal yang Perlu Dikonfirmasi kepada Klien
1. Siapa yang boleh membatalkan donasi berulang: donatur sendiri, staf, atau keduanya?
2. Apakah pembatalan berlaku langsung atau pada periode/tagihan berikutnya?
3. Apakah pembatalan bersifat permanen, atau donatur dapat membuat kesediaan baru setelahnya?
4. Apa yang terjadi pada tagihan yang sudah dibuat, sedang diproses, atau berstatus *pending* ketika pembatalan dilakukan?
5. Apakah pembatalan perlu diteruskan ke Payment Gateway Artivisi untuk menghentikan instruksi/mandat pembayaran berikutnya?
6. Apakah alasan pembatalan wajib dicatat?
7. Apakah transaksi yang sudah berhasil tetap tercatat dan tidak berubah ketika kesediaan dibatalkan?
8. Apakah pembatalan memicu pemberitahuan kepada donatur melalui FR-013?
9. Apakah staf memerlukan riwayat pembatalan dan kewenangan untuk melakukan pembatalan atas nama donatur?

---

## J. Checklist Konfirmasi Client

| ID & Nama Kebutuhan | Prioritas Usulan | Kesulitan Usulan | Tidak Dibutuhkan / Catatan Client |
| :--- | :--- | :--- | :--- |
| **FR-012 — Membatalkan Donasi Berulang** | Should Have — usulan | 3 — Medium | |

*Catatan: Isi kolom terakhir apabila kebutuhan tidak diperlukan atau terdapat catatan/perubahan dari klien. Biarkan kosong jika kebutuhan tetap diperlukan.*

---

## K. Catatan dan Status Dokumen
FR-012 diturunkan dari kebutuhan SRS untuk memungkinkan pembatalan kesediaan donasi berulang sesuai ketentuan yang berlaku, serta BR-008 pada BRS. Dokumen ini membedakan pembatalan kesediaan dari jeda sementara dan pengembalian dana. Sifat pembatalan, waktu efektif, pihak yang berwenang, serta dampaknya terhadap transaksi berjalan dan layanan pembayaran masih memerlukan validasi.  
**Status:** Draft untuk Review dan Validasi Klien; belum menjadi baseline sebelum disetujui.