# Laporan Task-2 Praktikum 2
## Sistem Organisasi Film Netflix

### 1. Header dan Fungsi Logging
![Library dan Fungsi Logging](foto_anthony/Screenshot%202025-04-30%20112438.png)

**Penjelasan**:
- Kumpulan library penting untuk operasi dasar sistem
- Implementasi fungsi logging dengan timestamp
- Error handling sederhana

**Penjelasan kode**
### 📁 Library yang Digunakan
- `stdio.h` — Operasi input/output dasar  
- `stdlib.h` — Manajemen memori dinamis  
- `string.h` — Manipulasi string  
- `pthread.h` — Pemrograman multithread  
- `time.h` — Penanganan waktu dan tanggal  
- `unistd.h` — System call Unix  
- `sys/stat.h` — Operasi file system  
- `ctype.h` — Penanganan karakter  
- `errno.h` — Manajemen error  
- `sys/wait.h` — Kontrol proses

### 📝 Fungsi `catat_log()`
- Membuka/membuat file `log.txt` dalam mode *append*
- Format waktu: `[HH:MM:SS]`
- Menulis pesan log dari parameter
- Menutup file setelah selesai
- Jika gagal, langsung `return` tanpa error

---

### 2. Fungsi Parsing CSV
![Fungsi Parse CSV](foto_anthony/Screenshot%202025-04-30%20112510.png)

**Fitur**:
- Handle field dengan koma dalam tanda kutip
- Pembersihan karakter khusus
- Pembagian field yang efisien

## 2️⃣ Fungsi Parsing CSV

### 🎯 Tujuan
Fungsi parsing CSV menangani baris data yang kompleks dan memiliki tanda kutip:

- Memisahkan kolom (field) berdasarkan koma `,`
- Mengabaikan koma yang berada dalam tanda kutip `"..."` agar tidak terpecah
- Membersihkan karakter newline di akhir field
- Menyimpan pointer ke tiap field dalam array

### ⚙️ Parameter Fungsi
- `line`: baris CSV yang akan dipecah
- `fields[]`: array penampung hasil field
- `max_fields`: batas maksimum field yang boleh diproses

### 📌 Catatan
Digunakan flag `dalam_tanda_kutip` sebagai penanda konteks parsing dalam/luar kutipan.

---

### 3. Menu Download & Ekstrak
![Proses Download](foto_anthony/Screenshot%202025-04-30%20112550.png)
![Proses Ekstraksi](foto_anthony/Screenshot%202025-04-30%20112618.png)

**Alur Kerja**:
1. Download file ZIP dari Google Drive
2. Ekstrak ke folder `data`
3. Hapus file ZIP setelah selesai

## 3️⃣ Menu 1: Download & Ekstrak File ZIP

### 🔧 Proses Otomatis
1. **Membuat direktori `data/`** jika belum ada (dengan permission 0777)
2. **Mendownload file ZIP**:
   - Menggunakan `fork()` untuk membuat child process
   - Menjalankan `wget` dengan URL file Google Drive di dalam child
   - Parent process menunggu dengan `wait()`
3. **Ekstraksi ZIP**:
   - Membuat child process baru dengan `fork()`
   - Mengeksekusi perintah `unzip` ke direktori `data/`
   - Parent menunggu hingga selesai
4. **Menghapus file ZIP** setelah proses ekstraksi sukses
5. **Mencatat semua aktivitas** ke file `log.txt`

### 🧵 Thread
- Fungsi dijalankan dalam `pthread_create`
- Thread keluar secara otomatis setelah selesai

---

### 4. Kelompokkan Film
#### Berdasarkan Abjad
![Kelompok Abjad](foto_anthony/Screenshot%202025-04-30%20112646.png)

**Klasifikasi**:
- Huruf A-Z → `A.txt`, `B.txt`, dst
- Angka → `1.txt`, `2.txt`, dst
- Lainnya → `#.txt`

#### Berdasarkan Tahun
![Kelompok Tahun](foto_anthony/Screenshot%202025-04-30%20112708.png)

**Struktur**:
- Satu file per tahun (`2020.txt`, `2021.txt`, dst)
- Format konsisten: `Judul - Tahun - Sutradara`

## 4️⃣ Menu 2: Kelompokkan Film

### 🔤 Berdasarkan Judul

- Membuka file CSV utama
- Membuat direktori `judul/` untuk menyimpan hasil
- Untuk setiap baris data film:
  - Mengidentifikasi huruf pertama dari judul film
  - Membuat file berdasarkan kategori:
    - Huruf A-Z → `A.txt`, `B.txt`, ..., `Z.txt`
    - Angka 0-9 → `1.txt`, `2.txt`, ..., `9.txt`, `0.txt`
    - Karakter lain → `#.txt`
  - Menulis informasi dalam format:
    ```
    Judul - Tahun - Sutradara
    ```
  - Mencatat aktivitas ke `log.txt`
- Menutup semua file setelah selesai

---

### 📅 Berdasarkan Tahun

- Membuka file CSV utama
- Membuat direktori `tahun/` untuk menyimpan hasil
- Untuk setiap baris data film:
  - Menggunakan tahun rilis sebagai nama file
    - Contoh: `2020.txt`, `1998.txt`
  - Menulis informasi dalam format:
    ```
    Judul - Tahun - Sutradara
    ```
  - Mencatat aktivitas ke `log.txt`
- Menutup semua file setelah selesai


### 5. Menu Laporan
![Pembuatan Laporan](foto_anthony/Screenshot%202025-04-30%20112730.png)

**Statistik**:
- Perhitungan film per negara
- Pembagian periode sebelum/sesudah 2000
- Format file: `report_DDMMYYYY.txt`

### 🧮 Proses
- Baca CSV → Kelompokkan per negara

### 📊 Isi Laporan
- Jumlah film **sebelum** dan **setelah** tahun 2000 per negara
- File: `report_DDMMYYYY.txt`
- Format rapi & terurut otomatis

---

### 6. Main Program
![Menu Utama](foto_anthony/Screenshot%202025-04-30%20120457.png)

### 🖥️ Fitur
1. Download & Ekstrak  
2. Kelompokkan Film  
3. Buat Laporan  
4. Keluar

### 🔄 Mekanisme
- Gunakan `pthread_create` → tiap fitur jalan paralel
- Tunggu dengan `pthread_join`
- Loop sampai pilih keluar

---
