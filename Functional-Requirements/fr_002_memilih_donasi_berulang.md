# FUNCTIONAL REQUIREMENT (FR)

## FR-002 — MEMILIH DONASI BERULANG

**Sistem Donasi Berulang dan Kanal Pembayaran Digital**

* **Organisasi:** Baitulmal Tazkia

* **Versi:** 1.0 — Finalisasi untuk Presentasi

* **Status:** Dokumen dirapikan; aturan bisnis yang belum tersedia tetap menunggu konfirmasi

* **Tanggal acuan:** 7 November 2026

### A. Identitas Kebutuhan

| Atribut | Keterangan | 
| ----- | ----- | 
| **ID Kebutuhan** | FR-002 | 
| **Nama Kebutuhan** | Memilih Donasi Berulang | 
| **Aktor utama** | Calon donatur / donatur | 
| **Tujuan** | Memungkinkan donatur memilih opsi donasi berulang apabila program atau kampanye mendukung fitur tersebut. | 
| **Prioritas** | Belum ditentukan dalam SRS Draft v0.2. | 
| **Status** | Finalisasi dokumen untuk presentasi; mekanisme bisnis masih memerlukan klarifikasi. | 

### B. Deskripsi Functional Requirement

Sistem harus memeriksa apakah program atau kampanye yang dilihat donatur mendukung donasi berulang. Apabila fitur didukung dan opsinya diaktifkan, sistem menampilkan pilihan donasi berulang. Donatur dapat memilih pilihan tersebut, kemudian sistem melanjutkan ke proses pengaturan donasi. Apabila program atau metode pembayaran tidak mendukung donasi berulang, sistem tidak menawarkan pilihan tersebut dan memberikan penjelasan kepada donatur.

* **Pemicu:** Donatur memilih opsi donasi berulang.

* **Kondisi awal:** Program mendukung donasi berulang dan opsi tersebut diaktifkan.

* **Batasan:** FR-002 hanya membahas ketersediaan dan pemilihan opsi donasi berulang. Pengaturan nominal, jadwal/periode, dan peruntukan dibahas pada FR-003; penyimpanan kesediaan donasi dan jadwal dibahas pada FR-004. Penyajian halaman kampanye merupakan cakupan FR-001. FR-002 tidak mencakup autentikasi donatur, pembayaran/penagihan, pengingat, atau notifikasi.

#### 1. Format Outline

* Sistem memeriksa dukungan donasi berulang pada program atau kampanye.

* Sistem menampilkan pilihan donasi berulang hanya jika program/kampanye mendukung dan opsi tersebut diaktifkan.

* Donatur memilih opsi donasi berulang yang tersedia.

* Sistem melanjutkan donatur ke proses pengaturan donasi pada FR-003.

* Jika program atau metode pembayaran tidak mendukung donasi berulang, sistem tidak menampilkan pilihan tersebut dan memberikan penjelasan.

> **Catatan:** Pemeriksaan dukungan oleh sistem disimpulkan dari kondisi awal dan kriteria penerimaan SRS Draft v0.2; cara pemeriksaannya belum ditentukan.

#### 2. Proses Bisnis

**Aktor:** Calon donatur/donatur dan sistem. *(Langkah 1–2 merupakan titik awal yang dicakup FR-001; FR-002 dimulai pada langkah 3).*

| No. | Aktor | Aktivitas | Dasar | 
| ----- | ----- | ----- | ----- | 
| 1 | Donatur | Membuka halaman informasi kampanye. | Tertulis di SRS — FR-001 | 
| 2 | Sistem | Menampilkan opsi donasi yang tersedia. | Tertulis di SRS — FR-001; letak daftar opsi perlu konfirmasi. | 
| 3 | Sistem | Memeriksa apakah program/kampanye mendukung donasi berulang dan opsi tersebut diaktifkan. | Disimpulkan dari kondisi awal dan kriteria penerimaan SRS; cara pemeriksaan perlu konfirmasi. | 
| 4 | Sistem | Menampilkan pilihan donasi berulang jika didukung. | Tertulis di SRS | 
| 5 | Donatur | Memilih opsi donasi berulang. | Tertulis di SRS | 
| 6 | Sistem | Melanjutkan ke proses pengaturan donasi (FR-003). | Tertulis di SRS | 

