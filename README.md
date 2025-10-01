# Jarkom-Modul-1-2025-K-16

### MEMBER
1. Muhammad Ardiansyah Tri Wibowo - 5027241091
2. Nisrina Bilqis - 5027241054

### AKSES SOAL
https://docs.google.com/document/d/1DJRVpIwqNb6KUA0gsWtQ4rguR8S7h-zebR1OGQ9xkQw/

### REPORTING 
Pada soal pertama yaitu
```
Untuk mempersiapkan pembuatan entitas selain mereka,
Eru yang berperan sebagai Router membuat dua Switch/Gateway.
Dimana Switch 1 akan menuju ke dua Ainur yaitu Melkor dan Manwe.
Sedangkan Switch 2 akan menuju ke dua Ainur lainnya yaitu Varda dan Ulmo.
Keempat Ainur tersebut diberi perintah oleh Eru untuk menjadi Client.

```
Dengan modul yang telah diberikan, yang dapat diakses pada laman berkut 

https://github.com/lab-kcks/Modul-Komdat-Jarkom/tree/main/Modul-GNS3

Dengan mengikuti step ini, maka kita sudah dapat menyelesaikan soal pertama

<img src="blob:https://web.whatsapp.com/f42060b3-9d89-4a8f-bbd2-0cf16f6549f1"/><img width="1575" height="546" alt="image" src="https://github.com/user-attachments/assets/31b850e2-6b74-4b64-a533-d7664a15a976" />

Pada soal kedua
```
Karena menurut Eru pada saat itu Arda (Bumi) masih terisolasi dengan dunia luar,
maka buat agar Eru dapat tersambung ke internet.

```

Dengan mengikuti sesuai step yang diberikan modul, maka soal ini bisa diselesai dengan baik.

Berikut lampiran beberapa dokumentasi konfigurasi

<img src="blob:https://web.whatsapp.com/8944b7a2-e2f0-455b-9cf8-92491c139df4"/><img width="789" height="189" alt="image" src="https://github.com/user-attachments/assets/364f700b-75cf-4b71-b2eb-c4f7ad5ca16f" />


Pada soal ketiga
```
Sekarang pastikan agar setiap Ainur (Client) dapat terhubung satu sama lain.
```

kita bisa melakukan ping pada tiap clientnya, dengan menjalankan `soal3.sh` kita bisa ping semua client sekaligus
kita manfaatkan command `ping [ip client/target] -c 10` yang kita akan limit paketnya hanya 10 saja.

<img>

Pada soal Keempat
```
Setelah berhasil terhubung, sekarang Eru ingin agar setiap Ainur (Client) dapat mandiri.
Oleh karena itu pastikan agar setiap Client dapat tersambung ke internet.

```

Kita bisa melakukan sesuai apa yang ada di modul yang diberikan oleh assisten, maka dengan apa yang sudah diberikan, bisa menjalankan script `soal4.sh` untuk set nameserver dan ping google.com dengan paket yang dibatasi

<img src="blob:https://web.whatsapp.com/814426c5-3071-4779-9e43-e99697fb37cd"/><img width="789" height="289" alt="image" src="https://github.com/user-attachments/assets/953a2876-71fa-4e00-9ece-d49761fbd5e9" />

Pada soal kelima
```
Ainur terkuat Melkor tetap berusaha untuk menanamkan kejahatan ke dalam Arda (Bumi). 
Sebelum terjadi kerusakan, Eru dan para Ainur lainnya meminta agar semua konfigurasi 
tidak hilang saat semua node di restart.
```

Pada soal ini kita diminta untuk ketika node direstart konfigurasinya tidak hilang, sesuai yang ada dimodul, kita bisa menggunakan `/root/.bashrc` atau membuat script tersendiri agar tiap sekali kita restart bisa langsung terkonfigurasi secara otomatis tanpa mengulang dari awal.

