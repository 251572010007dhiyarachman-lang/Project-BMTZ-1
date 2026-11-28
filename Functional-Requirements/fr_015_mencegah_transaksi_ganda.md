# BAITULMAL TAZKIA
## SISTEM DONASI BERULANG DAN KANAL PEMBAYARAN DIGITAL

### FUNCTIONAL REQUIREMENT (FR)
# FR-015: MENCEGAH TRANSAKSI GANDA

**Versi:** 1.0 | **Status:** Draft untuk Review dan Validasi Klien | **Tanggal:** 25 November 2026  
**Acuan:** SRS dan BRS Fitur 4 versi 1.0, tanggal acuan 14 November 2026.

---

## A. Identitas Kebutuhan

| Informasi | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-015 |
| **Nama Kebutuhan** | Mencegah Transaksi Ganda |
| **Aktor Utama** | Donatur; sistem; Payment Gateway; staf internal yang berwenang. |
| **Tujuan** | Mengurangi risiko pemrosesan ulang atau pengiriman ulang yang menghasilkan pencatatan transaksi donasi secara ganda. |
| **Pemicu** | Permintaan pembayaran atau pengiriman/pencatatan data transaksi dilakukan, termasuk ketika terjadi pengulangan permintaan. |
| **Kondisi Awal** | Setiap permintaan atau transaksi memiliki referensi yang dapat digunakan untuk penelusuran; format referensi dan mekanisme idempotensi perlu disepakati. |
| **Prioritas Usulan** | Must Have — usulan, perlu persetujuan Baitulmal Tazkia. |
| **Tingkat Kesulitan Usulan** | 4 — Hard |
| **Status** | Draft untuk review dan validasi; belum menjadi baseline implementasi. |

---

## B. Deskripsi Functional Requirement

FR-015 menjelaskan penggunaan referensi transaksi atau mekanisme idempotensi agar pemrosesan ulang tidak menghasilkan pencatatan transaksi ganda. Sistem memeriksa apakah permintaan yang diterima merupakan permintaan baru atau pengulangan dari transaksi yang sama. Jika dikenali sebagai pengulangan, sistem tidak membuat transaksi/catatan pembayaran baru yang duplikat dan tetap mempertahankan referensi transaksi yang dapat ditelusuri. Kunci idempotensi, ruang lingkup pemeriksaan, masa penyimpanan, dan penanganan kondisi bersamaan belum dirinci dalam SRS.

### 1. Format Outline dan Batasan
* Sistem menggunakan referensi transaksi atau mekanisme identifikasi unik untuk mengenali permintaan.
* Sebelum membuat catatan baru, sistem memeriksa apakah referensi atau kunci permintaan sudah pernah diproses.
* Jika permintaan merupakan pengulangan transaksi yang sama, sistem tidak membuat catatan transaksi baru yang duplikat.
* Sistem mempertahankan hasil/referensi transaksi sebelumnya agar permintaan ulang dapat ditelusuri.
* Pengiriman ulang akibat kegagalan integrasi harus ditangani tanpa menggandakan catatan transaksi.

### 2. Proses Bisnis

| Tahap | Aktivitas | Dasar / Catatan |
| :---: | :--- | :--- |
| **1** | Permintaan pembayaran atau pencatatan transaksi diterima sistem. | SRS FR-015; titik pemeriksaan rinci perlu konfirmasi. |
| **2** | Sistem membaca referensi transaksi atau kunci identifikasi permintaan. | Format dan pembentuk referensi perlu disepakati. |
| **3** | Sistem memeriksa apakah referensi/kunci tersebut sudah pernah diproses. | Aturan cakupan pemeriksaan perlu konfirmasi. |
| **4** | Jika belum pernah diproses, sistem melanjutkan proses sesuai alur terkait dan menyimpan referensinya. | Selaras dengan FR-006/FR-007 dan NFR-005. |
| **5** | Jika sudah pernah diproses, sistem mencegah pembuatan catatan duplikat dan mengembalikan/menampilkan hasil yang dapat ditelusuri. | Perilaku respons untuk permintaan ulang perlu konfirmasi. |

