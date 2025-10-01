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

Pada soal ke-Delapan
```
Ulmo, sebagai penjaga perairan, perlu mengirimkan data ramalan cuaca ke node Eru. 
Lakukan koneksi sebagai client dari node Ulmo ke FTP Server Eru menggunakan user ainur. Upload sebuah file berikut (link file). 
Analisis proses ini menggunakan Wireshark dan identifikasi perintah FTP yang digunakan untuk proses upload.

```

Kita harus mendownload dengan `wget` dengan command `wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=11ra_yTV_adsPIXeIPMSt0vrxCBZu0r33' -O cuaca.zip

lalu kita menggunakan unzip, namun sebelum itu kita harus `apt install unzip` agar bisa menggunakan unzip dan jangan lupa `apt install ftp` biar kita bisa menggunakan `ftp`

lalu kita upload dengan ip 192.219.1.1 dengan user ainur, lalu kita gunakan cmd `put cuaca.txt` biar bisa upload di ftp Eru.

<img src="blob:https://web.whatsapp.com/e2d1dea5-793b-4862-afd8-787d8df59e2c" alt="no 8"/><img width="959" height="658" alt="image" src="https://github.com/user-attachments/assets/100a2a65-ab89-41fc-83b5-b578a3f7cd07" />


Pada soal ke-Sembilan
```
Eru ingin membagikan "Kitab Penciptaan" di (link file) kepada Manwe. 
Dari FTP Server Eru, download file tersebut ke node Manwe. 
Karena Eru merasa Kitab tersebut sangat penting maka ia mengubah akses user ainur menjadi read-only. 
Gunakan Wireshark untuk memonitor koneksi, identifikasi perintah FTP yang digunakan, dan uji akses user ainur.
```

Pada soal ini 
Kita harus mendownload dengan `wget` dengan command `wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=11ra_yTV_adsPIXeIPMSt0vrxCBZu0r33' -O kitab.zip`

lalu kita menggunakan unzip, namun sebelum itu kita harus `apt install unzip` agar bisa menggunakan unzip dan jangan lupa `apt install ftp` biar kita bisa menggunakan `ftp`

lalu kita download dengan ip 192.219.1.1 dengan user ainur, lalu kita gunakan cmd `get kitab_penciptaan.txt` biar bisa download dari ftp Eru. Pastikan user ainur hanya memiliki akses read-only untuk menguji perubahan akses yang dilakukan oleh Eru.

<img src="blob:https://web.whatsapp.com/89aaf918-c300-4df2-b523-bf29fb1a9e92" alt="no 9 get data / read only"/><img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/cdd9cc7d-3529-4857-9730-43ec21ec4501" />

<img src="blob:https://web.whatsapp.com/1cc0f7bb-faef-480c-ab78-1e9e4b5857f3" alt="soal 9 wireshark"/><img width="958" height="726" alt="image" src="https://github.com/user-attachments/assets/4dd5585d-8274-4a13-ab10-e8c6424065ce" />


Pada soal ke-Sepuluh
```
Melkor yang marah karena tidak diberi akses, mencoba melakukan serangan dengan mengirimkan banyak sekali request ke server Eru. Gunakan command ping dari node Melkor ke node Eru dengan jumlah paket yang tidak biasa (spam ping misalnya 100 paket). Amati hasilnya, apakah ada packet loss? Catat average round trip time untuk melihat apakah serangan tersebut mempengaruhi kinerja Eru.
```

Pada soal ini  
untuk melakukan spam ping dari node Melkor ke node Eru. Berikut adalah isi scriptnya:  

```bash
#!/bin/bash
ping -c 100 192.219.1.1
```

dengan data yang kita amati, tidak adanya terjadi packet lost atau apapun itu, dikarenakan semua server berjalan dalam satu jaringan yang sama, dan terhubung denga ethernet. Tidak ada mungkin kejadian packet lost pada kondisi ini.

<img src="blob:https://web.whatsapp.com/f2d0931d-d4fc-426f-8ecf-4af34d900741"/><img width="698" height="176" alt="image" src="https://github.com/user-attachments/assets/fd676805-cc7b-47b3-8022-1f7b8fe0967c" />

Pada soal ke-Sebelas
```
Sebelum era koneksi aman, Eru sering menyelinap masuk ke wilayah Melkor. Eru perlu masuk ke node tersebut untuk memeriksa konfigurasi, 
namun ia tahu Melkor mungkin sedang memantau jaringan. Buktikan kelemahan protokol Telnet dengan membuat akun dan password baru di node 
Melkor kemudian menangkap sesi login Eru ke node Melkor menggunakan Wireshark. Tunjukkan bagaimana username dan password dapat terlihat sebagai plain text. 
```

Pada soal ini  
untuk membuktikan kelemahan protokol Telnet, berikut adalah isi scriptnya:  

```bash
#!/bin/bash
telnet 192.219.1.2
```

