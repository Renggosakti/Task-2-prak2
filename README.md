[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/Eu-CByJh)
|    NRP     |      Name      |
| :--------: | :------------: |
| 5025241103 |  Uwais Achmad  |
| 5025241085 |Mario Napitupulu|
| 5025241072 | Arya Rangga p.p|

# Praktikum Modul 3 _(Module 3 Lab Work)_

### Laporan Resmi Praktikum Modul 3 _(Module 3 Lab Work Report)_

Di suatu pagi hari yang cerah, Budiman salah satu mahasiswa Informatika ditugaskan oleh dosennya untuk membuat suatu sistem operasi sederhana. Akan tetapi karena Budiman memiliki keterbatasan, Ia meminta tolong kepadamu untuk membantunya dalam mengerjakan tugasnya. Bantulah Budiman untuk membuat sistem operasi sederhana!

_One sunny morning, Budiman, an Informatics student, was assigned by his lecturer to create a simple operating system. However, due to Budiman's limitations, he asks for your help to assist him in completing his assignment. Help Budiman create a simple operating system!_

### Soal 1

**Answer:**

- **Code:**
```bash
sudo apt update
sudo apt install -y build-essential bison flex libssl-dev libelf-dev bc qemu grub-pc-bin grub-efi dosfstools mtools cpio busybox-static
```

- **Explanation:**
Perintah ini digunakan untuk menginstall semua dependensi dan tool yang dibutuhkan untuk membangun sistem operasi Budiman.

### Soal 2

**Answer:**

- **Code:**
```bash
sudo bash
mkdir -p myramdisk/{bin,dev,proc,sys,etc,root,sisop,home/Budiman,home/guest,home/praktikan1,home/praktikan2}
cp -a /dev/null myramdisk/dev
cp -a /dev/tty* myramdisk/dev
cp -a /dev/zero myramdisk/dev
cp -a /dev/console myramdisk/dev
cp /usr/bin/busybox myramdisk/bin
cd myramdisk/bin
./busybox --install .
```

- **Explanation:**
1. Perintah `mkdir -p` digunakan untuk membuat direktori yang diperlukan oleh sistem operasi Budiman sesuai perintah dosen.
2. Subdirektori:
```
    bin: Untuk binary/executable.

    dev: Untuk file device (e.g., null, tty).

    proc, sys: Untuk filesystem virtual kernel.

    etc: Konfigurasi sistem.

    root, home/*: Direktori home pengguna
```
3. `cp -a:` Menyalin file dengan preserve semua atribut (permission, timestamp, dll.).

    File device yang disalin:

        null: Device untuk menghilangkan output (/dev/null).

        tty*: Terminal virtual (e.g., tty1, ttyS0).

        zero: Device yang menghasilkan null bytes (/dev/zero).

        console: Device untuk kernel messages (/dev/console).

4. Menyalin Busybox ke `myramdisk/bin` untuk menjadi dasar sistem dan menginstal busybox



### Soal 3

**Answer:**

- **Code:**
File `etc/passwd`:
```
root:$1$bz3KuNW0$0eGCjU8imqhH9mmcFdwD.1:0:0:root:/root:/bin/sh
Budiman:$1$gVeeaTxC$EExfcCECkjpcyIEvLLhUR1:1000:100:Budiman:/home/Budiman:/bin/sh
guest:$1$LeOrV5Wl$7QGTT5p.9WYBmIi7ukYms1:1001:100:guest:/home/guest:/bin/sh
praktikan1:$1$vGnfB2HV$ou0WzBlKXuWIyfrv6C3DX1:1002:100:praktikan1:/home/praktikan1:/bin/sh
praktikan2:$1$qnvpFaRm$0sgmoxSxWZVf9Gysn/2Sq/:1003:100:praktikan2:/home/praktikan2:/bin/sh
```

File `etc/group`:
```
root:x:0:root
bin:x:1:bin,daemon
daemon:x:2:daemon
tty:x:5:Budiman,guest,praktikan1,praktikan2
disk:x:6:root
wheel:x:10:root,Budiman
users:x:100:Budiman,guest,praktikan1,praktikan2
Budiman:x:1000:
guest:x:1001:
praktikan1:x:1002:
praktikan2:x:1003:
```

- **Explanation:**
1. Buka terminal, pastikan berada di folder `osboot`:
`cd ~/osboot`
2. Edit file passwd untuk mendefinisikan user dan home directory:
`sudo nano myramdisk/etc/passwd`
3. Masukkan kode tadi
4. Format file `/etc/passwd` adalah: `username:password_hash:uid:gid:comment:home_dir:shell`
5. Setiap user punya UID unik dan shell `/bin/sh`
6. Password sudah di-hash menggunakan `openssl passwd -1 <password>`
7. Edit file grup:
`sudo nano myramdisk/etc/group`
8. Masukkan isi group tadi
9. Grup `wheel` memberi Budiman akses selevel superuser
10. `tty` memberi akses ke terminal
11. `users` adalah grup umum untuk semua user biasa

### Soal 4

**Answer:**

- **Code:**
```bash
sudo chmod 700 /home/user/osboot/myramdisk/root
sudo chown root:root /home/user/osboot/myramdisk/root
```

- **Explanation:**
Memberikan hak akses penuh hanya kepada root agar direktori `./root` tidak bisa diakses oleh user lain.

### Soal 5

**Answer:**

- **Code:**
```bash
sudo chmod 700 /home/user/osboot/myramdisk/home/Budiman
sudo chmod 700 /home/user/osboot/myramdisk/home/guest
sudo chmod 700 /home/user/osboot/myramdisk/home/praktikan1
sudo chmod 700 /home/user/osboot/myramdisk/home/praktikan2
```

