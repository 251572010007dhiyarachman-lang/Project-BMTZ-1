# BAITULMAL TAZKIA
## SISTEM DONASI BERULANG DAN KANAL PEMBAYARAN DIGITAL

### FUNCTIONAL REQUIREMENT (FR)
# FR-006: MEMPROSES PEMBAYARAN MELALUI GATEWAY

**Versi:** 1.0 | **Status:** Draft untuk Review dan Validasi Klien | **Tanggal:** 25 November 2026  
**Acuan:** SRS dan BRS Fitur 4 versi 1.0, tanggal acuan 14 November 2026.

---

## A. Identitas Kebutuhan

| Informasi | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-006 |
| **Nama Kebutuhan** | Memproses Pembayaran melalui Gateway |
| **Aktor Utama** | Sistem Fitur 4 dan Payment Gateway Artivisi; donatur terlibat sesuai mekanisme pembayaran yang diputuskan. |
| **Tujuan** | Mengirim permintaan pembayaran atau penagihan ke Payment Gateway Artivisi sesuai metode dan kontrak integrasi yang telah disepakati, lalu menyimpan referensi transaksi serta mencatat respons proses. |
| **Pemicu** | Donatur melanjutkan proses pembayaran atau jadwal penagihan tercapai sesuai mekanisme yang disetujui. |
| **Kondisi Awal** | Data kesediaan donasi dan jadwal tersedia; metode pembayaran dan dukungan gateway telah dikonfirmasi; kontrak integrasi disepakati. |
| **Prioritas Usulan** | Must Have — usulan, perlu persetujuan Baitulmal Tazkia. |
| **Tingkat Kesulitan Usulan** | 4 — Hard |
| **Status** | Draft untuk review dan validasi; metode pembayaran, pola penagihan, dan detail integrasi Artivisi belum dikonfirmasi. |

---

## B. Deskripsi Functional Requirement

Jika mekanisme pembayaran telah diputuskan dan didukung oleh Payment Gateway Artivisi, sistem mengirim permintaan pembayaran atau penagihan sesuai kontrak integrasi yang disepakati. Sistem menyimpan referensi transaksi dan mencatat respons gateway. Jika gateway menolak permintaan, mengalami timeout, atau belum memberikan respons final, sistem mencatat kondisi tersebut dan tidak menyatakan pembayaran berhasil. Pengiriman permintaan ke gateway bukan bukti bahwa pembayaran telah berhasil.

### 1. Format Outline dan Batasan
* Sistem hanya menggunakan metode pembayaran yang telah dikonfirmasi didukung oleh Artivisi.
* Sistem menyiapkan dan mengirim permintaan pembayaran atau penagihan sesuai kontrak integrasi.
* Sistem menyimpan referensi transaksi yang diterima atau dibentuk sesuai kesepakatan integrasi.
* Sistem mencatat respons penolakan, timeout, atau kondisi ketika status belum final.
* Sistem tidak menetapkan pembayaran berhasil hanya karena permintaan telah dikirim atau diterima gateway.

> **Batasan:** FR-006 menangani pengiriman permintaan ke gateway dan pencatatan referensi/respons awal. Pengaturan nominal dan jadwal berada pada FR-003/FR-004; pengingat pembayaran pada FR-005; verifikasi dan pembaruan status pada FR-007; tanda terima, penyediaan data integrasi, notifikasi, tautan pembayaran satu kali, dan pencegahan transaksi ganda berada pada FR-008 sampai FR-015 sesuai pembagian SRS.

---

## C. Proses Bisnis

| Tahap | Aktor | Aktivitas | Dasar / Catatan |
| :---: | :--- | :--- | :--- |
| **1** | PIC / pihak terkait | Menetapkan mekanisme pembayaran dan metode yang akan digunakan. | Kondisi awal SRS; keputusan bisnis dan dukungan gateway perlu konfirmasi. |
| **2** | Sistem Fitur 4 | Menyiapkan data permintaan pembayaran/penagihan berdasarkan kesediaan dan jadwal donasi. | Mengacu SRS; field dan pemetaan payload perlu konfirmasi. |
| **3** | Sistem Fitur 4 | Mengirim permintaan ke Payment Gateway Artivisi sesuai kontrak. | Mengacu SRS; endpoint, autentikasi, dan protokol belum tersedia. |
| **4** | Payment Gateway Artivisi | Memproses permintaan dan memberikan respons sesuai kemampuan layanan. | Respons dan format data mengikuti dokumentasi/kontrak Artivisi. |
| **5** | Sistem Fitur 4 | Menyimpan referensi transaksi dan mencatat respons awal. | Mengacu SRS; format referensi dan field respons perlu konfirmasi. |

