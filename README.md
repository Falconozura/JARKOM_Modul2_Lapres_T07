# JARKOM_Modul2_T07
Lapres Praktikum Jarkom Modul 2<br />
<br />
![kelompok](https://img.shields.io/badge/Kelompok-T07-00a69a)<br />
<br />
Anggota:<br />
- ![fikri](https://img.shields.io/badge/Fikri%20Haykal-05311840000006-blueviolet)<br />
- ![syarif](https://img.shields.io/badge/Fancista%20Syarif%20H.-05311840000027-blueviolet)<br />

## DNS (Domain Name System)
### Soal 1
  Membuat alamat `http://semerut07.pw`.
  - DNS Server <b>MALANG</b>
  - Mengarah IP <b>PROBOLINGGO</b>
  #### Penyelesaian
  Menambahkan sebuah zona pada file `/etc/bind/named.conf.local` pada server <b>MALANG</b>.<br />
  ```
  zone "semerut7.pw" {
    type master;
    file "/etc/bind/semeru/semerut7.pw";
  };
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/1.png?raw=true)<br />
  Membuat sebuah file `/etc/bind/semeru/semerut7.pw`. Lalu dikonfigurasi seperti berikut:<br />
  ```
@           IN      SOA     semerut7.pw. root.semerut7.pw. (
                            2020111001  ; Serial
                            604800      ; Refresh
                            86400       ; Retry
                            2419200     ; Expire
                            604800 )    ; Negative Cache TTL
;
@           IN      NS      semerut7.pw.
@           IN      A       10.151.83.140
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/2.png?raw=true)<br />
### Soal 2
  Membuat domain alias `http://www.semerut7.pw` pada domain `http://semerut07.pw`.
  #### Penyelesaian
  Mengkonfigurasi file `/etc/bind/semeru/semerut7.pw` dengan menambahkan record <b>CNAME</b> seperti berikut:<br />
  ```
@           IN      SOA     semerut7.pw. root.semerut7.pw. (
                            2020111001  ; Serial
                            604800      ; Refresh
                            86400       ; Retry
                            2419200     ; Expire
                            604800 )    ; Negative Cache TTL
;
@           IN      NS      semerut7.pw.
@           IN      A       10.151.83.140
www         IN      CNAME   semerut7.pw.
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/2.png?raw=true)<br />
### Soal 3
  Membuat subdomain `http://penanjakan.semerut7.pw`.
  #### Penyelesaian
  Mengkonfigurasi file `/etc/bind/semeru/semerut7.pw` dengan menambahkan record <b>A</b> seperti berikut:<br />
  ```
@           IN      SOA     semerut7.pw. root.semerut7.pw. (
                            2020111001  ; Serial
                            604800      ; Refresh
                            86400       ; Retry
                            2419200     ; Expire
                            604800 )    ; Negative Cache TTL
;
@           IN      NS      semerut7.pw.
@           IN      A       10.151.83.140
www         IN      CNAME   semerut7.pw.
penanjakan  IN      A       10.151.93.140
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/2.png?raw=true)<br />
### Soal 4
  Membuat reverse domain `http://semerut7.pw`.
  - DNS Server <b>MALANG</b>
  - Mengarah IP <b>PROBOLINGGO</b>
  #### Penyelesaian
  Menambahkan sebuah zona pada file `/etc/bind/named.conf.local` pada server <b>MALANG</b>.<br />
  ```
zone "83.151.10.in-addr.arpa" {
    type master;
    file "/etc/bind/semeru/83.151.10.in-addr.arpa";
};
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/1.png?raw=true)<br />
  Membuat sebuah file `/etc/bind/semeru/83.151.10.in-addr.arpa`. Lalu dikonfigurasi seperti berikut:<br />
  ```
@       IN      SOA     semerut7.pw. root.semerut7.pw. (
                        2020111001  ; Serial
                        604800      ; Refresh
                        86400       ; Retry
                        2419200     ; Expire
                        604800 )    ; Negative Cache TTL
;
83.151.10.in-addr.arpa.       IN      NS      semerut7.pw.
140                           IN      PTR     semerut7.pw.
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/3.png?raw=true)<br />
### Soal 5
  Membuat DNS Slave pada <b>MOJOKERTO</b>.
  #### Penyelesaian
  Mengkonfigurasi zona `semerut7.pw` `/etc/bind/named.conf.local` pada server <b>MALANG</b> seperti berikut ini:<br />
  ```
  zone "semerut7.pw" {
      type master;
      also-notify { 10.151.83.139; };
      allow-transfer { 10.151.83.139; };
      file "/etc/bind/semeru/semerut7.pw";
  };
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/1.png?raw=true)<br />
  Menambahkan sebuah zona pada file `/etc/bind/named.conf.local` pada server <b>MOJOKERTO</b> seperti berikut.<br />
  ```
  zone "semerut7.pw" {
      type slave;
      masters { 10.151.83.138; };
      file "/var/lib/bind/semerut7.pw";
  }
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/4.png?raw=true)<br />
### Soal 6
  Membuat subdomain `http://penanjakan.semerut7.pw`.
  - Didelegasikan pada server <b>MOJOKERTO</b>
  - Mengarah IP <b>PROBOLINGGO</b>
  #### Penyelesaian
  Mengkonfigurasi file `/etc/bind/semeru/semerut7.pw` dengan menambahkan record <b>A</b> dan <b>NS</b> seperti berikut:<br />
  ```
@           IN      SOA     semerut7.pw. root.semerut7.pw. (
                            2020111001  ; Serial
                            604800      ; Refresh
                            86400       ; Retry
                            2419200     ; Expire
                            604800 )    ; Negative Cache TTL
;
@           IN      NS      semerut7.pw.
@           IN      A       10.151.83.140
www         IN      CNAME   semerut7.pw.
penanjakan  IN      A       10.151.83.140
ns1         IN      A       10.151.83.139
gunung      IN      NS      ns1
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/2.png?raw=true)<br />
  Mengkonfigurasi zona `semerut7.pw` `/etc/bind/named.conf.local` pada server <b>MALANG</b> seperti berikut ini:<br />
  ```
