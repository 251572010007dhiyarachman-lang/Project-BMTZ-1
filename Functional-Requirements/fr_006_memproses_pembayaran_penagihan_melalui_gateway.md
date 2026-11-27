# FUNCTIONAL REQUIREMENT

## FR-006 — Memproses Pembayaran/Penagihan Melalui Gateway

**Sistem Donasi Berulang dan Kanal Pembayaran Digital | Baitulmal Tazkia**

### A. Identitas Kebutuhan

| Elemen | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-006 |
| **Nama Kebutuhan** | Memproses Pembayaran/Penagihan Melalui Gateway |
| **Aktor Utama** | Subsistem Donasi Berulang dan Payment Gateway Artivisi. Peran donatur bergantung pada mekanisme pembayaran yang diputuskan. |
| **Tujuan** | Mengirim permintaan pembayaran atau penagihan ke Payment Gateway Artivisi sesuai kontrak dan menyimpan referensi transaksi, hanya dengan metode yang telah dikonfirmasi didukung. |
| **Prioritas** | Belum ditentukan. |
| **Status** | Draft awal untuk presentasi; belum menjadi persyaratan final klien. Mekanisme pembayaran dan rincian integrasi masih perlu klarifikasi. |
| **Acuan** | FR-006 versi 0.1 Draft Awal dan SRS Draft v0.2, tanggal acuan 26 Oktober 2026. |

### B. Deskripsi Functional Requirement

Apabila mekanisme pembayaran yang dipilih telah disetujui dan Payment Gateway Artivisi mendukungnya, sistem mengirim permintaan pembayaran atau penagihan ke gateway sesuai kontrak, kemudian menyimpan referensi transaksi. Apabila gateway menolak, mengalami timeout, atau tidak memberikan status final, sistem mencatat kondisi tersebut dan tidak menyatakan transaksi berhasil. Pengiriman permintaan ke gateway tidak dianggap sebagai pembayaran berhasil.

* **Pemicu:** Mekanisme pembayaran yang dipilih telah disetujui dan gateway mendukungnya.
* **Kondisi awal:** Metode dan integrasi telah dikonfirmasi oleh PIC/gateway. SRS menyebut dua kemungkinan mekanisme, yaitu pembayaran manual melalui tautan atau penagihan berkala melalui Artivisi. Alur rinci baru dapat ditetapkan setelah mekanisme diputuskan.

### C. Ruang Lingkup dan Batasan

**Termasuk dalam FR-006:**
* Memastikan metode pembayaran dan integrasi yang digunakan telah dikonfirmasi didukung.
* Mengirim permintaan pembayaran atau penagihan ke Payment Gateway Artivisi sesuai kontrak yang disepakati.
* Menyimpan referensi transaksi yang diterima dari proses integrasi.
* Mencatat kondisi ketika gateway menolak permintaan, mengalami timeout, atau belum memberikan status final.
* Tidak menyatakan transaksi berhasil hanya karena permintaan telah dikirim ke gateway.

**Tidak termasuk dalam FR-006:**
* Pengaturan nominal, jadwal, dan peruntukan donasi (FR-003).
* Penyimpanan kesediaan donasi dan jadwal (FR-004).
* Pengiriman pengingat pembayaran (FR-005).
* Pemeriksaan dan pembaruan status transaksi (FR-007).
* Pengiriman data untuk proses tanda terima (FR-008).
* Penyediaan data rekonsiliasi dan pelaporan (FR-010).
* Notifikasi kepada donatur (FR-013).
* Tautan pembayaran satu kali (FR-014).
* Pencegahan pencatatan atau penagihan ganda (FR-015).

> **Batas penting:** FR-006 menangani pengiriman permintaan ke gateway, penyimpanan referensi transaksi, dan pencatatan kondisi kegagalan atau status belum final. Pemeriksaan/pembaruan status transaksi ditangani pada FR-007.