**Alur alternatif — program atau metode pembayaran tidak mendukung:**

* Sistem tidak menawarkan pilihan donasi berulang.

* Sistem memberikan penjelasan kepada donatur.

* Isi dan bentuk penjelasan serta langkah lanjutan donatur belum ditentukan dalam SRS dan perlu dikonfirmasi.

* SRS belum menetapkan metode pembayaran mana yang mendukung donasi berulang maupun tahap pemilihan metode pembayaran.

#### 3. Field, Tipe Data, dan Validasi

*SRS Draft v0.2 belum menetapkan field, tipe data, maupun aturan validasi rinci untuk FR-002. Tabel berikut hanya memetakan informasi yang tersirat dari SRS. Nama field merupakan label konseptual, bukan nama kolom basis data; tipe data tidak ditentukan dan tidak boleh dianggap sebagai keputusan implementasi.*

| Informasi / Field Konseptual | Tipe Data | Validasi Berdasarkan SRS | Status | 
| ----- | ----- | ----- | ----- | 
| **Dukungan donasi berulang pada program/kampanye** | Belum ditentukan | Pilihan hanya dapat dilanjutkan jika didukung konfigurasi program. | Perlu konfirmasi: bentuk data dan lokasi konfigurasi. | 
| **Aktivasi opsi donasi berulang** | Belum ditentukan | Opsi harus dalam kondisi aktif. | Perlu konfirmasi: apakah terpisah dari dukungan program dan siapa pengaturnya. | 
| **Dukungan metode pembayaran terhadap donasi berulang** | Belum ditentukan | Belum ditentukan. | Perlu konfirmasi sesuai OQ-002. | 
| **Pilihan donasi berulang oleh donatur** | Belum ditentukan | Hanya dapat dipilih jika opsi tersedia. | Perlu konfirmasi; penyimpanan kesediaan bukan cakupan FR-002, melainkan FR-004. | 

#### 4. UI Mockup

**Sketsa tekstual — Kondisi 1: program mendukung donasi berulang**

```
+-------------------------------------------------------+
| [ INFORMASI KAMPANYE — sesuai FR-001 ]                |
|                                                       |
| PILIHAN DONASI                                        |
| [ Opsi donasi lain yang tersedia — jika ada ]         |
| [ DONASI BERULANG ] — tampil hanya jika didukung      |
|                                                       |
| [ LANJUTKAN ]                                         |
+-------------------------------------------------------+

```

**Sketsa tekstual — Kondisi 2: program atau metode pembayaran tidak mendukung donasi berulang**

```
+-------------------------------------------------------+
| [ INFORMASI KAMPANYE — sesuai FR-001 ]                |
|                                                       |
| PILIHAN DONASI                                        |
| [ Opsi donasi lain yang tersedia — jika ada ]         |
| (Pilihan donasi berulang tidak ditampilkan)           |
|                                                       |
| [ Penjelasan kepada donatur — teks perlu dikonfirmasi]|
+-------------------------------------------------------+

```

*Elemen, susunan halaman, label tombol, teks penjelasan, dan identitas visual harus dikonfirmasi kepada Baitulmal Tazkia. Arahan awal rapat untuk tampilan adalah navy blue dan putih, sesuai NFR-006 pada SRS Draft v0.2.*

#### 5. Non-Functional Requirement Terkait

| Aspek | Kebutuhan Awal | Catatan | 
| ----- | ----- | ----- | 
| **Keamanan** | FR-002 tidak memproses atau menyimpan data pembayaran; perlindungan data donatur mengikuti NFR-001 SRS. | Detail kebijakan keamanan perlu klarifikasi. | 
| **Kinerja** | Pilihan donasi berulang dapat ditampilkan dalam waktu yang wajar. | Target waktu respons belum ditetapkan; lihat OQ-014. | 
| **Kemudahan penggunaan** | Instruksi dan penjelasan kepada donatur jelas dan mudah dipahami. | Mengacu pada NFR-004; kriteria uji perlu klarifikasi dan ditinjau melalui UI/mockup. | 
| **Tampilan** | Antarmuka mengikuti arahan awal rapat: navy blue dan putih. | NFR-006 memiliki dasar tersedia; tampilan disesuaikan dengan identitas resmi organisasi. | 