zone "semerut7.pw" {
    type master;
    also-notify { 10.151.83.139; };
    allow-transfer { 10.151.83.139; };
    file "/etc/bind/semeru/semerut7.pw";
};
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/1.png?raw=true)<br />
  Menonaktifkan `dnssec-validation auto;` serta menambahkan baris `allow-query{any;};` pada file `/etc/bind/named.conf.options` pada server <b>MALANG</b> dan <b>MOJOKERTO</b>
  ```
  //dnssec-validation auto;
  allow-query{any;};
  
  auth-nxdomain no;   #conform to RFC1035
  listen-on-v6 { any; };
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/5.png?raw=true)<br />
  Menambahkan sebuah zona pada file `/etc/bind/named.conf.local` pada server <b>MOJOKERTO</b>.<br />
  ```
zone "gunung.semerut7.pw"{
    type master;
    file "/etc/bind/delegasi/gunung.semerut7.pw";
    allow-transfer { any; };
}
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/4.png?raw=true)<br />
  Mengkonfigurasi file `/etc/bind/delegasi/gunung.semerut7.pw` seperti berikut:<br />
  ```
@           IN      SOA     gunung.semerut7.pw. root.gunung.semerut7.pw. (
                            2020111001  ; Serial
                            604800      ; Refresh
                            86400       ; Retry
                            2419200     ; Expire
                            604800 )    ; Negative Cache TTL
;
@           IN      NS      gunung.semerut7.pw.
@           IN      A       10.151.83.140   ; IP MOJOKERTO
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/6.png?raw=true)<br />
### Soal 7
  Membuat subdomain `http://naik.gunung.semerut7.pw`.
  - Didelegasikan pada server <b>MOJOKERTO</b>
  - Mengarah IP <b>PROBOLINGGO</b>
  #### Penyelesaian
  Mengkonfigurasi file `/etc/bind/delegasi/gunung.semerut7.pw` dengan menambahkan record <b>A</b> seperti berikut:<br />
  ```
@           IN      SOA     gunung.semerut7.pw. root.gunung.semerut7.pw. (
                            2020111001  ; Serial
                            604800      ; Refresh
                            86400       ; Retry
                            2419200     ; Expire
                            604800 )    ; Negative Cache TTL
;
@           IN      NS      gunung.semerut7.pw.
@           IN      A       10.151.83.140   ; IP MOJOKERTO
naik        IN      A       10.151.83.140   ; IP MOJOKERTO
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/6.png?raw=true)<br />

## Web Server
### Soal 8
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
