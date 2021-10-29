# Jarkom-Modul-2-C08-2021

Berikut adalah laporan resmi Praktikum Jaringan Komputer Modul 2 tahun 2021

Anggota Kelompok C08 :

- 05111940000100 - Muhammad Raihan
- 05111940000208 - Inez Yulia Amanda
- 05111940000209 - Refaldyka Galuh Pratama

## 1. EniesLobby akan dijadikan sebagai DNS Master, Water7 akan dijadikan DNS Slave, dan Skypie akan digunakan sebagai Web Server. Terdapat 2 Client yaitu Loguetown, dan Alabasta. Semua node terhubung pada router Foosha, sehingga dapat mengakses internet
1. Klik `Servers` di kiri atas
2. Klik `local`
3. Klik `Add blank project`
4. Masukkan nama `project` 
5. Klik `Add project`
6. Klik tombol `Add a node` di samping kiri
7. Lalu tarik `ubuntu-`1 ke area kosong di halaman
8. Tunggu sampai loading selesai
9. Jika berhasil akan menampilkan tampilan yang mirip dengan ini
    ![1.1](assets/1a.png)
11. Klik kanan dan `change hostname` menjadi `Foosha`
    ![1.2](assets/1b.png)
13. Klik kanan lagi dan `change symbol` menjadi symbol `router`
    ![1.3](assets/1c.png)
15. Lakukanlah langkah 6 hingga 10 untuk `LogueTown`, `Alabasta`, `EniesLobby`, `Water7`, dan `Skypie`. Sehingga menjadi seperti pada gambar
    ![1.4](assets/1d.png)
17. Jika sudah klik tombol `Add a node` di samping kiri lagi
18. Tarik `NAT` dan dua `Switch` ke area kosong
    ![1.5](assets/1e.png)
19. Gunakan menu `Add a Link` dan tambahkan link seperti pada gambar berikut pada setiap node
    ![1.6](assets/1f.png)
21. Lalu kita setting network masing-masing node dengan fitur Edit network configuration seperti yang ditunjukkan disini sebelumnya, kita bisa menghapus semua settingnya dan  mengisi dengan settingan di bawah
  - Foosha
  ```
  auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.18.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.18.2.1
	netmask 255.255.255.0
  ```
  - Loguetown
  ```
  auto eth0
iface eth0 inet static
	address 10.18.1.2
	netmask 255.255.255.0
	gateway 10.18.1.1
  ```
  - Alabasta
  ```
  auto eth0
iface eth0 inet static
	address 10.18.1.3
	netmask 255.255.255.0
	gateway 10.18.1.1
  ```
  - EniesLobby
  ```
  auto eth0
iface eth0 inet static
	address 10.18.2.2
	netmask 255.255.255.0
	gateway 10.18.2.1
  ```
  - Water7
  ```
  auto eth0
iface eth0 inet static
	address 10.18.2.3
	netmask 255.255.255.0
	gateway 10.18.2.1
  ```
  - Skypie
  ```
  auto eth0
iface eth0 inet static
	address 10.18.2.4
	netmask 255.255.255.0
	gateway 10.18.2.1
  ```
22. Restart semua node
23. Topologi yang dibuat sudah bisa berjalan secara lokal, tetapi kita belum bisa mengakses jaringan keluar. Maka kita perlu melakukan beberapa hal.
24. Ketikkan `vim .bashrc` pada router `Foosha` dan masukkan command berikut
   ```
   iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.18.0.0/16
   ```
26. Ketikkan command `cat /etc/resolv.conf` di `Foosha` kemudian ingat ingat nameservernya
27. Pada node LogueTown, Alabasta, EniesLobby, Water7, dan Skypie. Ketikkan command `vim .bashrc` kemudian masukkan command 
   ```
   echo nameserver 192.168.122.1 > /etc/resolv.conf
   ```
29. Semua node sekarang seharusnya sudah bisa melakukan ping ke google, yang artinya adalah sudah tersambung ke internet
## 2. Buat website utama dengan mengakses franky.c08.com dengan alias www.franky.c08.com pada folder kaizoku