> **Alur Alternatif:** Jika permintaan ulang terjadi karena *timeout* atau respons gateway belum diterima, sistem tidak boleh langsung menganggap permintaan sebagai transaksi baru tanpa pemeriksaan referensi. Jika status transaksi pertama belum diketahui, sistem mempertahankan status tersebut untuk ditelusuri dan mengikuti prosedur pemeriksaan yang disepakati. Mekanisme teknis untuk kondisi dua permintaan bersamaan juga perlu ditetapkan.

### 3. Field, Tipe Data, dan Validasi

| Field / Informasi | Tipe / Bentuk | Validasi / Aturan Awal | Status |
| :--- | :--- | :--- | :--- |
| **Referensi transaksi** | String/ID unik | Digunakan untuk menelusuri transaksi yang sama. | Format/pembentuk perlu konfirmasi. |
| **Kunci idempotensi** | String/token (jika digunakan) | Permintaan dengan kunci sama tidak menghasilkan proses/catatan ganda. | Penggunaan dan masa berlaku perlu konfirmasi. |
| **Status pemrosesan** | Kode status | Membedakan belum diproses, sedang diproses, selesai, atau gagal sesuai daftar status final. | Daftar status perlu konfirmasi. |
| **Waktu permintaan** | Tanggal dan waktu | Membantu penelusuran permintaan awal dan pengulangan. | Zona waktu/format perlu disepakati. |
| **Hasil pemeriksaan duplikasi** | Status/indikator | Menandai permintaan baru atau pengulangan. | Aturan hasil perlu konfirmasi. |

### 4. Mockup Konseptual

```text
+-------------------------------------------------------+
| PEMERIKSAAN TRANSAKSI                                 |
+-------------------------------------------------------+
| Referensi transaksi : [ ID / kunci permintaan       ] |
| Status pemeriksaan  : [ permintaan baru / sudah     ] |
|                       [ pernah diproses             ] |
|                                                       |
| Jika sudah pernah diproses:                           |
| [ Gunakan referensi dan hasil transaksi yang sama   ] |
| Catatan: tidak membuat catatan transaksi duplikat.    |
+-------------------------------------------------------+
```
*Catatan: Mockup ini konseptual, bukan desain UI final. Arahan visual SRS NFR-006 adalah navy blue dan putih.*

### 5. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Terkait | Catatan |
| :--- | :--- | :--- |
| **Keamanan** | Referensi/kunci tidak boleh membuka data transaksi kepada pihak yang tidak berwenang. | Mengacu NFR-001. |
| **Keandalan** | Pengulangan permintaan tidak boleh menyebabkan status pembayaran keliru atau transaksi ganda. | Mengacu NFR-002. |
| **Integrasi** | Pemeriksaan harus konsisten dengan mekanisme integrasi gateway dan modul penerima yang disepakati. | Mengacu NFR-003. |
| **Konsistensi Data** | Transaksi memiliki referensi yang dapat digunakan untuk penelusuran dan pencocokan. | Mengacu NFR-005. |
| **Pemulihan Kegagalan** | Pengiriman ulang setelah kegagalan tidak menghasilkan pencatatan ganda. | Mengacu NFR-007. |

### 6. Kriteria Penerimaan
- [ ] Setiap transaksi/permintaan yang diproses memiliki referensi atau mekanisme identifikasi yang disepakati.
- [ ] Sistem dapat mengenali permintaan yang merupakan pengulangan dari transaksi yang sama.
- [ ] Permintaan pengulangan tidak menghasilkan catatan transaksi atau pembayaran baru yang duplikat.
- [ ] Referensi dan hasil transaksi sebelumnya tetap dapat ditelusuri.
- [ ] Pengiriman ulang akibat kegagalan integrasi tidak menggandakan catatan transaksi.
- [ ] Status pembayaran tetap mengikuti hasil verifikasi FR-007; pencegahan duplikasi tidak boleh mengubah status menjadi berhasil tanpa verifikasi.

### 7. Prioritas dan Tingkat Kesulitan