Saya memanfaatkan keduanya, salah satu configurasi skript `soal5.sh` sudah cukup untuk membantu dari soal 1-10.

<img width="939" height="965" alt="image" src="https://github.com/user-attachments/assets/f21690bb-a4bd-48bd-a063-cc4d17530403" />

Pada soal ke-enam
```
Setelah semua Ainur terhubung ke internet, Melkor mencoba menyusup ke dalam komunikasi antara Manwe dan Eru. 
Jalankan file berikut (link file) lalu lakukan packet sniffing menggunakan Wireshark pada koneksi antara Manwe dan Eru, 
lalu terapkan display filter untuk menampilkan semua paket yang berasal dari atau menuju ke IP Address Manwe. 
Simpan hasil capture tersebut sebagai bukti.
```

Pada soal ini sendiri, kita diminta untuk shifting terhadap jaringan Manwe dengan Eru, dengan menjalankan file yang diberikan, kita mendapatkan hasil yang dapat dilihat di `soal6.pcapng` atau melalui dokumentasi berikut:

<img src="blob:https://web.whatsapp.com/ae7dbbfa-4c64-4a5a-9387-dbbf09800d87"/><img width="1600" height="850" alt="image" src="https://github.com/user-attachments/assets/8f976ece-b0a0-4676-a909-5d65b9e76281" />


Pada soal ke-tujuh
```
Untuk meningkatkan keamanan, Eru memutuskan untuk membuat sebuah FTP Server di node miliknya. 
Lakukan konfigurasi FTP Server pada node Eru. Buat dua user baru: ainur dengan hak akses write&read 
dan melkor tanpa hak akses sama sekali ke direktori shared. Buktikan hasil tersebut dengan membuat file 
teks sederhana kemudian akses file tersebut menggunakan kedua user.
```

Pada soal ini kita dapat menginstall `apt install vsftpd` sebagai FTP Server pada eru, dan Client menggunakan  `apt install ftp`. lengkapnya melalui skript `soal7.sh` sudah bisa dijalankan secara otomatis dengan membuat user Melkor dan Ainur.

soal7.sh
```
# Konfigurasi user ainur dan melkor
echo "Membuat user ainur dan melkor..."
useradd -m ainur
## Set password untuk user ainur yaitu ainur 
echo "ainur:ainur" | chpasswd
# Direktori home yang dimiliki root (Wajib untuk vsftpd keamanan modern)
mkdir -p /home/ainur/ftp_root && chown root:root /home/ainur/ftp_root && chmod 555 /home/ainur/ftp_root

# Direktori untuk file bersama (tempat ainur bisa menulis)
mkdir /home/ainur/ftp_root/share_files && chown ainur:ainur /home/ainur/ftp_root/share_files && chmod 775 /home/ainur/ftp_root/share_files
usermod -d /home/ainur/ftp_root ainur

echo "User ainur sudah dibuat."
echo "Membuat user melkor..."
useradd -m melkor
## Set password untuk user melkor yaitu melkor
echo "melkor:melkor" | chpasswd
mkdir -p /home/melkor/no_access && chown root:root /home/melkor/no_access && chmod 500 /home/melkor/no_access && usermod -d /home/melkor/no_access melkor
cd /home/ainur/ftp_root/ && chmod u-w share_files && chmod 555 share_files

```

setelah itu kita melakukan `service vsftpd restart` agar config bisa terapply dengan baik

<img src="blob:https://web.whatsapp.com/46c3d41e-069b-4592-9339-7ef01cd2b4e3"/><img width="947" height="522" alt="image" src="https://github.com/user-attachments/assets/0d1dc757-b9c9-498d-a2e5-fa6ec7ff3eb2" />

<img src="blob:https://web.whatsapp.com/7d68f4f8-d93b-4a17-a55c-dace70783495"/><img width="947" height="435" alt="image" src="https://github.com/user-attachments/assets/14ad71ce-1f8b-4cef-bc04-92870364fcb2" />