Setelah koneksi Telnet dimulai, kita dapat menggunakan Wireshark pada jaringan yang sama untuk menangkap paket data yang dikirimkan. Dengan menggunakan filter protokol `telnet`, analisis data akan menjadi lebih mudah. Selama sesi login berlangsung, Wireshark memungkinkan kita untuk melihat username dan password yang digunakan dalam bentuk teks biasa (plain text). Sebagai contoh, username `eru` dan password `password123` dapat terlihat langsung tanpa enkripsi. Hal ini terjadi karena protokol Telnet tidak menggunakan enkripsi untuk data yang dikirimkan, sehingga semua informasi, termasuk kredensial login, dapat dengan mudah dibaca oleh siapa saja yang memantau jaringan. Kelemahan ini menunjukkan mengapa Telnet tidak lagi digunakan di era koneksi aman. Sebagai gantinya, protokol seperti SSH yang mengenkripsi data digunakan untuk menghindari risiko penyadapan. Dengan langkah-langkah ini, kita dapat membuktikan bahwa Telnet tidak aman untuk digunakan dalam jaringan yang rentan terhadap penyadapan.

<img src="blob:https://web.whatsapp.com/558e8667-eea0-4c13-a36a-4b8623853b7e"/><img width="613" height="513" alt="image" src="https://github.com/user-attachments/assets/579f1efa-6f14-4469-9d8b-055594d2cfdf" />
<img src="blob:https://web.whatsapp.com/feeaec19-e8fa-4018-92b8-2a9ef957e0e9"/><img width="1600" height="700" alt="image" src="https://github.com/user-attachments/assets/9a0548bb-6e7a-4869-b16c-c20870b6fbcd" />


Pada soal ke-Dua belas
```
Eru mencurigai Melkor menjalankan beberapa layanan terlarang di node-nya. Lakukan pemindaian port sederhana dari node Eru ke 
node Melkor menggunakan Netcat (nc) untuk memeriksa port 21, 80, dalam keadaan terbuka dan port rahasia 666 dalam keadaan tertutup.
```

Pada soal ini  
untuk melakukan pemindaian port sederhana dari node Eru ke node Melkor menggunakan Netcat:  

```bash
#!/bin/bash
nc -zv 192.219.1.2 21 80 666
```

Dengan menggunakan perintah di atas, kita dapat memeriksa status port pada node Melkor. Hasilnya akan menunjukkan apakah port 21 dan 80 dalam keadaan terbuka dan port 666 dalam keadaan tertutup. Perintah `-z` digunakan untuk melakukan pemindaian tanpa mengirimkan data, dan `-v` digunakan untuk menampilkan output secara detail. Analisis ini membantu Eru memastikan layanan apa saja yang berjalan di node Melkor dan mengidentifikasi potensi layanan terlarang.

Namun kita pun harus membuka port yang harus di open dengan `ufw` dan `service port 80 = apache2, dan 21 servie port ftp`
dengan ini kita harus menginstall `apt install apache2 vsftpd` agar bisa diping oleh netcat

<img src="blob:https://web.whatsapp.com/ee2642cf-c12f-45bb-ab3f-1bf4237583ba"/><img width="565" height="285" alt="image" src="https://github.com/user-attachments/assets/1ca0fcb6-f7f0-4d40-a1d8-b1e5296e9cc3" />

ada soal ke-Sebelas
```
Sebelum melakukan koneksi SSH dari node Varda ke Eru, kita perlu memastikan bahwa SSH telah terinstal di node Varda. Berikut adalah langkah-langkah untuk menginstal SSH:

1. Update daftar paket:
    ```bash
    sudo apt update
    ```

2. Instal OpenSSH Client:
    ```bash
    sudo apt install openssh-client
    ```

3. Pastikan OpenSSH Client telah terinstal dengan memeriksa versinya:
    ```bash
    ssh -V
    ```

Setelah SSH terinstal, kita dapat melanjutkan dengan melakukan koneksi SSH dari node Varda ke Eru menggunakan perintah berikut:

```bash
#!/bin/bash
ssh eru@192.219.1.1
```

Setelah koneksi SSH dimulai, kita dapat menggunakan Wireshark pada jaringan yang sama untuk menangkap paket data yang dikirimkan. Namun, berbeda dengan Telnet, data yang dikirimkan melalui SSH dienkripsi sehingga tidak dapat dibaca secara langsung. Dengan menggunakan filter protokol `ssh`, kita dapat melihat bahwa semua paket data yang ditangkap hanya berupa data terenkripsi. Sebagai contoh, meskipun username `eru` dan password digunakan untuk login, informasi tersebut tidak dapat dilihat dalam bentuk teks biasa (plain text) karena telah dienkripsi oleh protokol SSH.

Keamanan ini disebabkan oleh penggunaan algoritma enkripsi yang kuat dalam SSH, yang memastikan bahwa data yang dikirimkan tidak dapat diakses oleh pihak yang tidak berwenang. Dengan langkah-langkah ini, kita dapat membuktikan bahwa SSH jauh lebih aman dibandingkan Telnet untuk koneksi administratif, terutama dalam jaringan yang rentan terhadap penyadapan. Paket-paket terenkripsi yang ditangkap oleh Wireshark menjadi bukti nyata bahwa SSH melindungi data sensitif dari pengintaian.

<img src="blob:https://web.whatsapp.com/e2195600-10e2-4588-bde7-b32852e7901c" alt="no 13"/><img width="877" height="498" alt="image" src="https://github.com/user-attachments/assets/fd6e4abc-ffe0-41ed-9899-b020571a35af" />

<img src="blob:https://web.whatsapp.com/1c7d1f69-963b-42ba-9e64-314f1964e3e5" alt="no 13 wireshark"/><img width="1600" height="847" alt="image" src="https://github.com/user-attachments/assets/1cdfc11e-c144-4b32-98cf-ca49cc913da1" />