### D. Proses Bisnis

*Label: `[Tertulis di SRS]` berarti dinyatakan pada SRS Draft v0.2; `[Disimpulkan dari SRS]` berarti diturunkan dari kondisi awal atau kriteria penerimaan; `[Perlu Konfirmasi]` berarti informasinya belum tersedia.*

| No. | Aktor | Aktivitas | Dasar / Catatan |
| :--- | :--- | :--- | :--- |
| 1 | PIC / sistem | Memastikan mekanisme pembayaran yang dipilih telah disetujui dan didukung gateway. | Kondisi awal tertulis di SRS; cara pemeriksaan perlu konfirmasi. |
| 2 | Subsistem Donasi Berulang | Memastikan metode dan integrasi telah dikonfirmasi didukung. | Disimpulkan dari kondisi awal dan kriteria penerimaan SRS. |
| 3 | Subsistem Donasi Berulang | Mengirim permintaan pembayaran atau penagihan ke Payment Gateway Artivisi sesuai kontrak. | Tertulis di SRS; isi permintaan, autentikasi, dan kontrak teknis perlu konfirmasi. |
| 4 | Payment Gateway Artivisi | Memberikan respons yang dapat mencakup ID transaksi dan status. | Unsur respons disebut pada SRS Bab 2.3; nama field dan format perlu konfirmasi. |
| 5 | Subsistem Donasi Berulang | Menyimpan referensi transaksi. | Tertulis di SRS; format dan aturan keunikan perlu konfirmasi. |

**Alur alternatif — gateway menolak, timeout, atau belum memberi status final:**
* Sistem mencatat kondisi penolakan, timeout, atau status yang belum final.
* Sistem tidak menyatakan transaksi berhasil.
* Kebijakan percobaan ulang (*retry*) mengikuti keputusan yang disepakati; jumlah, jeda, dan batas *retry* belum ditentukan.
* Batas tanggung jawab pencatatan kondisi pada FR-006 dan pemeriksaan ulang status pada FR-007 perlu dikonfirmasi.

### E. Field, Tipe Data, dan Validasi

*SRS Draft v0.2 menyebut unsur data yang mungkin dipertukarkan dengan gateway, tetapi belum menetapkan nama field, tipe data, token, autentikasi, daftar status, callback/webhook, timeout, atau retry. Nama berikut merupakan field usulan untuk pembahasan, bukan nama kolom basis data maupun nama field kontrak API.*

| Field Usulan | Tujuan / Isi | Tipe Data | Validasi / Status |
| :--- | :--- | :--- | :--- |
| **Metode pembayaran** | Metode yang dipilih untuk proses pembayaran/penagihan. | Belum ditentukan. | Hanya metode yang telah dikonfirmasi didukung; daftar metode perlu konfirmasi (OQ-002). |
| **Referensi transaksi** | Referensi untuk menelusuri transaksi. | Belum ditentukan. | Harus dapat ditelusuri; format dan aturan keunikan mengikuti kontrak yang perlu disepakati (NFR-005). |
| **Nominal** | Nominal donasi dari proses pendaftaran. | Belum ditentukan. | Mengikuti data pendaftaran pada FR-003 dan FR-004; pemetaan ke kontrak gateway perlu konfirmasi. |
| **Jadwal / token** | Jadwal penagihan atau token jika mekanisme dan gateway mendukung. | Belum ditentukan. | Dikirim hanya jika metode dan persetujuan mendukung; makna dan format token perlu konfirmasi. |
| **ID transaksi gateway** | Identitas transaksi yang dikembalikan gateway. | Belum ditentukan. | Diterima dari respons gateway; nama dan format field perlu konfirmasi. |
| **Status dari gateway** | Status yang dikembalikan gateway. | Belum ditentukan. | Menggunakan status yang benar-benar diberikan gateway; daftar status dan pemetaan perlu konfirmasi (OQ-005). |
| **Catatan kondisi** | Informasi penolakan, timeout, atau status belum final. | Belum ditentukan. | Kondisi harus dicatat; isi, format, dan lokasi pencatatan perlu konfirmasi. |

