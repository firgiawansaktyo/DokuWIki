<h1 align="center"><img src="https://tr4.cbsistatic.com/hub/i/r/2013/10/04/f874e321-e469-4527-be52-9a568fa20d8d/resize/770x/af17703c07c5ff25c9f4c64b36aba944/dokuwiki.logo.jpg"></h1>

[Sekilas Tentang](#sekilas-tentang) | [Instalasi](#instalasi) | [Konfigurasi Umum](#konfigurasi-umum)
:---:|:---:|:---:|:---:|:---:|:---:|:---:



# Sekilas Tentang Dokuwiki
[`^ Back to Top ^`](#)

**Dokuwiki** adalah software wiki Open Source yang tidak memerlukan database. Syntax yang dimiliki Dokuwiki rapi dan mudah dibaca. Perawatan, backup, dan integrasi yang mudah membuat Dokuwiki disukai oleh administrator. Dokuwiki memiliki Built in access controls dan authentication connectors.

# Instalasi
[`^ Back to Top  ^`](#)

#### Komponen yang Dibutuhkan :
- Webserver yang mendukung PHP seperti apache
- PHP versi 5.6 ke atas
- Postfix
- PuTTY (optional)
- Browser internet

#### Proses Instalasi :
1. Install SSH ke dalam server di *Virtual Machine*.
    ```
    $ sudo apt update
    $ sudo apt install ssh
    ```

2. Akses VM secara *remote* dengan cara buka terminal di *host* untuk login *remote* ke port 2222.
	```
    ssh <Username>@localhost -p 2222
	```
    
3. Pastikan seluruh paket sistem kita *up-to-date*, dan install seluruh kebutuhan sistem seperti `Apache` dan `PHP`
    ```
   $ sudo apt-get update && sudo apt-get upgrade
   $ sudo apt-get install apache2 libapache2-mod-php
   $ sudo apt-get install php7.0
   $ sudo apt-get install php-mbstring
   $ sudo apt-get install php7.0-xml
	```

4. Aktifkan Apache Rewrite module
 	```
    $ sudo a2enmod rewrite
    ```

5. Setelah semua kebutuhan selesai kita harus *men-restart* VM yang sebelumnya telah dibuat.
	```
    $ sudo service apache2 restart
    ```
    
6. Unduh dan ekstrak versi terbaru dari **Dokuwiki**
	```
    $ cd /var/www
    $ sudo wget https://download.dokuwiki.org/src/dokuwiki/dokuwiki-stable.tgz
    $ sudo tar xvf dokuwiki-stable.tgz
    $ sudo mv dokuwiki-*/ dokuwiki
    ```

7. Ubah otorisasi kepemilikan ke user www-data (webserver)
    ```
    $ sudo chown -R www-data:www-data /var/www/html/dokuwiki
    ```

8. Ubah dokumen root di apache supaya menunjuk ke /var/www/html/dokuwiki
    ```
    $ sudo nano /etc/apache2/sites-enabled/000*.conf
    ```
    Ubah DocumentRoot dari `/var/www/html` menjadi `/var/www/html/dokuwiki`
    
    a. Ubah dokumen di /etc/apache2/sites-available/000*.conf dari `/var/www/html` menjadi `/var/www/html/dokuwiki`
    
    b. Aktifkan project baru dengan meletakkannya di /etc/apache2/sites-enabled dengan:
    ```
    $ sudo a2ensite apache2-dokuwiki
    ```
    
    c. Reload apache2 service
    `sudo service apache2 reload`

9.	Ubah settting AllowOverride pada apache2
    ```
    $ sudo nano /etc/apache2/apache2.conf
    ```
    Pada bagian /var/www, ubah:
    `AllowOverride None` menjadi `AllowOverride All`

10. Restart apache2 service
 
    ```
    $ sudo service apache2 restart
    ```

11. Kunjungi `http://<host>:<port>/dokuwiki/install.php` untuk meneruskan instalasi.
<img src="https://imh01-inmotionhosting1.netdna-ssl.com/support/images/stories/edu/dokuwiki/101/install-dokuwiki-manually/install-dokuwiki-manually-2.gif">

12. Install `postfix` agar dapat mengirim email ke pendaftar dengan:
    ```
    $ sudo apt-get install postfix
	```
    
# Konfigurasi Umum
[`^ Back to Top ^`](#)

Semua file konfigurasi dapat ditemukan di folder `./conf` atau `/etc/dokuwiki`.
File utama biasanya dapat ditemukan di Dokuwiki, dimana lokal file harus dibuat oleh wiki admin atau super admin. Konfigurasi utama seperti:
- automatic abbreviation hints
- automatic text replacements
- interwiki shortcut links
- mime type settings for uploads
- image replacements

# Maintenance Dokuwiki
[`^ Back to Top ^`](#)

Untuk maintenance, disarankan untuk menggunakan Bash (unix shell) untuk membersihkan script secara otomatis, seperti menghapus revisi yang dulu, direktori yang kosong, dan menghapus cache. Untuk menjalankan secara otomatis, gunakan cronjob. Contoh berikut digunakan untuk memanggil script setiap hari 7 menit setelah tengah malam:

	```
	$ 7 0 * * * root /full/path/to/cleanup.sh
	```


