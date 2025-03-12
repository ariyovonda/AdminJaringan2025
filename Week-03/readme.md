<div align="center">
  <h1 class="text-align: center;font-weight: bold">Praktikum 2 (Config & NTP Client)
  <br>Workshop Administrasi Jaringan 2025</h1>
  <h3 class="text-align: center;">Dosen Pengampu : Dr. Ferry Astika Saputra, S.T., M.Sc.</h3>
</div>
<br />
<div align="center">
  <img src="https://upload.wikimedia.org/wikipedia/id/4/44/Logo_PENS.png" alt="Logo PENS">
  <h3 style="text-align: center;">Disusun Oleh : </h3>
  <p style="text-align: center;">
  <strong>Nama : Bayu Ariyo Vonda Wicaksono<strong>
  <br><strong>NRP : 3123500017<strong>
  <br><strong>Kelas : 2 D3 IT A<strong>
  </p>
</div>

## A. Konfigurasi dan Instalasi NTP Client
  
### 1. Install NTP Client 
>$ apt -y install ntpsec

<div align="center">
<h3>
Hasil
</h3>

<p>
NTP Client telah terinstall pada OS Linux Debian 12 dengan masuk sebagai root terlebih dahulu.
</p>

### 2. Konfigurasi pada ntp.conf 
> $ nano /etc/ntpsec/ntp.conf

<div align="center">
<h3>
Hasil
</h3>

<p>
Hapus komen untuk Pool 0 hingga Pool 3, kemudian tambahkan dibawahnya "pool ntp.nict.jp iburst" Lalu simpan perubahan kemudian keluar.
</p>


![Image](Assets/ntpsec.jpg)

</div>

### 3. Restart NTP dan Verifikasi Status
> $ systemctl restart ntpsec

> $ ntpq -p

<div align="center">
<h3>
Hasil
</h3>

<p>
Fungsi restart NTP untuk membaca konfigurasi yang telah ditambahkan pada langkah kedua. Kemudian verifikasi status menampilkan daftar server NTP yang tergabung dalam pool zona Indonesia. Yang berarti server-server ini berada di wilayah Indonesia atau ditujukan untuk pengguna di Indonesia agar mendapatkan waktu yang lebih akurat dengan latensi lebih rendah.
</p>

</div>



</div>

## B. Instalasi dan Konfigurasi Samba
### 1. Install Samba pada terminal
> $ apt install -y samba

<div align="center">
<h3>
Hasil
</h3>

![Image](Assets/b1.png)
<p>
Instalasi samba menggunakan perintah seperti pada gambar, Masuk sebagai Root terlebih dahulu.
</p>

</div>

### 2. Membuat Folder kosong pada direktori Home dan mengubah izin.
> $ apt install -y samba

> $ chmod 777 /home/share


<div align="center">
<h3>
Hasil
</h3>

![Image](Assets/B3.png)
<p>
Pada Gambar tersebut berfungsi untuk membuat folder "share" pada direktori home kemudian mengubah izin pada folder tersebut agar semua pengguna dapat membaca,menulis dan mengeksekusi.
</p>

</div>

### 3. Konfigurasi smb.conf untuk public shared
> $ nano /etc/samba/smb.conf

<div align="center">
<h3>
Hasil
</h3>

![Image](Assets/IMG%20(5).png)
<p>
Pada bagian [global] tambahkan "unix charset = UTF-8" yang berfungsi untuk mengatur karakter encoding pada sistem Unix/Linux.
</p>

![Image](Assets/IMG%20(6).png)
<p>
Pada bagian interfaces tambahkan network yang akan diizinkan untuk mengakses, saya menggunakan network pada windows yaitu "172.20.10.0/24"
</p>

![Image](Assets/194532.png)
<p>
Tambahkan konfigurasi [Share] dan tambahkan juga path beserta izin folder seperti pada gambar kemudian simpan perubahan dan keluar.
</p>

</div>

### 4. Restart Samba service dan Pengujian untuk Public Shared
> $ systemctl restart smbd

<div align="center">
<h3>
Hasil
</h3>

![Image](Assets/IMG%20(9).png)
<p>
Untuk mengakses pada Windows gunakan IP yang terdaftar pada Linux kemudian akses seperti gambar diatas.
</p>

![Image](Assets/B5.png)
<p>
Disini saya menambahkan Folder "BERHASIL" di dalam nya, maka pada direktori home/share yang terdapat pada Linux Debian akan bertambah juga seperti pada Windows.
</p>

</div>

### 5. Mengakses Public shared menggunakan CLI dan file manager
> $ smbclient //100.100.20.98/share -N


<div align="center">
<h3>
Hasil
</h3>