> **Alur Alternatif:** Jika gateway menolak permintaan, terjadi timeout, atau tidak ada respons final, sistem mencatat kondisi tersebut dan mempertahankan referensi yang tersedia. Sistem tidak menyatakan transaksi berhasil. Pemeriksaan status lebih lanjut dilakukan melalui FR-007. Aturan retry, jeda, dan batas percobaan harus mengikuti keputusan serta kontrak yang disetujui.

---

## D. Field, Tipe Data, dan Validasi

| Field Usulan | Tujuan / Isi | Tipe Data | Validasi / Status |
| :--- | :--- | :--- | :--- |
| **Metode pembayaran** | Metode yang dipilih untuk pembayaran/penagihan. | Belum ditentukan | Hanya metode yang telah dikonfirmasi didukung Artivisi. |
| **Nominal** | Nominal dari data donasi. | Belum ditentukan | Harus sesuai data FR-003/FR-004 dan kontrak gateway. |
| **Referensi transaksi** | Identitas untuk menelusuri transaksi. | Belum ditentukan | Harus dapat dicocokkan; format dan keunikan perlu disepakati. |
| **ID transaksi gateway** | Identitas transaksi dari gateway jika diberikan. | Belum ditentukan | Mengikuti respons dan dokumentasi Artivisi. |
| **Jadwal / token** | Informasi penjadwalan atau token bila mekanisme mendukung. | Belum ditentukan | Hanya digunakan jika disejui dan didukung gateway. |
| **Respons gateway** | Respons atas permintaan pembayaran/penagihan. | Belum ditentukan | Format dan kode respons mengikuti kontrak. |
| **Catatan kondisi** | Penolakan, timeout, atau status belum final. | Belum ditentukan | Kondisi harus dapat ditelusuri; detail pencatatan perlu disepakati. |

---

## E. Diagram Konseptual Integrasi

| Urutan | Komponen | Proses |
| :---: | :--- | :--- |
| **1** | Sistem Fitur 4 | Menyiapkan permintaan pembayaran/penagihan. |
| **2** | Sistem Fitur 4 $\rightarrow$ Artivisi | Mengirim permintaan sesuai kontrak API yang disepakati. |
| **3** | Payment Gateway Artivisi | Memproses permintaan dan mengirim respons. |
| **4** | Sistem Fitur 4 | Menyimpan referensi dan mencatat respons awal. |
| **5** | FR-007 | Memeriksa dan memverifikasi status transaksi sebelum dinyatakan berhasil. |

*Catatan: Diagram ini bersifat konseptual. Endpoint, payload, autentikasi, callback/webhook, metode pembayaran, dan detail teknis lainnya belum ditetapkan oleh dokumen sumber.*

---

## F. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Terkait | Catatan |
| :--- | :--- | :--- |
| **Keamanan** | Data pembayaran dan data donatur dilindungi dari akses tidak berwenang. | NFR-001 SRS; data sensitif yang boleh disimpan perlu disepakati. |
| **Keandalan** | Permintaan yang terkirim tidak boleh langsung dianggap sebagai pembayaran berhasil. | NFR-002 SRS. |
| **Integrasi** | Pertukaran data dilakukan melalui API atau mekanisme yang disepakati. | NFR-003 SRS; kontrak belum final. |
| **Konsistensi data** | Referensi transaksi dapat digunakan untuk penelusuran dan pencocokan. | NFR-005 SRS. |
| **Pemulihan kegagalan** | Kegagalan integrasi dapat dicatat dan ditelusuri; pengiriman ulang tidak menimbulkan catatan ganda. | NFR-007 dan FR-015; detail teknis perlu konfirmasi. |

---

