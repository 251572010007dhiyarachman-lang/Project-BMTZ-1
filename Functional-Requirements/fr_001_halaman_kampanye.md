# FUNCTIONAL REQUIREMENT (FR)
## FR-001 — HALAMAN KAMPANYE
**Sistem Donasi Berulang dan Kanal Pembayaran Digital**

* **Organisasi:** Baitulmal Tazkia
* **Versi:** 0.1 — Draft Awal
* **Status:** Untuk ditinjau dan divalidasi
* **Tanggal acuan:** 25 Oktober 2026

---

### A. Identitas Kebutuhan

| Atribut | Keterangan |
| :--- | :--- |
| **ID Kebutuhan** | FR-001 |
| **Nama Kebutuhan** | Halaman Kampanye |
| **Aktor Utama** | Calon donatur / donatur |
| **Tujuan** | Memberikan informasi kampanye sebelum calon donatur melanjutkan ke proses donasi. |
| **Prioritas** | Belum ditentukan |
| **Status** | Draft awal; belum menjadi persyaratan final klien |

---

### B. Deskripsi Functional Requirement

Sistem menyediakan halaman informasi kampanye donasi yang dapat diakses oleh calon donatur melalui tautan kampanye. Halaman menampilkan informasi program donasi agar calon donatur dapat memahami kampanye sebelum memilih untuk melanjutkan ke proses donasi berulang.

#### 1. Format Outline
* Akses calon donatur ke halaman melalui tautan kampanye.
* Penampilan informasi kampanye yang telah dimasukkan dan dikelola oleh staf internal.
* Penyediaan akses untuk melanjutkan ke proses donasi sesuai alur yang disepakati.
* **Batasan:** FR-001 berfokus pada penyajian informasi kampanye. Pemilihan nominal dan jadwal donasi merupakan fungsi lanjutan yang dirinci pada FR terkait.

#### 2. Proses Bisnis
**Aktor:** Calon donatur dan sistem. *(Pengelolaan informasi kampanye dilakukan oleh staf internal).*

1. Staf internal memasukkan atau memperbarui informasi kampanye sesuai kewenangannya.
2. Calon donatur memperoleh tautan kampanye melalui kanal komunikasi.
3. Calon donatur membuka tautan kampanye.
4. Sistem menampilkan informasi kampanye yang tersedia.
5. Calon donatur membaca informasi kampanye.
6. Calon donatur memilih untuk melanjutkan ke proses donasi berulang.

> **Alur alternatif yang perlu diputuskan:** Penanganan tautan tidak valid, kampanye tidak aktif, atau informasi kampanye belum tersedia.

#### 3. Field, Tipe Data, dan Validasi
*Tabel berikut merupakan usulan awal untuk dibahas. Draft SRS yang tersedia belum menetapkan seluruh field halaman kampanye secara rinci; daftar ini bukan keputusan final.*

| Field Usulan | Tipe Data | Validasi Usulan | Status |
| :--- | :--- | :--- | :--- |
| **Judul kampanye** | `VARCHAR` / String | Tidak kosong; batas panjang ditetapkan kemudian | Perlu konfirmasi |
| **Deskripsi kampanye** | `TEXT` | Tidak kosong jika ditetapkan sebagai informasi wajib | Perlu konfirmasi |
| **Gambar kampanye** | `URL` / String | Format dan ukuran jika unggah gambar didukung | Perlu konfirmasi |
| **Tautan/slug kampanye** | `VARCHAR` / String | Unik dan format URL valid | Perlu konfirmasi |
| **Status kampanye** | `ENUM` / String | Nilai status ditentukan pengelola | Perlu konfirmasi |

#### 4. UI Mockup
*Sketsa tekstual awal (bukan desain final):*

```text
+-------------------------------------------------------+
| [ LOGO / IDENTITAS BAITULMAL ]                        |
|                                                       |
| [ GAMBAR KAMPANYE ]                                   |
|                                                       |
| JUDUL KAMPANYE                                        |
| Deskripsi singkat program donasi                      |
| Informasi kampanye lainnya (sesuai hasil validasi)    |
|                                                       |
| [ LANJUTKAN DONASI ]                                  |
+-------------------------------------------------------+
```

*Elemen, susunan halaman, identitas visual, dan label tombol harus dikonfirmasi kepada pihak Baitulmal Tazkia.*

#### 5. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Awal | Catatan |
| :--- | :--- | :--- |
| **Keamanan** | Calon donatur hanya melihat informasi; tidak dapat mengubah data kampanye. | Aturan akses perlu ditetapkan. |
| **Kinerja** | Halaman dapat dimuat dalam waktu yang wajar. | Target waktu respons belum ditetapkan. |
| **Kemudahan penggunaan** | Informasi dan instruksi mudah dipahami. | Perlu ditinjau melalui UI/mockup. |
| **Ketersediaan** | Tautan dapat diakses saat kampanye tersedia/aktif. | Target availability belum ditetapkan. |

---

### C. Kriteria Penerimaan Awal
- [ ] Calon donatur dapat membuka halaman melalui tautan kampanye yang valid.
- [ ] Sistem menampilkan informasi kampanye yang telah tersedia.
- [ ] Calon donatur dapat membaca informasi sebelum melanjutkan ke proses donasi.
- [ ] Akses untuk melanjutkan ke proses donasi tersedia sesuai alur yang disepakati.

---

### D. Hal yang Perlu Dikonfirmasi
1. Informasi apa saja yang wajib ditampilkan pada halaman kampanye?
2. Apakah halaman hanya menampilkan kampanye donasi berulang atau juga jenis kampanye lain?
3. Siapa yang berwenang membuat, mengubah, mengaktifkan, dan menonaktifkan kampanye?
4. Apa respons sistem jika tautan tidak valid atau kampanye sudah tidak aktif?
5. Apakah halaman berada di aplikasi ini atau diakses melalui website/kanal lain?
6. Apakah tombol lanjutan langsung menuju pemilihan nominal dan jadwal donasi?

---

### E. Catatan untuk Presentasi
* **Fokus Ruang Lingkup:** FR-001 menjelaskan penyajian informasi kampanye kepada calon donatur. Fungsi ini menjadi titik awal alur donasi: calon donatur memperoleh informasi terlebih dahulu, kemudian dapat melanjutkan ke proses donasi berulang. FR ini tidak menetapkan metode pembayaran, jadwal pengingat, autodebit, atau verifikasi transaksi karena hal-hal tersebut merupakan fungsi/keputusan lain.
* **Status Draft:** Jika ditanya mengapa *field*, validasi, UI, dan NFR belum final: SRS versi 0.1 menyatakan kebutuhan masih berupa rancangan awal dan harus dikonfirmasi dengan pihak terkait.