![Image](Assets/B7.png)
<p>
Gambar tersebut membuktikan bahwa folder share yang dibuat menggunakan samba dapat diakses menggunakan CLI.
</p>

#### Akses via file manager
![Image](Assets/IMG%20(24).png)
<p>
Untuk mengakses menggunakan file manager dengan mengetik "smb://100.100.20.98/share" kemudian klik connect.

</div>

### 6. Konfigurasi Limited Shared Folder
> $ nano /etc/samba/smb.conf


<div align="center">
<h3>
Hasil
</h3>

![Image](Assets/IMG%20(22).png)
<p>
Tambahkan konfigurasi di dalam smb.conf untuk [Limited] seperti pada gambar diatas.
</p>

![Image](Assets/IMG%20(28).png)
<p>
Tambahkan user yang dapat mengakses folder tersebut
</p>

![Image](Assets/IMG%20(29).png)
<p>
Set password untuk user yang telah ditambahkan
</p>

</div>

### 7. Restart Samba service dan Pengujian untuk Limited shared folder
> $ systemctl restart smbd


<div align="center">
<h3>
Hasil
</h3>

![Image](Assets/194225.png)
<p>
Ketika mengakses Limited dengan network yang telah ditambahkan maka akan tampil seperti gambar tersebut. Masukkan username dan password yang telah dibuat pada langkah Sebelumnya.
</p>

![Image](Assets/194952.png)

### 8. Mengakses via CLI dan File manager untuk Limited shared folder
> $ smbclient //192.168.100.173/shared01 -U sambauser

<div align="center">
<h3>
Hasil
</h3>

![Image](Assets/195514.png)
<p>
Masukkan password yang telah dibuat, kemudian dapat mengakses Limited Akses Folder tersebut
</p>

### Mengakses via file manager
![Image](Assets/195501.png)
<p>
Masukkan IP yang terdaftar dan direktori limited
</p>

![Image](Assets/195556.png)
<p>
Masukkan username dan password yang telah dibuat pada langkah sebelumnya
</p>

![Image](Assets/195618.png)
<p>
Mengakses via File manager berhasil
</p>

</div>

## C. Rangkuman Package Management materi pada Ethol

1. Debian 12
Debian adalah sistem operasi Linux yang terkenal karena stabilitas dan keamanannya.
Versi terbaru, Debian 12 (Bookworm), menghadirkan berbagai pembaruan dan peningkatan kinerja dibandingkan versi sebelumnya.
2. Proses Instalasi Debian 12
Buku ini menguraikan langkah-langkah instalasi Debian 12, termasuk pemilihan paket dan pengaturan awal sistem.
Dijelaskan pula penggunaan Debian Installer untuk mengelola partisi, akun pengguna, serta konfigurasi jaringan dasar.
3. Pengelolaan Pengguna dan Hak Akses
Menjelaskan cara membuat, menghapus, serta mengatur akun pengguna dalam Debian 12.
Pembahasan mengenai sistem izin file (permissions), grup pengguna, dan kebijakan keamanan yang perlu diterapkan.
4. Pengelolaan Paket dengan APT
Cara menginstal, memperbarui, dan menghapus perangkat lunak menggunakan perintah seperti apt-get, apt-cache, dan dpkg.
Penjelasan tentang repositori Debian serta cara menambahkan sumber paket baru ke dalam sistem.
5. Konfigurasi Jaringan
Membahas dasar-dasar pengaturan jaringan, termasuk alamat IP, DNS, dan gateway.
Penggunaan perintah ip, ifconfig, serta nmcli untuk mengelola koneksi jaringan.
6. Administrasi Sistem
Memantau performa sistem dengan perintah seperti top, htop, df, dan free.
Mengelola layanan menggunakan systemd (systemctl start/stop/status).
Konfigurasi keamanan jaringan melalui ufw atau iptables.
7. Keamanan Sistem
Panduan untuk meningkatkan keamanan Debian 12, seperti pembaruan sistem, manajemen akses pengguna sudo, serta pengamanan akses SSH.
Penggunaan fail2ban sebagai perlindungan terhadap serangan brute-force.
8. Backup dan Pemulihan Data
Strategi pencadangan menggunakan rsync, tar, dan cron jobs.
Metode pemulihan sistem dalam situasi kehilangan data atau kerusakan sistem.
9. Automasi dengan Skrip Bash
Pengantar scripting menggunakan Bash untuk mengotomatisasi tugas administrasi sistem.
Contoh skrip sederhana untuk monitoring sistem dan pembaruan otomatis.

## Referensi
[NTP Client](https://www.server-world.info/en/note?os=Debian_12&p=ntp&f=1)

[Samba](https://www.server-world.info/en/note?os=Debian_12&p=samba&f=1)
</div>