## G. Kriteria Penerimaan
- [ ] Sistem hanya menggunakan metode pembayaran yang telah dikonfirmasi didukung oleh Artivisi.
- [ ] Sistem mengirim permintaan pembayaran/penagihan sesuai kontrak integrasi yang disepakati.
- [ ] Sistem menyimpan referensi transaksi yang dapat digunakan untuk penelusuran.
- [ ] Sistem mencatat kondisi penolakan, timeout, atau respons yang belum final.
- [ ] Sistem tidak menyatakan pembayaran berhasil hanya karena permintaan telah dikirim ke gateway.
- [ ] Status pembayaran berhasil hanya ditetapkan setelah proses verifikasi pada FR-007.

*Catatan: Pengujian rinci baru dapat ditetapkan setelah mekanisme pembayaran dan kontrak integrasi gateway dikonfirmasi.*

---

## H. Prioritas dan Tingkat Kesulitan

| Komponen | Usulan | Dasar |
| :--- | :--- | :--- |
| **Prioritas MoSCoW** | Must Have — usulan | Pemrosesan pembayaran digital merupakan bagian inti ruang lingkup Fitur 4 pada SRS/BRS. Usulan ini tetap memerlukan persetujuan klien. |
| **Tingkat kesulitan** | 4 — Hard | Melibatkan integrasi pihak ketiga, pertukaran data, referensi transaksi, penanganan penolakan/timeout, dan ketergantungan pada kontrak teknis gateway. |

### Dasar Pertimbangan Penilaian
Skala kesulitan 1–5: **1–2 Easy**, **3 Medium**, dan **4–5 Hard**. FR-006 diusulkan pada tingkat **4 (Hard)** karena membutuhkan integrasi dengan layanan eksternal, kesesuaian payload dan autentikasi, serta penanganan respons dan kegagalan. Prioritas *Must Have* diusulkan karena fungsi pembayaran digital merupakan bagian inti Fitur 4. Kedua penilaian ini merupakan usulan dan bukan persetujuan final klien.

---

## I. Hal yang Perlu Dikonfirmasi kepada Klien / Artivisi
1. Mekanisme apa yang digunakan: pembayaran manual melalui tautan, penagihan berkala melalui Artivisi, atau keduanya?
2. Metode pembayaran apa saja yang benar-benar didukung untuk kebutuhan donasi berulang?
3. Apa pemicu pengiriman permintaan dan bagaimana tanggal penagihan ditentukan?
4. Apa endpoint, payload, autentikasi, nama field, dan format respons pada integrasi Artivisi?
5. Apakah Artivisi menyediakan ID transaksi/referensi unik dan bagaimana aturan pencocokannya?
6. Apakah status diperoleh melalui callback/webhook, pemeriksaan berkala, atau mekanisme lain? *(detail verifikasi ditangani FR-007)*
7. Bagaimana penanganan penolakan, timeout, dan respons yang belum final?
8. Apakah retry dilakukan? Jika ya, berapa jeda dan batas percobaannya?
9. Data pembayaran apa yang boleh disimpan oleh sistem dan bagaimana perlindungannya?
10. Bagaimana permintaan ulang dicegah agar tidak membuat transaksi atau penagihan ganda (koordinasi dengan FR-015)?

---

## J. Checklist Konfirmasi Client

| ID & Nama Kebutuhan | Prioritas Usulan | Kesulitan Usulan | Tidak Dibutuhkan / Catatan Client |
| :--- | :--- | :--- | :--- |
| **FR-006 — Memproses Pembayaran melalui Gateway** | Must Have — usulan | 4 — Hard | |

---

## K. Catatan dan Status Dokumen
FR-006 berada setelah pendaftaran dan penyimpanan kesediaan donasi (FR-003/FR-004) dan sebelum verifikasi status transaksi (FR-007). Dokumen ini diselaraskan dengan SRS/BRS Fitur 4 versi 1.0 tanggal 14 November 2026. Mekanisme pembayaran, metode yang didukung, kontrak API, respons, timeout, dan retry masih memerlukan validasi dari Baitulmal Tazkia dan Payment Gateway Artivisi.  
**Status dokumen:** Draft untuk Review dan Validasi Klien; belum menjadi baseline sebelum disetujui.