# BAITULMAL TAZKIA
## SISTEM DONASI BERULANG DAN KANAL PEMBAYARAN DIGITAL

### FUNCTIONAL REQUIREMENT (FR)
# FR-005: MENGIRIM PENGINGAT PEMBAYARAN

**Versi:** 1.0 | **Status:** Draft untuk Review dan Validasi Klien | **Tanggal:** 25 November 2026  
**Acuan:** SRS dan BRS Fitur 4 versi 1.0, tanggal acuan 14 November 2026.

---

## A. Identitas Kebutuhan

| Informasi | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-005 |
| **Nama Kebutuhan** | Mengirim Pengingat Pembayaran |
| **Aktor Utama** | Sistem; donatur sebagai penerima pengingat. |
| **Tujuan** | Menyediakan pengiriman pengingat pembayaran donasi berulang kepada donatur sesuai jadwal dan kanal yang disetujui, serta mencatat hasil pengirimannya apabila kanal mendukung. |
| **Pemicu** | Jadwal pengingat pembayaran tercapai berdasarkan aturan yang telah disepakati. |
| **Kondisi Awal** | Data kesediaan donasi dan jadwal telah tersimpan pada FR-004; kontak donatur dan kanal pengiriman tersedia serta penggunaannya telah disetujui. |
| **Prioritas Usulan** | Should Have — usulan, perlu persetujuan Baitulmal Tazkia. |
| **Tingkat Kesulitan Usulan** | 3 — Medium |
| **Status** | Draft untuk review dan validasi; mekanisme pengingat manual/autodebit, waktu, frekuensi, dan kanal belum diputuskan. |

---

## B. Deskripsi Functional Requirement

Ketika jadwal pengingat tercapai berdasarkan aturan yang disepakati, sistem menyiapkan dan mengirim pesan pengingat kepada donatur melalui kanal komunikasi yang disetujui. Jika kanal menyediakan informasi hasil pengiriman, sistem mencatat hasil tersebut. Jika pengiriman gagal, sistem mencatat kegagalan agar dapat ditelusuri. Pengiriman pengingat tidak membuktikan bahwa pembayaran telah dilakukan dan tidak boleh mengubah status pembayaran menjadi berhasil.

### 1. Format Outline dan Batasan
* Sistem menentukan waktu pengingat berdasarkan jadwal dan aturan yang disepakati.
* Sistem memastikan data kontak dan kanal pengiriman tersedia serta dapat digunakan.
* Sistem mengirim pesan pengingat kepada donatur melalui kanal yang disetujui.
* Sistem mencatat hasil pengiriman apabila kanal mendukung informasi tersebut.
* Sistem mencatat kegagalan pengiriman agar dapat ditelusuri.
* Jika pembayaran belum terkonfirmasi setelah pengingat, sistem tidak menyatakan pembayaran berhasil.

> **Batasan:** FR-005 hanya membahas pengingat pembayaran. Pengiriman permintaan pembayaran/penagihan melalui gateway termasuk FR-006; verifikasi status transaksi termasuk FR-007; notifikasi status donasi termasuk FR-013; penyimpanan kesediaan dan jadwal termasuk FR-004. Hubungan pengingat dengan mekanisme autodebit masih perlu diputuskan.

---

## C. Proses Bisnis

| Tahap | Aktor | Aktivitas | Dasar / Catatan |
| :---: | :--- | :--- | :--- |
| **1** | Sistem | Membaca jadwal donasi dan menentukan waktu pengingat. | Mengacu SRS; aturan tanggal dan frekuensi perlu konfirmasi. |
| **2** | Sistem | Memastikan kontak donatur dan kanal pengiriman tersedia. | Kondisi awal; sumber kontak dan izin penggunaan perlu konfirmasi. |
| **3** | Sistem | Mengirim pesan pengingat melalui kanal yang disetujui. | Mengacu SRS; kanal dan isi pesan belum ditetapkan. |
| **4** | Sistem | Mencatat hasil pengiriman jika kanal mendukung. | Mengacu SRS; format catatan perlu konfirmasi. |
| **5** | Sistem | Mencatat kegagalan pengiriman jika terjadi. | Mengacu kebutuhan keterlacakan; detail retry belum ditentukan. |

> **Alur Alternatif:** Jika pengiriman gagal atau kanal tidak memberikan respons, sistem mencatat kondisi tersebut. Percobaan ulang, jeda antarpercobaan, dan eskalasi hanya dilakukan jika aturan tersebut telah disepakati. Jika donatur belum membayar, status pembayaran tetap belum terkonfirmasi sampai ada hasil yang diverifikasi melalui FR-007.

---

## D. Field, Tipe Data, dan Validasi

| Field Usulan | Tujuan / Isi | Tipe Data | Validasi / Status |
| :--- | :--- | :--- | :--- |
| **Jadwal pengingat** | Waktu atau aturan pengiriman pesan. | Belum ditentukan | Mengikuti jadwal yang disetujui; waktu dan frekuensi perlu konfirmasi. |
| **Kanal pengiriman** | Media pengiriman pesan. | Belum ditentukan | Hanya kanal yang disetujui; perlu konfirmasi. |
| **Kontak tujuan** | Nomor/alamat tujuan donatur. | Belum ditentukan | Harus tersedia dan boleh digunakan untuk pengingat. |
| **Isi pesan** | Teks pengingat yang dikirim. | Teks (usulan) | Isi pesan dan pengelolanya perlu disepakati. |
| **Hasil pengiriman** | Informasi terkirim/gagal bila tersedia. | Belum ditentukan | Mengikuti kemampuan kanal. |
| **Catatan kegagalan** | Informasi untuk menelusuri kegagalan. | Belum ditentukan | Kegagalan harus dapat ditelusuri; format perlu konfirmasi. |

