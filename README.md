### Laporan Task-2 Praktikum 2

1. Header dan Fungsi Logging
[lampiran_satu](foto_anthony/)

Penjelasan:

Program menggunakan berbagai library standar C untuk:

Operasi input/output dasar (stdio.h)

Manajemen memori dinamis (stdlib.h)

Manipulasi string (string.h)

Pemrograman multithread (pthread.h)

Penanganan waktu dan tanggal (time.h)

System calls Unix (unistd.h)

Operasi filesystem (sys/stat.h)

Penanganan karakter (ctype.h)

Manajemen error (errno.h)

Kontrol proses (sys/wait.h)

Fungsi catat_log() bertujuan untuk:

Membuat/membuka file log.txt dalam mode append

Mencatat setiap aktivitas dengan format waktu [HH:MM:SS]

Menulis pesan log yang diterima sebagai parameter

Menutup file setelah selesai menulis

Jika gagal membuka file, fungsi akan langsung kembali tanpa error

2. Fungsi Parsing CSV
Penjelasan:
Fungsi ini dirancang untuk:

Memproses satu baris data CSV dengan format kompleks

Menangani field yang mengandung koma dalam tanda kutip

Memisahkan field-field berdasarkan delimiter koma

Mengabaikan koma yang berada dalam tanda kutip

Menyimpan pointer ke setiap field yang dipisahkan

Membersihkan karakter newline di akhir setiap field

Menerima parameter:

line: baris teks dari file CSV

fields: array untuk menyimpan hasil pemisahan

max_fields: batas maksimum field yang diproses

Menggunakan flag dalam_tanda_kutip untuk membedakan koma dalam string

3. Menu 1: Download & Ekstrak File ZIP
Penjelasan:
Fungsi ini melakukan:

Pembuatan direktori 'data' dengan permission penuh

Proses download:

Membuat child process menggunakan fork()

Pada child process: menjalankan wget untuk download file ZIP dari URL Google Drive

Pada parent process: menunggu child selesai

Proses ekstraksi:

Membuat child process baru

Pada child process: mengekstrak file ZIP ke folder 'data' menggunakan unzip

Pada parent process: menunggu proses ekstraksi selesai

Penghapusan file ZIP setelah ekstraksi

Pencatatan log otomatis untuk setiap tahap

Keluar dari thread setelah semua proses selesai

4. Menu 2: Kelompokkan Film
Berdasarkan Abjad:

Membuka file CSV utama

Membuat direktori 'judul' untuk penyimpanan

Memproses setiap baris data film:

Mengidentifikasi huruf pertama judul

Membuat file berdasarkan kategori:

Huruf A-Z -> A.txt, B.txt, dst

Angka 0-9 -> 1.txt, 2.txt, dst

Karakter lain -> #.txt

Menulis data dalam format: Judul - Tahun - Sutradara

Mencatat aktivitas ke log.txt

Menutup file setelah selesai

Berdasarkan Tahun:

Membuka file CSV utama

Membuat direktori 'tahun' untuk penyimpanan

Memproses setiap baris data film:

Menggunakan tahun rilis sebagai nama file

Format penamaan: YYYY.txt (contoh: 2020.txt)

Menulis data dalam format: Judul - Tahun - Sutradara

Mencatat aktivitas ke log.txt

Menutup file setelah selesai

5. Menu 3: Buat Laporan
Penjelasan:
Fungsi ini:

Membuka dan membaca file CSV utama

Membuat struktur data untuk menyimpan statistik per negara:

Nama negara

Jumlah film sebelum tahun 2000

Jumlah film setelah tahun 2000

Memproses setiap baris data:

Mengelompokkan film berdasarkan negara

Menghitung film berdasarkan periode tahun

Membuat nama file laporan berdasarkan tanggal saat ini (format: report_DDMMYYYY.txt)

Menulis laporan berisi:

Daftar negara

Jumlah film sebelum dan setelah tahun 2000 per negara

Format penomoran otomatis

Menutup file setelah selesai

6. Main Program
Penjelasan:
Program utama menyediakan:

Menu interaktif dengan pilihan:

Download & Ekstrak

Kelompokkan Film

Buat Laporan

Keluar

Mekanisme pembuatan thread untuk setiap fitur:

Menggunakan pthread_create

Menunggu thread selesai dengan pthread_join

Loop terus menerus sampai user memilih keluar

Antarmuka sederhana dengan input nomor pilihan