### F. UI Mockup / Diagram Alur Integrasi

*SRS tidak menetapkan tampilan antarmuka khusus untuk FR-006 karena fungsi ini terutama berupa proses sistem dan pertukaran data dengan gateway. Diagram berikut adalah mockup alur integrasi untuk bahan presentasi, bukan desain halaman donatur atau tampilan final.*

```text
+-----------------------------------------------------------------------+
| SUBSISTEM DONASI BERULANG                                             |
| Menyiapkan permintaan pembayaran / penagihan                          |
+-----------------------------------------------------------------------+
                                   |
     Permintaan sesuai kontrak API (payload, autentikasi, & field
     menunggu konfirmasi)
                                   v
+-----------------------------------------------------------------------+
| PAYMENT GATEWAY ARTIVISI                                              |
| Memproses permintaan dan mengembalikan respons                        |
+-----------------------------------------------------------------------+
                                   |
     Respons dapat memuat ID transaksi dan status dari gateway
                                   v
+-----------------------------------------------------------------------+
| SUBSISTEM DONASI BERULANG                                             |
| Menyimpan referensi transaksi dan mencatat respons                    |
+-----------------------------------------------------------------------+
```
*Catatan: Permintaan yang berhasil dikirim atau diterima untuk diproses tidak sama dengan pembayaran berhasil. Status pembayaran tetap menunggu pemeriksaan/verifikasi pada FR-007.*

#### F.1 Mockup kondisi gateway menolak / timeout / status belum final

```text
+-----------------------------------------------------------------------+
| PAYMENT GATEWAY ARTIVISI                                              |
| Penolakan / timeout / status belum final                              |
+-----------------------------------------------------------------------+
                                   |
     Respons gagal atau tidak ada status final
                                   v
+-----------------------------------------------------------------------+
| SUBSISTEM DONASI BERULANG                                             |
| 1. Mencatat kondisi                                                   |
| 2. Tidak menyatakan transaksi berhasil                                |
| 3. Retry mengikuti kebijakan yang disetujui (belum ditentukan)        |
+-----------------------------------------------------------------------+
```
*Jika tersedia tampilan bagi donatur pada jalur pembayaran manual, bentuk halaman/tautan tersebut belum ditentukan dalam SRS. Arah visual awal untuk antarmuka yang nantinya disepakati adalah navy blue dan putih (NFR-006).*

### G. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Awal | Catatan |
| :--- | :--- | :--- |
| **Keamanan** | Data kartu atau nomor rekening mentah tidak ditetapkan untuk disimpan tanpa dasar dan desain keamanan yang disepakati. | NFR-001 dan Bab 2.3 SRS; kebijakan dan kepatuhan perlu klarifikasi. |
| **Keandalan status** | Sistem tidak menyatakan pembayaran berhasil tanpa hasil terverifikasi dari sumber yang disepakati. | NFR-002; permintaan terkirim bukan bukti pembayaran. |
| **Integrasi** | Pertukaran data dengan gateway menggunakan kontrak API yang disepakati. | NFR-003; kontrak API belum final/tersedia pada bahan yang ditinjau. |
| **Keterlacakan** | Referensi transaksi memungkinkan pencocokan antara subsistem donasi, gateway, penerimaan donasi, dan rekonsiliasi. | NFR-005; format referensi perlu disepakati. |
| **Pemulihan kegagalan integrasi** | Kegagalan pertukaran data dapat ditelusuri dan tidak menyebabkan transaksi dianggap berhasil atau tercatat ganda. | NFR-007; logging, monitoring, retry, dan target pemulihan belum ditetapkan. |
| **Kinerja** | Timeout dan target waktu respons mengikuti hasil klarifikasi. | Belum ditetapkan (OQ-005 dan OQ-014). |

