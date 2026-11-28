# BAITULMAL TAZKIA
## SISTEM DONASI BERULANG DAN KANAL PEMBAYARAN DIGITAL

### FUNCTIONAL REQUIREMENT (FR)
# FR-013: MENGIRIM PEMBERITAHUAN STATUS DONASI

**Versi:** 1.0 | **Status:** Draft untuk Review dan Validasi Klien | **Tanggal:** 25 November 2026  
**Acuan:** SRS dan BRS Fitur 4 versi 1.0, tanggal acuan 14 November 2026.

---

## A. Identitas Kebutuhan

| Informasi | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-013 |
| **Nama Kebutuhan** | Mengirim Pemberitahuan Status Donasi |
| **Aktor Utama** | Donatur; sistem; staf internal (jika memiliki hak akses dan disepakati). |
| **Tujuan** | Memberikan informasi kepada donatur mengenai status donasi dan pembayaran melalui mekanisme komunikasi yang disetujui. |
| **Pemicu** | Terjadi perubahan atau kondisi status donasi/pembayaran yang menurut aturan perlu diberitahukan. |
| **Kondisi Awal** | Data donasi atau transaksi tersedia dan statusnya telah diperoleh dari proses terkait; aturan pemicu pemberitahuan telah disepakati. |
| **Prioritas Usulan** | Should Have — usulan, perlu persetujuan Baitulmal Tazkia. |
| **Tingkat Kesulitan Usulan** | 3 — Medium |
| **Status** | Draft untuk review dan validasi; belum menjadi baseline implementasi. |

---

## B. Deskripsi Functional Requirement

FR-013 menjelaskan penyediaan dan pengiriman pemberitahuan kepada donatur terkait status donasi atau pembayaran. Sistem menggunakan informasi status dari proses terkait, terutama hasil verifikasi transaksi pada FR-007, kemudian menyampaikan informasi sesuai kanal dan aturan komunikasi yang disetujui. Kanal, daftar status yang diberitahukan, isi pesan, dan waktu pengiriman belum ditetapkan secara rinci dalam SRS sehingga harus dikonfirmasi.

### 1. Format Outline dan Batasan
* Sistem menentukan apakah suatu status donasi/pembayaran memerlukan pemberitahuan berdasarkan aturan yang disepakati.
* Sistem menyiapkan informasi pemberitahuan berdasarkan status transaksi/donasi yang tersedia.
* Sistem mengirim atau menyediakan pemberitahuan melalui kanal komunikasi yang disetujui.
* Sistem mencatat hasil pengiriman atau kegagalan agar dapat ditelusuri.
* Pemberitahuan tidak boleh menyatakan pembayaran berhasil jika status belum terverifikasi.

### 2. Proses Bisnis

| Tahap | Aktivitas | Dasar / Catatan |
| :---: | :--- | :--- |
| **1** | Perubahan/kondisi status donasi atau pembayaran teridentifikasi. | SRS FR-013; daftar pemicu perlu konfirmasi. |
| **2** | Sistem memeriksa status dan menentukan apakah pemberitahuan perlu dikirim. | Mengacu FR-007 dan aturan komunikasi yang akan disepakati. |
| **3** | Sistem menyiapkan isi pemberitahuan sesuai jenis status. | Isi/template pesan perlu konfirmasi. |
| **4** | Sistem mengirim pemberitahuan melalui kanal yang disetujui. | Kanal komunikasi belum ditetapkan. |
| **5** | Sistem mencatat hasil pengiriman untuk penelusuran. | Selaras dengan kebutuhan keandalan; detail log perlu konfirmasi. |

> **Alur Alternatif:** Jika status masih *pending*, tidak diketahui, atau belum diverifikasi, sistem tidak boleh mengirim pesan yang menyatakan pembayaran berhasil. Jika pengiriman gagal, sistem mencatat kegagalan; percobaan ulang hanya dilakukan apabila aturan *retry* telah disepakati.

### 3. Field, Tipe Data, dan Validasi

| Field / Informasi | Tipe / Bentuk | Validasi / Aturan Awal | Status |
| :--- | :--- | :--- | :--- |
| **Penerima** | Identitas/kontak donatur | Harus merujuk donatur yang terkait dengan transaksi; sumber dan validitas kontak perlu disepakati. | Perlu konfirmasi. |
| **Jenis status** | Kode/kategori status | Hanya status yang disepakati yang memicu pemberitahuan. | Perlu konfirmasi. |
| **Isi pesan** | Teks | Informasi harus sesuai status dan tidak menyesatkan. | Perlu konfirmasi. |
| **Kanal pengiriman** | Kanal komunikasi | Contoh kanal belum ditetapkan oleh SRS; tidak diasumsikan WhatsApp, email, atau SMS. | Perlu konfirmasi. |
| **Waktu pengiriman** | Tanggal dan waktu | Mengikuti aturan waktu/pemicu yang disepakati. | Perlu konfirmasi. |
| **Hasil pengiriman** | Status dan catatan respons | Mencatat berhasil/gagal jika fasilitas kanal mendukung. | Perlu konfirmasi. |

### 4. Mockup Konseptual

```text
+-------------------------------------------------------+
| PEMBERITAHUAN STATUS DONASI                           |
+-------------------------------------------------------+
| Status donasi/pembayaran : [ status terverifikasi   ] |
| Informasi                : [ isi pesan sesuai status] |
| Kanal                    : [ kanal yang disetujui   ] |
| Hasil pengiriman         : [ berhasil / gagal /     ] |
|                            [ belum diketahui        ] |
+-------------------------------------------------------+
```
*Catatan: Mockup ini konseptual, bukan desain UI final. Arahan visual SRS NFR-006 adalah navy blue dan putih.*