- **Explanation:**
Setiap user hanya bisa mengakses direktori miliknya sendiri dan tidak bisa mengakses milik user lain.

### Soal 6

**Answer:**

- **Code:**
Tambahkan pada file `etc/profile`:
```bash
#!/bin/sh
cat << "EOF"
 __    __   ___ _        __  ___  ___ ___   ___      ______  ___
|  |__|  | /  _| |      /  ]/   \|   |   | /  _]    |      |/   \
|  |  |  |/  [_| |     /  /|     | _   _ |/  [_     |      |     |
|  |  |  |    _| |___ /  / |  O  |  \_/  |    _]    |_|  |_|  O  |
|  `  '  |   [_|     /   \_|     |   |   |   [_       |  | |     |
 \      /|     |     \     |     |   |   |     |      |  | |     |
  \_/\_/ |_____|_____\____|\___/|___|___|_____|      |__|  \___/
EOF

cat << "EOF"
 $$$$$$\  $$$$$$\ $$\ $$$$$$\ $$$$$$$\
$$  __$$\$$  __$$\$  $$  __$$\$$  ____|
$$ /  $$ $$ /  \__\_/\__/  $$ $$ |      
$$ |  $$ \$$$$$$\     $$$$$$  $$$$$$$\
$$ |  $$ |\____$$\   $$  ____/\_____$$\
$$ |  $$ $$\   $$ |  $$ |     $$\   $$ |
 $$$$$$  \$$$$$$  |  $$$$$$$$\\$$$$$$  |
 \______/ \______/   \________|\______/
EOF

```

- **Explanation:**
1. Buka terminal dan buat/edit file berikut:
`sudo nano myramdisk/etc/profile`
2. Buat sambutan dengan Menampilkan banner ASCII saat user login sebagai bentuk sambutan yang menarik serta gunakan `echo`
3. `cat << "EOF" ... EOF:` Menampilkan banner teks saat login

### Soal 7

**Answer:**

- **Code:**
```bash
if [ -x /bin/whoami ]; then
    echo "Hello $(/bin/whoami)"
fi
```

- **Explanation:**
1. Menampilkan ucapan selamat datang yang menyebutkan nama user setelah login.
2. `if [ -x /bin/whoami ]; then [ -x /bin/whoami ]:` Mengecek apakah file /bin/whoami executable (memiliki izin eksekusi).
3. `if ... then:` Jika kondisi terpenuhi (file executable), jalankan perintah dalam blok then.
3. `$(/bin/whoami):` Mengeksekusi perintah /bin/whoami (menampilkan username pengguna saat ini) dan menyimpan hasilnya.
4. `echo "Hello ...":` Menampilkan pesan "Hello" diikuti username (misal: Hello root).
5. `fi` Menandakan akhir dari blok if

### Soal 8

**Answer:**

- **Code:**
```bash
PS1='\u@\h:\w\$ '
export PS1
PATH="/bin:/sbin:/usr/bin:/usr/sbin"
export PATH
```
```
Terdapat perubahan pada Config kernel 

Device Drivers -> Graphics Support -> Frame Buffer Devices -> Support for Frame Buffer Devices -> VESA VGA
Device Drivers -> Graphics Support -> Frame Buffer Devices -> Support for Frame Buffer Devices -> SImple framebuffer support
Device Drivers -> Graphics Support -> Console display driver support -> Framebuffer Console support
Device Drivers -> Firmware Devices -> Mark VGA/VBE/EFI

kemudian save dengan -j$(nproc)

Command qemu jadi 
qemu-system-x86_64   -m 256   -kernel bzImage   -initrd myramdisk.gz   -vga std   -append "quiet vga=0x317"
```

- **Explanation:**
1. Mengubah tampilan prompt agar lebih mudah dibaca dan menyerupai terminal pengguna.
2. `PS1:` Variabel yang mendefinisikan tampilan prompt di shell.
3. `\u:` Username pengguna.
4. `\h:` Hostname (nama mesin).
5. `\w:` Direktori kerja saat ini (full path).
6. `\$:` Menampilkan $ untuk user biasa atau # untuk root.
7. Contoh hasil: `user@ubuntu:/home/user$` 
8. PATH: Variabel yang berisi daftar direktori tempat shell mencari perintah.
9. /bin:/sbin:...: Memprioritaskan pencarian perintah di:

        /bin (binary esensial sistem),

        /sbin (binary sistem untuk root),

        /usr/bin (binary untuk user),

        /usr/sbin (binary admin untuk user).

10. Export `PATH` dan `PS1` mengekspor agar berlaku variabel global dan semua Sub-shell

### Soal 9

**Answer:**

- **Code:**
```bash
cp budiman myramdisk/bin/
chmod +x myramdisk/bin/budiman
```
```
git clone https://github.com/morisab/budiman-text-editor.git
cd budiman-text-editor

g++ main.cpp -o budiman

./budiman
```

- **Explanation:**
1. Menambahkan binary editor `budiman` ke dalam sistem operasi Budiman agar user bisa mengedit file teks.
2. Clone the repository
3. compile program
4. jalankan program dengan `./budiman,
5. Note : 

### Soal 10

**Answer:**

- **Code:**
```bash
mkdir -p iso_root/boot/grub
cp bzImage iso_root/boot/
cp myramdisk.gz iso_root/boot/
touch iso_root/boot/grub/grub.cfg
```

- **Explanation:**
1. Seluruh sistem dikemas menjadi file ISO menggunakan `grub-mkrescue` agar bisa dijalankan di QEMU atau diserahkan ke dosen. gunakan `grub-mkrescue -o budiman_os.iso iso_root/`
2. Jalankan ISO Testing dengan `qemu-system-x86_64 -m 256 -cdrom budiman_os.iso -vga std`

