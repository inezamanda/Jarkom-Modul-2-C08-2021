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

## 15. Memberi autentikasi pada www.general.mecha.franky.c08.com dengan username luffy dan password onepiece

## 16. Setiap kali mengakses IP Skypie akan dialihkan secara otomatis ke www.franky.c08.com

## 17. Mengganti request gambar yang memiliki substring “franky” akan diarahkan menuju franky.png ketika mengakses www.super.franky.c08.com