---

## E. Mockup Konseptual

*Contoh isi pengingat (bukan desain pesan final):*

| Elemen Pesan | Contoh Isi |
| :--- | :--- |
| **Identitas pengirim** | Baitulmal Tazkia |
| **Sapaan dan pengingat** | Pengingat jadwal donasi berulang Anda. |
| **Nominal** | `[Nominal donasi — mengikuti data FR-003/FR-004]` |
| **Jadwal / peruntukan** | `[Jadwal dan peruntukan donasi]` |
| **Cara pembayaran** | `[Petunjuk atau tautan pembayaran — jika disepakati]` |

*Catatan: Kanal, redaksi, tautan pembayaran, dan waktu pengiriman belum ditetapkan. Mockup ini hanya membantu validasi kebutuhan.*

---

## F. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Terkait | Catatan |
| :--- | :--- | :--- |
| **Keamanan** | Kontak dan data donatur dilindungi dari akses tidak berwenang. | NFR-001 SRS. |
| **Keandalan** | Pengiriman pengingat tidak mengubah status pembayaran. | NFR-002 SRS. |
| **Keterlacakan** | Hasil dan kegagalan pengiriman dapat ditelusuri bila didukung kanal. | NFR-005 dan NFR-007 SRS. |
| **Kemudahan penggunaan** | Isi pesan mudah dipahami donatur. | NFR-004 SRS. |

---

## G. Kriteria Penerimaan
- [ ] Sistem menentukan pengingat berdasarkan jadwal dan aturan yang telah disepakati.
- [ ] Pengingat hanya dikirim melalui kanal yang disetujui dan kepada kontak yang tersedia.
- [ ] Sistem mencatat hasil pengiriman apabila kanal mendukung.
- [ ] Jika pengiriman gagal, sistem mencatat kegagalan agar dapat ditelusuri.
- [ ] Pengiriman pengingat tidak mengubah status pembayaran menjadi berhasil.
- [ ] Pembayaran hanya dapat dinyatakan berhasil setelah status diverifikasi melalui proses FR-007.

*Catatan: Kriteria penerimaan ini masih perlu disesuaikan setelah mekanisme pengingat dan kanal komunikasi disepakati.*

---

## H. Prioritas dan Tingkat Kesulitan

| Komponen | Usulan | Dasar |
| :--- | :--- | :--- |
| **Prioritas MoSCoW** | Should Have — usulan | Pengingat tercantum sebagai kebutuhan pada SRS, tetapi penerapannya bergantung pada keputusan apakah pembayaran dilakukan manual, autodebit, atau kombinasi. |
| **Tingkat kesulitan** | 3 — Medium | Melibatkan penjadwalan, pengiriman melalui kanal eksternal, dan pencatatan hasil/kegagalan. Kompleksitas bergantung pada kanal dan aturan retry. |

### Dasar Pertimbangan Penilaian
Skala kesulitan 1–5: **1–2 Easy**, **3 Medium**, dan **4–5 Hard**. FR-005 diusulkan pada tingkat **3 (Medium)** karena memerlukan pengaturan jadwal, pengiriman pesan, serta pencatatan hasil. Prioritas *Should Have* merupakan usulan sementara karena ruang lingkup pengingat manual dan hubungannya dengan autodebit masih perlu keputusan klien. Penilaian ini bukan persetujuan final.

---

## I. Hal yang Perlu Dikonfirmasi kepada Klien
1. Apakah pengingat pembayaran manual digunakan, atau pengingat berjalan bersama mekanisme autodebit?
2. Kapan pengingat dikirim dan berapa frekuensinya sebelum atau setelah tanggal pembayaran?
3. Kanal apa yang digunakan (misalnya WhatsApp, email, atau SMS), dan siapa penyedia/pengelolanya?
4. Dari mana data kontak donatur diperoleh dan bagaimana persetujuan penggunaan kontak dicatat?
5. Siapa yang menyusun dan menyetujui isi pesan pengingat?
6. Apakah pesan memuat tautan atau petunjuk pembayaran? Jika ya, siapa yang membuat tautan tersebut?
7. Bagaimana hasil pengiriman dicatat dan apa yang dilakukan jika pengiriman gagal?
8. Apakah ada percobaan ulang, berapa batas dan jedanya?
9. Bagaimana batas fungsi FR-005 dengan FR-013 (pemberitahuan status donasi)?
10. Apakah pengingat otomatis dihentikan ketika donasi dijeda atau dibatalkan melalui FR-011/FR-012?

---

## J. Checklist Konfirmasi Client

| ID & Nama Kebutuhan | Prioritas Usulan | Kesulitan Usulan | Tidak Dibutuhkan / Catatan Client |
| :--- | :--- | :--- | :--- |
| **FR-005 — Mengirim Pengingat Pembayaran** | Should Have — usulan | 3 — Medium | |

---

## K. Catatan dan Status Dokumen
FR-005 berada setelah penyimpanan kesediaan donasi dan jadwal pada FR-004. Dokumen ini diselaraskan dengan SRS/BRS Fitur 4 versi 1.0 tanggal 14 November 2026. Mekanisme pengingat manual atau autodebit, waktu, frekuensi, kanal, isi pesan, dan retry belum ditetapkan sehingga harus divalidasi bersama klien.  
**Status dokumen:** Draft untuk Review dan Validasi Klien; belum menjadi baseline sebelum disetujui.