| Komponen | Usulan | Dasar |
| :--- | :--- | :--- |
| **Prioritas MoSCoW** | Must Have — usulan, perlu persetujuan Baitulmal Tazkia. | Usulan analisis berdasarkan tujuan dan kebutuhan pada SRS; perlu persetujuan BMT. |
| **Tingkat Kesulitan** | 4 — Hard | FR-015 diusulkan pada tingkat 4 (Hard) karena perlu konsistensi pemeriksaan referensi pada proses pembayaran dan pertukaran data, termasuk penanganan *timeout*, *retry*, serta kemungkinan permintaan bersamaan. Prioritas *Must Have* diusulkan karena pencegahan transaksi ganda merupakan kebutuhan penting untuk menjaga keandalan dan konsistensi data, selaras dengan tujuan SRS dan NFR-005 serta NFR-007. Mekanisme teknis tetap perlu dipilih bersama tim teknis. |

### 8. Dasar Pertimbangan Penilaian
Skala kesulitan 1–5: **1–2 Easy**, **3 Medium**, dan **4–5 Hard**. FR-015 diusulkan pada tingkat **4 (Hard)** karena perlu konsistensi pemeriksaan referensi pada proses pembayaran dan pertukaran data, termasuk penanganan *timeout*, *retry*, serta kemungkinan permintaan bersamaan. Prioritas *Must Have* diusulkan karena pencegahan transaksi ganda merupakan kebutuhan penting untuk menjaga keandalan dan konsistensi data, selaras dengan tujuan SRS dan NFR-005 serta NFR-007. Mekanisme teknis tetap perlu dipilih bersama tim teknis. Penilaian prioritas dan kesulitan merupakan usulan, bukan keputusan final klien.

### 9. Hal yang Perlu Dikonfirmasi kepada Klien / Tim Teknis
1. Di tahap mana pencegahan transaksi ganda harus diterapkan: saat membuat permintaan pembayaran, menerima respons gateway, memperbarui status, atau mengirim data ke modul lain?
2. Apakah Payment Gateway Artivisi menyediakan referensi unik atau *idempotency key*? Jika ya, bagaimana format dan aturan penggunaannya?
3. Siapa yang membentuk referensi transaksi: sistem Fitur 4 atau gateway?
4. Apakah satu donasi berulang memiliki satu referensi tetap atau setiap jadwal pembayaran memiliki referensi transaksi tersendiri?
5. Bagaimana sistem menangani permintaan ulang ketika permintaan pertama *timeout* tetapi gateway mungkin sudah memproses pembayaran?
6. Berapa lama referensi/kunci idempotensi harus disimpan dan kapan boleh digunakan kembali?
7. Bagaimana menangani dua permintaan yang sama yang masuk hampir bersamaan?
8. Apakah pemeriksaan duplikasi juga berlaku pada pengiriman data ke modul tanda terima FR-008, catatan donasi FR-009, dan pelaporan/rekonsiliasi FR-010?
9. Bagaimana transaksi dari tautan pembayaran satu kali FR-014 diperiksa agar tidak tercatat dua kali?
10. Jika ada transaksi yang benar-benar berbeda tetapi nominal, waktu, dan donaturnya sama, aturan apa yang membedakannya dari transaksi duplikat?
11. Bagaimana pencatatan log dan proses pemulihan jika pemeriksaan duplikasi gagal atau layanan integrasi tidak tersedia?

### 10. Checklist Konfirmasi Client

| ID & Nama Kebutuhan | Prioritas Usulan | Kesulitan Usulan | Tidak Dibutuhkan / Catatan Client |
| :--- | :--- | :--- | :--- |
| **FR-015 — Mencegah Transaksi Ganda** | Must Have — usulan, perlu persetujuan Baitulmal Tazkia. | 4 — Hard | |

*Catatan: Isi kolom terakhir apabila kebutuhan tidak diperlukan atau terdapat catatan/perubahan dari klien. Biarkan kosong jika kebutuhan tetap diperlukan.*

### 11. Catatan dan Status Dokumen
FR-015 berfokus pada pencegahan pemrosesan atau pencatatan transaksi ganda, bukan pada verifikasi status pembayaran (FR-007) maupun rekonsiliasi/settlement (tanggung jawab fitur terkait). Referensi transaksi atau idempotensi disebut secara eksplisit dalam SRS, tetapi implementasi teknis, cakupan, masa simpan kunci, dan aturan *retry* belum ditetapkan. Seluruh detail tersebut perlu divalidasi bersama BMT dan tim teknis.  
**Status:** Draft untuk Review dan Validasi Klien.