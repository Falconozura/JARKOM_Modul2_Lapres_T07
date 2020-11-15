# JARKOM_Modul2_T07
Lapres Praktikum Jarkom Modul 2<br />
<br />
![kelompok](https://img.shields.io/badge/Kelompok-T07-00a69a)<br />
<br />
Anggota:<br />
- ![fikri](https://img.shields.io/badge/Fikri%20Haykal-05311840000006-blueviolet)<br />
- ![syarif](https://img.shields.io/badge/Fancista%20Syarif%20H.-05311840000027-blueviolet)<br />

## DNS
### Soal 1
  Membuat alamat `http://semerut07.pw`.
  - DNS Server <b>MALANG</b>
  - Mengarah IP <b>PROBOLINGGO</b>
  #### Penyelesaian
  Menambahkan sebuah zona pada file `/etc/bind/named.conf.local` pada server <b>MALANG</b>.<br />
  Membuat sebuah file `/etc/bind/semeru/semerut7.pw`. Lalu dikonfigurasi seperti berikut:<br />
### Soal 2
  Membuat domain alias `http://www.semerut7.pw` pada domain `http://semerut07.pw`.
  #### Penyelesaian
  Mengkonfigurasi file `/etc/bind/semeru/semerut7.pw` dengan menambahkan record <b>CNAME</b> seperti berikut:<br />
### Soal 3
  Membuat subdomain `http://penanjakan.semerut7.pw`.
  #### Penyelesaian
  Mengkonfigurasi file `/etc/bind/semeru/semerut7.pw` dengan menambahkan record <b>A</b> seperti berikut:<br />
### Soal 4
  Membuat reverse domain `http://semerut7.pw`.
  - DNS Server <b>MALANG</b>
  - Mengarah IP <b>PROBOLINGGO</b>
  #### Penyelesaian
  Menambahkan sebuah zona pada file `/etc/bind/named.conf.local` pada server <b>MALANG</b>.<br />
  Membuat sebuah file `/etc/bind/semeru/83.151.10.in-addr.arpa`. Lalu dikonfigurasi seperti berikut:<br />
### Soal 5
  Membuat DNS Slave pada <b>MOJOKERTO</b>.
  #### Penyelesaian
  Mengkonfigurasi zona `semerut7.pw` `/etc/bind/named.conf.local` pada server <b>MALANG</b> seperti berikut ini:<br />
  Menambahkan sebuah zona pada file `/etc/bind/named.conf.local` pada server <b>MOJOKERTO</b> seperti berikut.<br />
### Soal 6
### Soal 7
### Soal 8

## Web Server
### Soal 9
### Soal 10
### Soal 11
### Soal 12
### Soal 13
### Soal 14
### Soal 15
### Soal 16
### Soal 17
<ol>
  <li>Membuat alamat http://semerut07.pw </li>
  <li>Membuat alias http://www.semerut07.pw </li>
  <li>Membuat subdomain http://penanjakan.semerut07.pw </li>
  <li>Membuat reverse domain utama</li>
  <li>Membuat DNS slave</li>
  <li>Membuat domain http://gunung.semerut07.pw </li>
  <li>Menambahkan subdomain http://naik.gunung.semerut07.pw </li>
  <li>Mengatur web server</li>
  <li>Mengaktifkan mod rewrite</li>
  <li>Membuat web http://penanjakan.semerut07.pw </li>
  <li>Pada folder /public dibolehkan directory listing namun untuk folder yang berada di dalamnya tidak dibolehkan</li>
  <li>Membuat error page 404</li>
  <li>Membuat mod alias dari /javascript menjadi /js </li>
  <li>Membuat web http://naik.gunung.semerut04.pw </li>
  <li>Membuat password</li>
  <li>Melakukan redirect dari IP Probolinggo ke http://semerut07.pw </li>
  <li>Mengarahkan semua request gambar yang memiliki substring “semeru” pada /var/www/penanjakan.semeruto4.pw/public/images menuju semeru.jpg.
    
</ol>

## Jawaban
<ol>
 <li>Blablabla</li>
 <li>Blablabla</li>
 <li>Blablabla</li>
 <li>Blablabla</li>
 <li>Blablabla</li>
 <li>Blablabla</li>
 <li>Blablabla</li>
 <li>Blablabla</li>
 <li>Blablabla</li>
 <li>Blablabla</li>
 <li>Blablabla</li>
 <li>Blablabla</li>
 <li>Blablabla</li>
 <li>Blablabla</li>
 <li>Blablabla</li>
 <li>Blablabla</li>
 <li>Blablabla</li>
  
</ol>
