# JARKOM_Modul2_T07
Lapres Praktikum Jarkom Modul 2<br />
<br />
![kelompok](https://img.shields.io/badge/Kelompok-T07-00a69a)<br />
<br />
Anggota:<br />
- ![fikri](https://img.shields.io/badge/Fikri%20Haykal-05311840000006-blueviolet)<br />
- ![syarif](https://img.shields.io/badge/Fancista%20Syarif%20H.-05311840000027-blueviolet)<br />

## IP Address
```
NID TUNTAP
10.151.74.68

NID DMZ
10.151.83.136

IP_eth0_SURABAYA    = 10.151.74.70
IP_tuntap           = 10.151.74.69
IP_eth1_SURABAYA    = 10.151.83.137
IP_MALANG           = 10.151.83.138
IP_MOJOKERTO        = 10.151.83.139
IP_PROBOLINGGO      = 10.151.83.140
```

## Topologi
```
# Switch
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.74.69 eth1=daemon,,,switch2 eth2=daemon,,,switch1 mem=96M &

# Server
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch2 mem=128M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch2 mem=128M &
xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch2 mem=128M &

# Klien
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch1 mem=96M &
xterm -T GRESIK -e linux ubd0=GRESIK,jarkom umid=GRESIK eth0=daemon,,,switch1 mem=96M &
```

## UML Configuration
### Surabaya
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.74.70
netmask 255.255.255.252
gateway 10.151.74.69

auto eth1
iface eth1 inet static
address 10.151.83.137
netmask 255.255.255.248

auto eth2
iface eth2 inet static
address 192.168.0.1
netmask 255.255.255.0
```

### Malang
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.83.138
netmask 255.255.255.248
gateway 10.151.83.137
```

### Mojokerto
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.83.139
netmask 255.255.255.248
gateway 10.151.83.137
```

### Probolinggo
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.83.140
netmask 255.255.255.248
gateway 10.151.83.137
```

### Sidoarjo
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.2
netmask 255.255.255.0
gateway 192.168.0.1
```

### Gresik
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.3
netmask 255.255.255.0
gateway 192.168.0.1
```

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
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/1.png?raw=true)<br /><br />
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
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/2.png?raw=true)<br /><br />
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
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/2.png?raw=true)<br /><br />
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
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/2.png?raw=true)<br /><br />
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
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/1.png?raw=true)<br /><br />
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
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/3.png?raw=true)<br /><br />
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
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/1.png?raw=true)<br /><br />
  Menambahkan sebuah zona pada file `/etc/bind/named.conf.local` pada server <b>MOJOKERTO</b> seperti berikut.<br />
  ```
  zone "semerut7.pw" {
      type slave;
      masters { 10.151.83.138; };
      file "/var/lib/bind/semerut7.pw";
  }
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/4.png?raw=true)<br /><br />
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
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/2.png?raw=true)<br /><br />
  Mengkonfigurasi zona `semerut7.pw` `/etc/bind/named.conf.local` pada server <b>MALANG</b> seperti berikut ini:<br />
  ```
zone "semerut7.pw" {
    type master;
    also-notify { 10.151.83.139; };
    allow-transfer { 10.151.83.139; };
    file "/etc/bind/semeru/semerut7.pw";
};
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/1.png?raw=true)<br /><br />
  Menonaktifkan `dnssec-validation auto;` serta menambahkan baris `allow-query{any;};` pada file `/etc/bind/named.conf.options` pada server <b>MALANG</b> dan <b>MOJOKERTO</b>
  ```
  //dnssec-validation auto;
  allow-query{any;};
  
  auth-nxdomain no;   #conform to RFC1035
  listen-on-v6 { any; };
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/5.png?raw=true)<br /><br />
  Menambahkan sebuah zona pada file `/etc/bind/named.conf.local` pada server <b>MOJOKERTO</b>.<br />
  ```
zone "gunung.semerut7.pw"{
    type master;
    file "/etc/bind/delegasi/gunung.semerut7.pw";
    allow-transfer { any; };
}
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/4.png?raw=true)<br /><br />
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
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/6.png?raw=true)<br /><br />
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
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/6.png?raw=true)<br /><br />