### 5. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Terkait | Catatan |
| :--- | :--- | :--- |
| **Keamanan** | Data kontak dan transaksi dilindungi dari akses tidak berwenang. | Mengacu NFR-001. |
| **Keandalan** | Pesan tidak menyatakan pembayaran berhasil sebelum status diverifikasi. | Mengacu NFR-002. |
| **Integrasi** | Pengiriman melalui kanal/layanan yang disepakati. | Mengacu NFR-003; kanal belum dipilih. |
| **Konsistensi Data** | Pemberitahuan merujuk transaksi/donasi yang tepat. | Mengacu NFR-005. |
| **Pemulihan Kegagalan** | Kegagalan pengiriman dapat ditelusuri. | Mengacu NFR-007; kebijakan *retry* perlu konfirmasi. |

### 6. Kriteria Penerimaan
- [ ] Sistem dapat mengidentifikasi kondisi status yang memerlukan pemberitahuan sesuai aturan yang telah disepakati.
- [ ] Isi pemberitahuan sesuai dengan status donasi/pembayaran yang menjadi sumbernya.
- [ ] Sistem hanya menyampaikan keberhasilan pembayaran setelah status diverifikasi.
- [ ] Pemberitahuan dikirim melalui kanal yang telah disetujui.
- [ ] Hasil pengiriman atau kegagalan dapat ditelusuri sesuai kemampuan kanal yang digunakan.

### 7. Prioritas dan Tingkat Kesulitan

| Komponen | Usulan | Dasar |
| :--- | :--- | :--- |
| **Prioritas MoSCoW** | Should Have — usulan, perlu persetujuan Baitulmal Tazkia. | Usulan analisis berdasarkan tujuan dan kebutuhan pada SRS; perlu persetujuan BMT. |
| **Tingkat Kesulitan** | 3 — Medium | FR-013 diusulkan pada tingkat 3 (Medium) karena mencakup penentuan pemicu, penyusunan pesan, pengiriman melalui kanal, dan pencatatan hasil. Kompleksitas dapat meningkat jika diperlukan beberapa kanal, template dinamis, antrean, atau *retry*. Prioritas *Should Have* merupakan usulan karena pemberitahuan membantu transparansi kepada donatur, tetapi mekanisme komunikasinya masih perlu disepakati. |

### 8. Dasar Pertimbangan Penilaian
Skala kesulitan 1–5: **1–2 Easy**, **3 Medium**, dan **4–5 Hard**. FR-013 diusulkan pada tingkat **3 (Medium)** karena mencakup penentuan pemicu, penyusunan pesan, pengiriman melalui kanal, dan pencatatan hasil. Kompleksitas dapat meningkat jika diperlukan beberapa kanal, template dinamis, antrean, atau *retry*. Prioritas *Should Have* merupakan usulan karena pemberitahuan membantu transparansi kepada donatur, tetapi mekanisme komunikasinya masih perlu disepakati. Penilaian prioritas dan kesulitan merupakan usulan, bukan keputusan final klien.

### 9. Hal yang Perlu Dikonfirmasi kepada Klien / Tim Teknis
1. Status apa saja yang harus diberitahukan kepada donatur (misalnya berhasil, gagal, *pending*, donasi dijeda, atau dibatalkan)?
2. Peristiwa apa yang menjadi pemicu pemberitahuan: perubahan status transaksi, perubahan status donasi berulang, atau keduanya?
3. Kanal apa yang akan digunakan (WhatsApp, email, SMS, notifikasi aplikasi, atau kanal lain)?
4. Siapa penyedia layanan/akun pengiriman dan siapa yang bertanggung jawab atas biaya kanal?
5. Apakah isi pesan menggunakan template yang disediakan BMT? Siapa yang menyetujui isi pesannya?
6. Kapan pesan dikirim: langsung setelah status berubah atau secara terjadwal?
7. Apakah sistem perlu mencatat status terkirim, gagal, dibaca, atau hanya respons dari layanan pengiriman?
8. Jika pengiriman gagal, apakah perlu *retry*? Berapa kali dan dengan jeda berapa lama?
9. Bagaimana pemberitahuan untuk status *pending* atau status yang berubah setelah pemberitahuan awal?
10. Apakah pemberitahuan untuk jeda/pembatalan donasi berulang termasuk FR-013 dan bagaimana kaitannya dengan FR-011 serta FR-012?

### 10. Checklist Konfirmasi Client

| ID & Nama Kebutuhan | Prioritas Usulan | Kesulitan Usulan | Tidak Dibutuhkan / Catatan Client |
| :--- | :--- | :--- | :--- |
| **FR-013 — Mengirim Pemberitahuan Status Donasi** | Should Have — usulan, perlu persetujuan Baitulmal Tazkia. | 3 — Medium | |

*Catatan: Isi kolom terakhir apabila kebutuhan tidak diperlukan atau terdapat catatan/perubahan dari klien. Biarkan kosong jika kebutuhan tetap diperlukan.*

### 11. Catatan dan Status Dokumen
FR-013 berfokus pada pemberitahuan status donasi/pembayaran. FR-005 tetap berfokus pada pengingat pembayaran sesuai jadwal, sedangkan FR-013 menyampaikan informasi status/perubahan. FR-013 tidak melakukan verifikasi pembayaran (FR-007) dan tidak menggantikan pengelolaan jeda atau pembatalan (FR-011/FR-012). Kanal, template, daftar status, dan kebijakan *retry* belum ditetapkan dalam SRS dan harus dikonfirmasi.  
**Status:** Draft untuk Review dan Validasi Klien.