### H. Kriteria Penerimaan Awal

* [ ] Sistem hanya menggunakan metode pembayaran yang telah dikonfirmasi didukung.
* [ ] Sistem mengirim permintaan ke Payment Gateway Artivisi sesuai kontrak yang disepakati.
* [ ] Sistem menyimpan referensi transaksi yang dapat ditelusuri.
* [ ] Jika gateway menolak, mengalami timeout, atau tidak memberikan status final, sistem mencatat kondisi tersebut.
* [ ] Sistem tidak menyatakan transaksi berhasil hanya karena permintaan pembayaran/penagihan telah dikirim.
* [ ] Status hasil tidak dibuat atau diasumsikan sendiri oleh sistem, melainkan mengikuti respons dan proses verifikasi yang disepakati.

> *Kriteria penerimaan ini masih bersifat awal. Pengujian rinci baru dapat ditetapkan setelah mekanisme pembayaran dan kontrak integrasi gateway dikonfirmasi.*

### I. Hal yang Perlu Dikonfirmasi

| No. | Pertanyaan / Keputusan | Status |
| :--- | :--- | :--- |
| 1 | Mekanisme mana yang disetujui: pembayaran manual melalui tautan, penagihan berkala melalui Artivisi, atau keduanya untuk metode berbeda? (OQ-001) | Belum dikonfirmasi |
| 2 | Metode apa yang benar-benar mendukung pembayaran berulang? Apakah transfer, virtual account, dan e-wallet didukung? (OQ-002) | Belum dikonfirmasi |
| 3 | Peristiwa apa yang memicu pengiriman permintaan dan kapan tanggal penagihan ditetapkan? (OQ-003) | Belum dikonfirmasi |
| 4 | Apa endpoint, payload, autentikasi, nama field, token, referensi unik, kode respons/error, callback/webhook, dan batas waktu gateway? | Belum dikonfirmasi |
| 5 | Apa daftar status dari gateway dan bagaimana status pending/timeout ditangani? Di mana batas FR-006 dan verifikasi status FR-007? (OQ-005) | Belum dikonfirmasi |
| 6 | Apakah retry dilakukan, berapa jeda dan batas percobaannya, dan kapan kesediaan donasi dianggap berhenti? (OQ-004) | Belum dikonfirmasi |
| 7 | Pada jalur pembayaran manual, siapa yang membuat tautan pembayaran dan bagaimana donatur menerimanya? Apakah terkait dengan FR-014? | Belum dikonfirmasi |
| 8 | Bagaimana permintaan berulang dicegah agar tidak menghasilkan penagihan ganda? (FR-015 dan ALT-08) | Belum dikonfirmasi |
| 9 | Data pembayaran apa yang boleh disimpan sistem dan apa dasar kebijakannya? (NFR-001) | Belum dikonfirmasi |

### J. Catatan untuk Presentasi

* FR-006 menjelaskan pengiriman permintaan pembayaran atau penagihan ke Payment Gateway Artivisi dan penyimpanan referensi transaksi.
* FR-006 berada setelah pendaftaran donasi berulang (FR-002 sampai FR-004) dan sebelum pemeriksaan/pembaruan status transaksi (FR-007).
* FR-006 tidak mencakup pengingat pembayaran, verifikasi status transaksi, notifikasi, tautan pembayaran satu kali, atau pencegahan penagihan ganda karena hal tersebut berada pada FR terpisah.
* Permintaan yang berhasil dikirim ke gateway bukan bukti pembayaran berhasil.
* Alur rinci belum dapat ditetapkan sebelum keputusan mekanisme pembayaran dan kontrak API Artivisi tersedia.
* Dokumen ini dirapikan untuk bahan presentasi; belum menjadi baseline kebutuhan dan belum disetujui klien.

*— Akhir Dokumen FR-006 —*