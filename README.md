# Laporan Task-2 Praktikum 2
## Sistem Organisasi Film Netflix

### 1. Header dan Fungsi Logging
![Library dan Fungsi Logging](foto_anthony/Screenshot%202025-04-30%20112438.png)

**Penjelasan**:
- Kumpulan library penting untuk operasi dasar sistem
- Implementasi fungsi logging dengan timestamp
- Error handling sederhana

### 2. Fungsi Parsing CSV
![Fungsi Parse CSV](foto_anthony/Screenshot%202025-04-30%20112510.png)

**Fitur**:
- Handle field dengan koma dalam tanda kutip
- Pembersihan karakter khusus
- Pembagian field yang efisien

### 3. Menu Download & Ekstrak
![Proses Download](foto_anthony/Screenshot%202025-04-30%20112550.png)
![Proses Ekstraksi](foto_anthony/Screenshot%202025-04-30%20112618.png)

**Alur Kerja**:
1. Download file ZIP dari Google Drive
2. Ekstrak ke folder `data`
3. Hapus file ZIP setelah selesai

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

### 5. Menu Laporan
![Pembuatan Laporan](foto_anthony/Screenshot%202025-04-30%20112730.png)

**Statistik**:
- Perhitungan film per negara
- Pembagian periode sebelum/sesudah 2000
- Format file: `report_DDMMYYYY.txt`

### 6. Main Program
![Menu Utama](foto_anthony/Screenshot%202025-04-30%20120457.png)

**Fitur**:
1. Download & Ekstrak
2. Kelompokkan Film  
3. Buat Laporan
0. Keluar