## 3. Buat subdomain super.franky.c08.com dengan alias www.super.franky.c08.com yang diatur DNS nya di EniesLobby dan mengarah ke Skypie

## 4. Buat juga reverse domain untuk domain utama

## 5. Buat Water7 sebagai DNS Slave untuk domain utama

## 6. Setelah itu terdapat subdomain mecha.franky.c08.com dengan alias www.mecha.franky.c08.com yang didelegasikan dari EniesLobby ke Water7 dengan IP menuju ke Skypie dalam folder sunnygo

## 7. Buatkan subdomain melalui Water7 dengan nama general.mecha.franky.c08.com dengan alias www.general.mecha.franky.c08.com yang mengarah ke Skypie

## 8. Konfigurasi Webserver dengan domain www.franky.c08.com dan DocumentRoot pada /var/www/franky.c08.com.
1. Pindah ke direktori `/etc/apache2/sites-available` lalu *copy* file **000-default.conf** ke **franky.c08.com.conf** dengan perintah 
    ```
    cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/franky.c08.com.conf
    ```
2. Edit file **franky.c08.com.conf** sehingga menjadi
    ![8.1](assets/8a.png)
3. Aktifkan konfigurasi `a2ensite franky.c08.com.conf` 
4. Pindah ke direktori `/var/www` lalu download file dengan command `git config --global http.sslVerify false` lalu `git clone https://github.com/FeinardSlim/Praktikum-Modul-2-Jarkom.git` dan unzip file
    ![8.2](assets/8b.png)
5. Restart apache dengan `service apache2 restart`
6. Ketika mengakses **www.franky.c08.com** atau **www.franky.c08.com/index.php/home** maka akan mendapat tampilan seperti berikut
    ![8.3](assets/8c.png)

## 9. Mengubah url www.franky.c08.com/index.php/home dapat menjadi menjadi www.franky.c08.com/home
1. Jalankan perintah `a2enmod rewrite`
2. Melakukan konfigurasi pada server dengan menambahkan
    ```
    <Directory /var/www/semeruc02.pw>
        Options +FollowSymLinks -Multiviews
        AllowOverride All
    </Directory>
    ```
    pada **franky.c08.com.conf** seperti berikut
    ![9.1](assets/9a.png)
3. Pindah ke direktori `/var/www/franky.c08.com` dan buat file **.htaccess** lalu masukkan 
    ```
    RewriteEngine On
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule ^home$ index.php/home
    ```
    seperti berikut
    ![9.2](assets/9b.png)
4. Restart apache dengan `service apache2 restart`
5. Ketika mengakses **www.franky.c08.com/home** maka akan mendapat tampilan seperti berikut
    ![9.3](assets/9c.png)

## 10. Konfigurasi subdomain www.super.franky.c08.com Setelah itu, pada subdomain www.super.franky.c08.com, Luffy membutuhkan penyimpanan aset yang memiliki DocumentRoot pada /var/www/super.franky.c08.com.
1. Edit file **franky.c08.com.conf** sehingga menjadi
    ![10.1](assets/10a.png)
2. Restart apache dengan `service apache2 restart`
3. Ketika mengakses **www.super.franky.c08.com** maka akan mendapat tampilan seperti berikut
    ![10.2](assets/10b.png)

## 11. Akan tetapi, pada folder /public hanya dapat melakukan directory listing saja.
1. Konfigurasi file **franky.c08.com.conf** dengan menambahkan
    ```
    <Directory /var/www/super.franky.c08.com/public>
        Options +Indexes
    </Directory>
    ```
    sehingga menjadi
    ![11.1](assets/11a.png)
2. Ketika mengakses **www.super.franky.c08.com/public** maka akan mendapat tampilan seperti berikut
    ![11.2](assets/11b.png)

## 12. Mengganti error default dari apache menjadi error file 404.html pada folder/error.
1. Menambahkan konfigurasi berikut pada **franky.c08.com.conf**
    ```
    ErrorDocument 404 /error/404.html
    ```
    sehingga menjadi
    ![12.1](assets/12a.png)
