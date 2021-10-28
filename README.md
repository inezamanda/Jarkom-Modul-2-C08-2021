# Jarkom-Modul-2-C08-2021

Berikut adalah laporan resmi Praktikum Jaringan Komputer Modul 2 tahun 2021

Anggota Kelompok C08 :

- 05111940000100 - Muhammad Raihan
- 05111940000208 - Inez Yulia Amanda
- 05111940000209 - Refaldyka Galuh Pratama

## 1. EniesLobby akan dijadikan sebagai DNS Master, Water7 akan dijadikan DNS Slave, dan Skypie akan digunakan sebagai Web Server. Terdapat 2 Client yaitu Loguetown, dan Alabasta. Semua node terhubung pada router Foosha, sehingga dapat mengakses internet

## 2. Buat website utama dengan mengakses franky.c08.com dengan alias www.franky.c08.com pada folder kaizoku

## 3. Buat subdomain super.franky.c08.com dengan alias www.super.franky.c08.com yang diatur DNS nya di EniesLobby dan mengarah ke Skypie

## 4. Buat juga reverse domain untuk domain utama

## 5. Buat Water7 sebagai DNS Slave untuk domain utama

## 6. Setelah itu terdapat subdomain mecha.franky.c08.com dengan alias www.mecha.franky.c08.com yang didelegasikan dari EniesLobby ke Water7 dengan IP menuju ke Skypie dalam folder sunnygo

## 7. Buatkan subdomain melalui Water7 dengan nama general.mecha.franky.c08.com dengan alias www.general.mecha.franky.c08.com yang mengarah ke Skypie

## 8. Konfigurasi Webserver dengan domain www.franky.c08.com dan DocumentRoot pada /var/www/franky.c08.com.

## 9. Mengubah url www.franky.c08.com/index.php/home dapat menjadi menjadi www.franky.c08.com/home

## 10. Konfigurasi subdomain www.super.franky.c08.com Setelah itu, pada subdomain www.super.franky.c08.com, Luffy membutuhkan penyimpanan aset yang memiliki DocumentRoot pada /var/www/super.franky.c08.com.

## 11. Akan tetapi, pada folder /public hanya dapat melakukan directory listing saja.

## 12. Mengganti error default dari apache menjadi error file 404.html pada folder/error.

## 13. Konfigurasi virtual host agar dapat mengakses file asset www.super.franky.c08.com/public/js menjadi www.super.franky.c08.com/js.
 
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