### C. Kriteria Penerimaan

* \[ \] Pilihan donasi berulang hanya dapat dilanjutkan jika didukung konfigurasi program.

* \[ \] Sistem hanya menampilkan pilihan donasi berulang pada program atau kampanye yang mendukung dan mengaktifkannya.

* \[ \] Donatur dapat memilih opsi donasi berulang yang ditampilkan, lalu sistem melanjutkan ke proses pengaturan donasi (FR-003).

* \[ \] Jika program atau metode pembayaran tidak mendukung, sistem tidak menawarkan pilihan donasi berulang dan memberikan penjelasan kepada donatur.

> *Kriteria ini mengikuti SRS Draft v0.2 dan tetap perlu diperbarui setelah aturan bisnis dikonfirmasi.*

### D. Hal yang Perlu Dikonfirmasi

| No. | Pertanyaan / Keputusan yang Dibutuhkan | 
| ----- | ----- | 
| 1 | Apakah pendaftaran donasi berulang terhubung dengan penagihan otomatis (autodebit), pengingat untuk pembayaran manual, atau keduanya? (OQ-001) | 
| 2 | Metode pembayaran apa yang mendukung donasi berulang, dan pada tahap mana donatur memilih metode pembayaran? (OQ-002) | 
| 3 | Siapa yang berwenang mengatur dukungan serta mengaktifkan/menonaktifkan opsi donasi berulang pada program atau kampanye, dan di mana pengaturan dikelola? | 
| 4 | Apakah daftar opsi donasi ditampilkan langsung pada halaman kampanye (FR-001) atau pada langkah terpisah setelah tombol “Lanjutkan Donasi”? | 
| 5 | Apakah setiap program atau kampanye hanya memiliki satu opsi donasi berulang atau lebih dari satu? | 
| 6 | Apa isi dan bentuk penjelasan kepada donatur ketika opsi donasi berulang tidak tersedia? | 
| 7 | Apa langkah lanjutan bagi donatur ketika opsi donasi berulang tidak tersedia, dan apakah donatur dapat melanjutkan dengan opsi donasi lain? | 

### E. Catatan untuk Presentasi

* **Fokus Ruang Lingkup:** FR-002 menjelaskan kapan pilihan donasi berulang tersedia dan bagaimana donatur memilihnya. Fungsi ini berada setelah penyajian informasi kampanye (FR-001) dan sebelum pengaturan donasi (FR-003). Donatur hanya diberi pilihan donasi berulang apabila program/kampanye mendukung dan mengaktifkannya.

* **Batasan:** FR-002 tidak membahas nominal, jadwal/periode, peruntukan, penyimpanan kesediaan donasi, autentikasi donatur, pembayaran/penagihan, pengingat, maupun notifikasi.

* **Dasar Penyusunan:** SRS Draft v0.2 bagian FR-002 (pemicu, kondisi awal, alur utama, alur alternatif, dan kriteria penerimaan), serta NFR-001, NFR-004, NFR-006, OQ-001, OQ-002, dan OQ-014. Pemeriksaan dukungan oleh sistem merupakan kesimpulan dari kondisi awal dan kriteria penerimaan, bukan langkah yang tertulis secara eksplisit di SRS.

* **Status Dokumen:** Dokumen ini dirapikan dan dilengkapi untuk kebutuhan presentasi. Prioritas, tipe data, aturan metode pembayaran, mekanisme autodebit/pembayaran manual, dan detail UI belum ditetapkan oleh SRS; bagian tersebut secara sengaja tetap ditandai perlu konfirmasi dan tidak dianggap sebagai keputusan final klien.