2. Ketika mengakses url invalid seperti **www.super.franky.c08.com/halo** maka akan mendapat tampilan seperti berikut
    ![12.2](assets/12b.png)

## 13. Konfigurasi virtual host agar dapat mengakses file asset www.super.franky.c08.com/public/js menjadi www.super.franky.c08.com/js.
1. Jika mengakses **www.super.franky.c08.com/public/js** maka mendapatkan tampilan sebagai berikut
    ![13.1](assets/13a.png)
2. Edit file **franky.c08.com.conf** dengan menambahkan
    ```
    Alias "/js" "/var/www/super.franky.c08.com/public/js"
    ```
    sehingga menjadi
    ![13.2](assets/13b.png)
- Ketika mengakses **www.super.franky.c08.com/js** maka akan mendapatkan tampilan seperti berikut
    ![13.3](assets/13c.png)

## 14. Mengatur web www.general.mecha.franky.c08.com hanya bisa diakses dengan port 15000 dan port 15500
Langkah - langkah :
1. Membuat konfigurasi Web Server di /etc/apache2/sites-available/franky.c08.com.conf, tambahkan potongan kode berikut.
```
<VirtualHost *:15000 *:15500>
        ServerName general.mecha.franky.c08.com
        ServerAlias www.general.mecha.franky.c08.com
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/general.mecha.franky.c08.com
</VirtualHost>
```
2. Tambahkan port yang akan di listen pada /etc/apache2/ports.conf
```
Listen 15000
Listen 15500
```
3. Buat folder baru di /var/www dengan nama general.mecha.franky.c08.com
```
mkdir /var/www/general.mecha.franky.c08.com
```
4. Copy file - file lampiran github ke folder yang telah dibuat
```
cp -R /root/general.mecha.franky/* /var/www/general.mecha.franky.c08.com
```
5. Restart apache2
```
service apache2 restart
```
6. general.mecha.franky.c08.com dan Alias nya sudah bisa diakses melalui client menggunakan Lynx pada port 15000 atau 15500
## 15. Memberi autentikasi pada www.general.mecha.franky.c08.com dengan username luffy dan password onepiece
Langkah - langkah :
1. Tambahkan code berikut pada file /etc/apache2/sites-available/franky.c08.com.conf di bagian web server general.mecha.franky.c08.com
```
        <Directory /var/www/general.mecha.franky.c08.com>
        AuthType Basic
        AuthName "Ga Oleh Iki"
        AuthUserFile /etc/apache2/.htpasswd
        Require valid-user
        </Directory>
```
2. Buat user baru dengan command berikut sehingga memunculkan file .htpasswd pada direktori /etc/apache2
```
htpasswd -c /etc/apache2/.htpasswd luffy
```
3. Akan diminta memasukan password, masukkan 'onepiece'
4. Ketika web server general.mecha.franky.c08.com diakses, akan diminta authentikasi username dan password
## 16. Setiap kali mengakses IP Skypie akan dialihkan secara otomatis ke www.franky.c08.com
Langkah - langkah :
1. Tambahkan file .htaccess pada folder /var/www/html, lalu isikan berikut
```
RewriteEngine On
RewriteBase /
RewriteCond %{HTTP_HOST} ^10\.18\.2\.4$
RewriteRule ^(.*)$ http://www.franky.c08.com/$1 [L,R=301]
```
2. Ketika mengakses ip Skypie (10.18.2.4), akan langsung redirect ke http://www.franky.c08.com
## 17. Mengganti request gambar yang memiliki substring “franky” akan diarahkan menuju franky.png ketika mengakses www.super.franky.c08.com
1. Tambahkan file .htaccess pada folder /var/www/super.mecha.franky.c08.com, lalu isikan berikut
```
RewriteEngine On
RewriteRule ^(.*)franky(.*)$ http://www.super.franky.c08.com/public/images/franky.png [L,R=301]
```
2. Ketika mengakses image yang memiliki substring 'franky', akan langsung redirect ke http://www.super.franky.c08.com/public/images/franky.png