## Web Server
### Soal 8
  Mengatur web server `http://semerut7.pw` pada <b>PROBOLINGGO</b>
  #### Penyelesaian
  Membuat file di `/etc/apache2/sites-available/semerut7.pw` lalu disetting seperti berikut :<br />
  ```
  ServerName semerut7.pw
  DocumentRoot /var/www/semerut7.pw
  ...
  <Directory /var/www/semerut7.pw>
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/7.png?raw=true)<br /><br />
  Mendownload file pendukung untuk dijadikan direktori di `/var/www/semerut7.pw/`.
  ```
  wget 10.151.36.202/semeru.pw.zip
  ...
  unzip semeru.pw.zip
  ...
  mv semeru.pw semerut7.pw
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/19.png?raw=true)<br /><br />
### Soal 9
  Menggunakan modul rewrite agar `http://semerut7.pw/home` bisa menampilkan isi dari `http://semerut7.pw/index.php/home`
  #### Penyelesaian
  Mengaktifkan <b>Override</b> di file `/etc/apache2/sites-available/semerut7.pw` seperti berikut :<br />
  ```
  AllowOverride All
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/7.png?raw=true)<br /><br />
  Membuat file `.htaccess` di `/var/www/semerut7.pw/` dan dibuat seperti berikut:<br />
  ```
  RewriteEngine on
  RewriteRule ^home$ index.php/home
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/20.png?raw=true)<br /><br />
### Soal 10
  Mengatur web server untuk subdomain `http://semerut7.pw` pada <b>PROBOLINGGO</b>
  #### Penyelesaian
  Membuat file di `/etc/apache2/sites-available/penanjakan.semerut7.pw` lalu disetting seperti berikut :<br />
  ```
  ServerName penanjakan.semerut7.pw
  DocumentRoot /var/www/penanjakan.semerut7.pw
  ...
  <Directory /var/www/penanjakan.semerut7.pw>
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/9.png?raw=true)<br /><br />
  Mendownload file pendukung untuk dijadikan direktori di `/var/www/penanjakan.semerut7.pw/`.
  ```
  wget 10.151.36.202/penanjakan.semeru.pw.zip
  ...
  unzip penanjakan.semeru.pw.zip
  ...
  mv semeru penanjakan.semerut7.pw
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/21.png?raw=true)<br /><br />
### Soal 11
  Mengatur <b>directory listing</b> pada `http://penanjakan.semerut7.pw`
  #### Penyelesaian
  Mengatur file di `/etc/apache2/sites-available/penanjakan.semerut7.pw` seperti berikut :<br />
  ```
  <Directory ...>
      Options -Indexes
  </Directory>
  ```
  NB : untuk direktori yang akan dinonaktfikan.<br />
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/10.png?raw=true)<br /><br />
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/22.png?raw=true)<br /><br />
### Soal 12
  Mengatur halaman 404 pada `http://penanjakan.semerut7.pw`
  #### Penyelesaian
  Mengatur file di `/etc/apache2/sites-available/penanjakan.semerut7.pw` seperti berikut :<br />
  ```
  ErrorDocument 404 /errors/404.html
  ```
  NB : Karena file 404.html sudah disediakan, kita hanya perlu mengarahkan.<br />
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/11.png?raw=true)<br /><br />
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/23.png?raw=true)<br /><br />
### Soal 13
  Mengatur <b>directory alias</b> `http://penanjakan.semerut7.pw/public/javascripts` menjadi `http://penanjakan.semerut7.pw/js`
  #### Penyelesaian
  Mengatur file di `/etc/apache2/sites-available/penanjakan.semerut7.pw` seperti berikut :<br />
  ```
  Alias "/js" "/var/www/penanjakan.semerut7.pw/public/javascripts"
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/12.png?raw=true)<br /><br />
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/24.png?raw=true)<br /><br />
### Soal 14
  Membuat subdomain `http://naik.gunung.semerut7.pw` pada port <b>8888</b><br />naik.gunung.
  #### Penyelesaian
  Membuat file `/etc/apache2/sites-available/naik.gunung.semerut7.pw`.<br />
  ```
  <VirtualHost *:8888>
  
  ServerName naik.gunung.semerut7.pw:8888
  DocumentRoot /var/www/naik.gunung.semerut7.pw
  ...
  <Directory /var/www/naik.gunung.semerut7.pw>
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/13.png?raw=true)<br /><br />
  Menambahkan <b>Listen 8888</b> pada `/etc/apache2/ports.conf`.<br />
  ```
  Listen 8888
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/14.png?raw=true)<br /><br />
  Mendownload file pendukung untuk dijadikan direktori di `/var/www/semerut7.pw/`.
  ```
  wget 10.151.36.202/naik.gunung.semeru.pw.zip
  ...
  unzip naik.gunung.semeru.pw.zip
  ...
  mv naik.gunung.semeru.pw naik.gunung.semerut7.pw
  ```
### Soal 15
  Membuat AuthBasic pada `http://naik.gunung.semerut7.pw` dengan user <b>semeru</b> dan password <b>kuynaikgunung</b><br />
  #### Penyelesaian
  Membuat <b>htpasswd</b> sesuai username dan password yang diminta.<br />
  ```
  htpasswd -c /etc/apache2/.htpasswd semeru
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/15.png?raw=true)<br /><br />
  Mengatur <b>Override</b> dan <b>Auth</b> pada file `/etc/apache2/sites-available/naik.gunung.semerut7.pw`.<br />
  ```
  AllowOverride All
  ...
  AuthType Basic
  AuthName "Login dulu cuy!"
  AuthUserFile /etc/apache2/.htpasswd
  Require valid-user
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/16.png?raw=true)<br /><br />
### Soal 16
  Mengarahkan alamat IP ke domain utama `http://semerut7.pw`
  #### Penyelesaian
  Menambahkan <b>Apache Redirect</b> pada file `/etc/apache2/sites-available/default`.<br />
  ```
  Redirect 301 / http://semerut7.pw
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/17.png?raw=true)<br /><br />
  Mengatur <b>Override</b> pada file `/etc/apache2/sites-available/naik.gunung.semerut7.pw`.<br />
  ```
  AllowOverride All
  ```
### Soal 17
  Mengarahkan URL yang mempunyai substring <b>semeru</b> ke alamat `http://penanjakan.semerut7.pw/public/images/semeru.jpg`
  #### Penyelesaian
  Mengatur <b>Override</b> pada file `/etc/apache2/sites-available/naik.gunung.semerut7.pw`.<br />
  ```
  AllowOverride All
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/18.png?raw=true)<br /><br />
  Membuat file <b>.htaccess</b> pada direktori `/var/www/penanjakan.semerut7.pw`.<br />
  ```
  RewriteEngine on
  RewriteRule ^(.*)semeru(.*)$ public/images/semeru.jpg
  ```
  ![img](https://github.com/Falconozura/JARKOM_Modul2_Lapres_T07/blob/main/screenshots/27.png?raw=true)<br /><br />
