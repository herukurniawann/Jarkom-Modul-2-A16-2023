# Jarkom-Modul-2-A16-2023
## Praktikum Modul 2 Jaringan Komputer

**Kelompok A16 :**

| Nama | NRP |
| ----------- | ----------- |
| Clarissa Luna Maheswari | 5025211033 |
| Heru Dwi Kurniawan | 5025211055 

## Soal 1
Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian sebagai berikut. Folder topologi dapat diakses pada drive berikut 

**Penyelasaian Soal**
Untuk membuat sebuah topologi yang diminta di soal, lakukan set up di GNS3 sampai muncul tampilan berikut

![image](https://github.com/herukurniawann/Jarkom-Modul-2-A16-2023/assets/93961310/a4053584-2009-4843-8184-35f95b4d0eaf)

Kemudian salin alamat IP yang tertera yaitu 192.168.56.101 di browser google 
kemudian akan terbuka tampilan dari GNS3 nya seperti gambar berikut : 

![image](https://github.com/herukurniawann/Jarkom-Modul-2-A16-2023/assets/93961310/19b6e342-9606-4b09-b584-4c5bfca80e06)

Kemudian setelah terbuka tampilan GNS3 Seperti gambar di atas, selanjutnya membuat topologi dan sambungkan setiap masing-masing node dengan gambar yang di minta di soal. 
Pada praktikkum kali ini kelompok saya mendapat topologi 1.

![image](https://github.com/herukurniawann/Jarkom-Modul-2-A16-2023/assets/93961310/ddefe1b0-a391-456f-954d-60c6531e6d72)

Gunakan Fitur Changehostname untuk merubah setiap masing-masing node sesuai topologi gambar pada soal yang diminta, ketika sudah berhasil di ubah selanjutnya klik Applay.

![image](https://github.com/herukurniawann/Jarkom-Modul-2-A16-2023/assets/93961310/ae20cba3-58a6-4df7-a91d-b7e92a168d58)

Kemudian untuk merubah Symbol pada setiap masing-masing node, gunakan fitur Change Symbol untuk merubah symbol dari setiap node sesuai pada topologi gambar soal yang diminta. Setelah berhasil selanjutnya klik Applay

![image](https://github.com/herukurniawann/Jarkom-Modul-2-A16-2023/assets/93961310/1503dae7-dedf-4177-8104-c9397c8670e3)

Gambar sudah sesuai dengan topologi soal yang diminta, Langkah selanjutnya yaitu mengkonfigurasi masing-masing IP Prefix node dengan IP Prefix yang sudah disediakan Asisten. Untuk IP Prefix kelompok saya adalah **10.7.**

![image](https://github.com/herukurniawann/Jarkom-Modul-2-A16-2023/assets/93961310/48b1abd8-9e15-4150-874b-b76af5b8d80b)

Set up konfigurasi setiap masing - masing node 

**Puntadewa**

DHCP config for eth0
```bash
auto eth0
iface eth0 inet dhcp
```

Konfigurasi eth1
```bash
auto eth1
iface eth1 inet static
    address 10.7.1.1
    netmask 255.255.255.0
```

Konfigurasi eth2
```bash
auto eth2
iface eth2 inet static
    address 10.7.2.1
    netmask 255.255.255.0
```

Konfigurasi eth 3
```bash
auto eth3
iface eth3 inet static
    address 10.7.3.1
    netmask 255.255.255.0
```

Jika berhasil di set up, maka cek konfigurasi jaringan dengan menggunakan **ifconfig** di node puntadewa. 

![image](https://github.com/lunielism/yes/assets/93961310/6016d9d2-69ae-4f1f-a250-138a539cab19)

Jika sudah di cek dan sudah berhasil. maka dilanjutkan untuk set up node lain

**eth1**
Konfigurasi Yudhistira
```bash
auto eth0
iface eth0 inet static
     	address 10.7.1.2
     	netmask 255.255.255.0
     	gateway 10.7.1.1
```

Konfigurasi Nakula
```bash
auto eth0
iface eth0 inet static
     	address 10.7.1.3
     	netmask 255.255.255.0
     	gateway 10.7.1.1
```

eth2
Konfigurasi Werkudara
```bash
auto eth0
iface eth0 inet static
     	address 10.7.2.2
     	netmask 255.255.255.0
     	gateway 10.7.2.1
```

Konfigurasi Sadewa
```bash
auto eth0
iface eth0 inet static
     	address 10.7.2.3
     	netmask 255.255.255.0
     	gateway 10.7.2.1
```

eth3
Konfigurasi Prabukusuma
```bash
auto eth0
iface eth0 inet static
     	address 10.7.3.2
     	netmask 255.255.255.0
     	gateway 10.7.3.1
```

Konfigurasi Abimanyu
```bash
auto eth0
iface eth0 inet static
     	address 10.7.3.3
     	netmask 255.255.255.0
     	gateway 10.7.3.1
```

Konfigurasi Wisanggeni
```bash
auto eth0
iface eth0 inet static
     	address 10.7.3.4
     	netmask 255.255.255.0
     	gateway 10.7.3.1
```

Konfigurasi Arjuna
```bash
auto eth0
iface eth0 inet static
     	address 10.7.3.5
     	netmask 255.255.255.0
     	gateway 10.7.3.1
```

Kemudian setelah mensetting semua node, langkah selanjutnya adalah mensetting iptable agar seluruh node dibawah router dapat terhubung dengan internet.

dengan menggunakan sebagai berikut

```bash
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.7.0.0/16
```

![image](https://github.com/lunielism/yes/assets/93961310/05b162e3-eb43-402a-8892-6f1b0f3b19ec)

## Soal 2
Buatlah website utama pada node arjuna dengan akses ke arjuna.yyy.com dengan alias www.arjuna.yyy.com dengan yyy merupakan kode kelompok.

**Penyelesaian Soal**
Dikarenakan DNS akan tidak tersedia setelah dihentikan, maka diperlukan penggunaan script.sh untuk memastikan proses berjalan dengan efisien dan tidak berulang. Untuk melakukannya, buka terminal dan ketikkan nano .bashrc. Selanjutnya, tuliskan kembali langkah-langkah sebelumnya di bawah ini.

**Node Yudhistira**
![image](https://github.com/lunielism/yes/assets/93961310/ad6851cf-879b-4264-8c86-1557a6f089e0)

```bash
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install bind9 -y
echo 'zone "arjuna.a16.com"{  
        type master;
        file "/etc/bind/arjuna/arjuna.a16.com";
};' > /etc/bind/named.conf.local
mkdir /etc/bind/arjuna
cp /etc/bind/db.local /etc/bind/arjuna/arjuna.a16.com
echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     arjuna.a16.com. root.arjuna.a16.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      arjuna.a16.com.
@       IN      A       10.7.3.5       ; IP Arjuna 
www     IN      CNAME   arjuna.a16.com.
@       IN      AAAA    ::1' > /etc/bind/arjuna/arjuna.a16.com
service bind9 restart
```

**Node Sadewa/Nakula**

![image](https://github.com/lunielism/yes/assets/93961310/4d57db4d-e681-4a83-91cc-5ee66a878faf)

```bash
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install dnsutils
echo nameserver 10.7.1.2 > /etc/resolv.conf
ping arjuna.a16.com
```
**Hasil**

![image](https://github.com/lunielism/yes/assets/93961310/f5db2d21-317a-4f64-ad52-e8ee36deffa1)

## Soal 3
Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke abimanyu.yyy.com dan alias www.abimanyu.yyy.com.

**Penyelesaian Soal**
Tindakan yang harus diambil adalah serupa dengan langkah kedua, namun kali ini ada modifikasi pada kode program. kemudian tuliskan kode program berikut di node **Yudhistira.**

**Node Yudhistira**

![image](https://github.com/lunielism/yes/assets/93961310/6afb234a-dfd1-463b-a703-2670c2861da8)

```bash
echo 'zone "abimanyu.a16.com"{  
        type master;
        file "/etc/bind/arjuna/abimanyu.a16.com";
};' >> /etc/bind/named.conf.local
cp /etc/bind/db.local /etc/bind/arjuna/abimanyu.a16.com
echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.a16.com. root.abimanyu.a16.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.a16.com.
@       IN      A       10.7.3.3       ; IP Abimanyu 
www     IN      CNAME   abimanyu.a16.com.
@       IN      AAAA    ::1' > /etc/bind/arjuna/abimanyu.a16.com
service bind9 restart
```

**Node Sadewa/Nakula**

![image](https://github.com/lunielism/yes/assets/93961310/5ba0178a-d447-451f-b93f-1e77c0200a04)

```bash
echo nameserver 10.7.1.2 > /etc/resolv.conf
host -t CNAME www.abimanyu.a16.com  
ping www.abimanyu.a16.com -c 5
```

**Hasil**

![image](https://github.com/lunielism/yes/assets/93961310/3a6120fb-0d4a-4c04-8e8f-77745217b072)

## Soal 4
Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.yyy.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.

**Penyelesaian Soal**
Yang diperlukan serupa dengan langkah ketiga, tetapi kali ini Anda perlu menambahkan subdomain dengan nama **"parikesit"** pada kode program. Silakan tuliskan kode program ini pada web console di node **Yudhistira.**

**Node Yudhistira**

![image](https://github.com/lunielism/yes/assets/93961310/7bd0c4f2-b69d-47f5-88e1-c6346da2be16)

```bash

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.a16.com. root.abimanyu.a16.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.a16.com.
@       IN      A       10.7.3.3       ; IP Abimanyu 
www     IN      CNAME   abimanyu.a16.com.
parikesit   IN  A   10.7.3.3   ; IP Abimanyu
@       IN      AAAA    ::1' > /etc/bind/jarkom/abimanyu.a16.com
service bind9 restart
```
**Node Nakula/Sadewa**

![image](https://github.com/herukurniawann/Jarkom-Modul-2-A16-2023/assets/93961310/c7f3994d-0f00-40c3-8adc-44c0dab81373)

```bash
ping parikesit.abimanyu.a16.com
```

**Hasil**

![image](https://github.com/lunielism/yes/assets/93961310/11a860f7-9ca9-429e-80eb-1df587d71a55)

## Soal 5
Buat juga reverse domain untuk domain utama. (Abimanyu saja yang direverse)

Tahapan berikutnya adalah mendokumentasikan kembali kode program yang mencakup penambahan domain terbalik di **Yudhistira**. Kode programnya memiliki format seperti berikut ini.

![image](https://github.com/lunielism/yes/assets/93961310/2c579255-3771-46f7-a8f0-c0a6f5821e10)


```bash
echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.a16.com. root.abimanyu.a16.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
3.7.10.in-addr.arpa.   IN      NS      abimanyu.a16.com.
3                       IN      PTR     abimanyu.a16.com. ' > /etc/bind/arjuna/$

echo '
zone "3.7.10.in-addr.arpa" {
        type master;
        file "/etc/bind/arjuna/3.7.10.in-addr.arpa";
```
**Node Nakula&Sadewa**
![image](https://github.com/lunielism/yes/assets/93961310/227f6dc3-948d-4ced-b076-18bed5e8fa74)

```bash
echo nameserver 10.7.1.2 > /etc/resolv.conf
host -t PTR 10.7.1.2
```

**Hasil** 
![image](https://github.com/lunielism/yes/assets/93961310/9fc7c0c5-50b5-4b48-8287-f30e7724bf14)


## Soal 6
Agar dapat tetap dihubungi ketika DNS Server Yudhistira bermasalah, buat juga Werkudara sebagai DNS Slave untuk domain utama.

Untuk mengerjakan DNS Slave, kita memerlukan beberapa konfigurasi pada DNS Master dan DNS Slave (Werkudara)

**Node Yudhistira**
![image](https://github.com/lunielism/yes/assets/93961310/a0aa9e1e-3277-4a90-b4f2-afc70f1b9bf0)

```bash
echo 'zone "arjuna.a16.com"{  
        type master;
        also-notify { 10.7.2.2; };
        allow-transfer { 10.7.2.2; };
        file "/etc/bind/arjuna/arjuna.a16.com";
};
zone "abimanyu.a16.com"{  
        type master;
        also-notify { 10.7.2.2; };
        allow-transfer { 10.7.2.2; };
        file "/etc/bind/arjuna/abimanyu.a16.com";
};

zone "3.7.10.in-addr.arpa" {
        type master;
        file "/etc/bind/arjuna/3.7.10.in-addr.arpa";
};' > /etc/bind/named.conf.local

service bind9 restart
```
**Node Werkudara**

![image](https://github.com/lunielism/yes/assets/93961310/98f2e477-02d6-4cb6-a5cd-60f0f465630c)

```bash
zone "arjuna.a16.com" {
    type slave;
    masters { 10.7.1.2; };
    file "/var/lib/bind/arjuna/a16.com";
};
zone "abimanyu.a16.com" {
    type slave;
    masters { 10.7.1.2; };
    file "/var/lib/bind/abimanyu/a16.com";
};
```

**Node Nakula**
![image](https://github.com/lunielism/yes/assets/93961310/474f1247-564f-4d79-a4b5-ca02e339f377)

```bash
nameserver 10.7.1.2
nameserver 10.7.2.2
```
Kemudian matikan bind server pada Yudhistira ```bash service bind9 stop``` dan aktifkan bind server pada Werkudara  ```bash service bind9 restart```, setelah itu lakukan ping di node nakula.

![image](https://github.com/lunielism/yes/assets/93961310/45532069-a5de-40ef-8505-fd6a664ea314)

![image](https://github.com/lunielism/yes/assets/93961310/48a563d2-75ec-4a73-a340-2f5ff347f5c1)

**Hasil**
![image](https://github.com/lunielism/yes/assets/93961310/7132f8fe-721a-4da1-a859-d6c9ec6fbaef)

## Soal 7
Seperti yang kita tahu karena banyak sekali informasi yang harus diterima, buatlah subdomain khusus untuk perang yaitu baratayuda.abimanyu.yyy.com dengan alias www.baratayuda.abimanyu.yyy.com yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda.

Untuk melakukan Delegasi subdomain, kita memerlukan beberapa configurasi pada DNS Master dan DNS Slave. Kita juga meemerlukan beberapa modifikasi pada /etc/bind/named.conf.options

**Yudhistira**

![image](https://github.com/lunielism/yes/assets/93961310/1eb18d40-f2ce-4973-bd2b-21d99b45f600)

```bash
echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.a16.com. root.abimanyu.a16.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@               IN      NS      abimanyu.a16.com.
@               IN      A       10.7.3.3       ; IP Abimanyu 
www             IN      CNAME   abimanyu.a16.com.
ns1             IN      A       10.7.2.2        ; IP Werkudara
baratayuda      IN      NS      ns1
parikesit       IN      A       10.7.3.3   ; IP Abimanyu
@               IN      AAAA    ::1' > /etc/bind/arjuna/abimanyu.a16.com
cp /root/named.conf.options /etc/bind/named.conf.options

service bind9 restart
```

**Node Werkudara**

![image](https://github.com/lunielism/yes/assets/93961310/3299610e-97fc-4c2a-822d-af5306ee8b6d)

```bash
 allow-query {any;};
        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
```

![image](https://github.com/lunielism/yes/assets/93961310/9faf2497-1167-42af-ba93-a0586a0240da)

```bash
zone "baratayuda.abimanyu.a16.com" {
        type master;
        file "/etc/bind/baratayuda/abimanyu.a16.com";
        allow-transfer { 10.7.1.2; };
};
```

```bash

![image](https://github.com/lunielism/yes/assets/93961310/39b1679a-6df1-4a1d-9c10-d91220c8ca48)

```bash
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     baratayuda.abimanyu.a16.com. root.baratayuda.abimanyu.a$
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      baratayuda.abimanyu.a16.com.
@       IN      A       10.7.3.3       ; IP Abimanyu
www     IN      CNAME   baratayuda.abimanyu.a16.com.
rjp     IN      A       10.7.3.3        ; IP Abimanyu
www.rjp IN      CNAME   rjp.baratayuda.abimanyu.a16.com.
@       IN      AAAA    ::1
```

**Hasil**

![image](https://github.com/lunielism/yes/assets/93961310/5b5ca465-2811-4970-858e-be24fe7511fa)


## Soal 8
Untuk informasi yang lebih spesifik mengenai Ranjapan Baratayuda, buatlah subdomain melalui Werkudara dengan akses rjp.baratayuda.abimanyu.yyy.com dengan alias www.rjp.baratayuda.abimanyu.yyy.com yang mengarah ke Abimanyu.

Karena kita sudah melakukan Delegasi subdomain, langkah selanjutnya adalah melakukan subdomain melalui Werkudara dengan perlu memerlukan beberapa konfigurasi pada DNS Master dan DNS Slave.

**Node Werkudara

![image](https://github.com/lunielism/yes/assets/93961310/ef99a618-04ec-4b02-b5db-c4888ebf65e6)

```bash

;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     baratayuda.abimanyu.a16.com. root.baratayuda.abimanyu.a$
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      baratayuda.abimanyu.a16.com.
@       IN      A       10.7.3.3       ; IP Abimanyu
www     IN      CNAME   baratayuda.abimanyu.a16.com.
rjp     IN      A       10.7.3.3        ; IP Abimanyu
www.rjp IN      CNAME   rjp.baratayuda.abimanyu.a16.com.
@       IN      AAAA    ::1
```

**Hasil**
![image](https://github.com/lunielism/yes/assets/93961310/77de6584-c2f9-4212-82ff-5a470cc9e6a7)


## Soal 9
Arjuna merupakan suatu Load Balancer Nginx dengan tiga worker (yang juga menggunakan nginx sebagai webserver) yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Lakukan deployment pada masing-masing worker.

Cara Pengerjaan:

1. Kami menjalankan script berikut untuk melakukan konfigurasi Load Balancer Nginx Arjuna:
```bash
#!/bin/bash

# Konfigurasi Nginx
echo 'upstream backend {
  server 10.7.3.2;
  server 10.7.3.3;
  server 10.7.3.4;
}

server {
  listen 80;
  server_name arjuna.a16.com www.arjuna.a16.com;

  location / {
    proxy_pass http://backend;
  }
}
' > /etc/nginx/sites-available/jarkom

# Membuat symlink untuk konfigurasi Nginx
ln -s /etc/nginx/sites-available/jarkom /etc/nginx/sites-enabled/jarkom

# Menghapus konfigurasi default Nginx
rm /etc/nginx/sites-enabled/default

# Merestart layanan Nginx
service nginx restart

echo 'Selesai mengonfigurasi Nginx untuk arjuna.a16.com.'
```
2. Setelah mengkonfigurasi Arjuna, langkah selanjutnya adalah melakukan deployment pada masing-masing worker.
Pada tiap worker yaitu Prabakusuma, Abimanyu, dan Wisanggeni dijalankan perintah shell sebagai berikut:
```bash
#!/bin/bash

# Nyalakan layanan PHP-FPM
service php7.0-fpm start

# Konfigurasi Nginx untuk website
echo 'server {
    listen 80;

    root /var/www/jarkom;
    index index.php index.html index.htm index.nginx-debian.html;

    server_name _;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}' > /etc/nginx/sites-available/jarkom

# Membuat symlink untuk konfigurasi Nginx
ln -s /etc/nginx/sites-available/jarkom /etc/nginx/sites-enabled/jarkom

# Hapus konfigurasi default Nginx
rm /etc/nginx/sites-enabled/default

# Restart layanan Nginx
service nginx restart

echo 'Selesai mengonfigurasi Nginx dan PHP-FPM.'
```

3. Untuk memastikan bahwa load balancer berfungsi dengan baik, kami melakukan beberapa test pada salah satu client yaitu Nakula:
```bash
lynx http://10.7.3.2
lynx http://10.7.3.3
lynx http://10.7.3.4
lynx http://10.7.3.5
lynx http://arjuna.a16.com
```

## Soal 10
Kemudian gunakan algoritma Round Robin untuk Load Balancer pada Arjuna. Gunakan server_name pada soal nomor 1. Untuk melakukan pengecekan akses alamat web tersebut kemudian pastikan worker yang digunakan untuk menangani permintaan akan berganti ganti secara acak. Untuk webserver di masing-masing worker wajib berjalan di port 8001-8003. Contoh
    - Prabakusuma:8001
    - Abimanyu:8002
    - Wisanggeni:8003

### Cara Pengerjaan
#### Langkah 1: Konfigurasi Arjuna

1. Pastikan konfigurasi Arjuna yang benar telah selesai. Kami menggunakan algoritma Round Robin untuk mendistribusikan lalu lintas web secara merata ke setiap worker yang tersedia.

```bash
#!/bin/bash

# Konfigurasi DNS Abimanyu
echo '
; BIND data file for local loopback interface
;
$TTL 604800
@   IN  SOA abimanyu.a16.com. root.abimanyu.a16.com. (
    2       ; Serial
    604800  ; Refresh
    86400   ; Retry
    2419200 ; Expire
    604800  ; Negative Cache TTL
)
@   IN  NS  abimanyu.a16.com.
@   IN  A   10.7.3.3
www IN  CNAME abimanyu.a16.com
parikesit IN A 10.7.3.3
ns1 IN A 10.7.2.2
baratayuda IN NS ns1
' > /etc/bind/jarkom/abimanyu.a16.com

# Restart Bind9
service bind9 restart

# Konfigurasi Apache Abimanyu
cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/abimanyu.a16.com.conf

rm /etc/apache2/sites-available/000-default.conf

echo -e '<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/abimanyu.a16

  ServerName abimanyu.a16.com
  ServerAlias www.abimanyu.a16.com

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/abimanyu.a16.com.conf

a2ensite abimanyu.a16.com.conf

# Restart Apache2
service apache2 restart

```
#### Langkah 2: Deployment
Setelah mengkonfigurasi Arjuna, langkah selanjutnya adalah melakukan deployment pada masing-masing worker. Pastikan setiap worker telah diatur dengan benar dan siap melayani lalu lintas web.
```bash
# Contoh konfigurasi web server untuk PrabuKusuma (port 8001)
server {
  listen 8001;

  root /var/www/jarkom;
  index index.php index.html index.htm index.nginx-debian.html;

  server_name _;

  location / {
    try_files $uri $uri/ /index.php?$query_string;
  }

  location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/run/php/php7.0-fpm.sock;
  }

  location ~ /\.ht {
    deny all;
  }
}

```

#### Langkah 3: Uji Load Balancer

Untuk memastikan bahwa load balancer berfungsi dengan baik, lakukan beberapa tes dari client (Sadewa / Nakula). Gunakan perintah berikut:

```bash
lynx http://10.7.3.2
lynx http://10.7.3.3
lynx http://10.7.3.4
lynx http://10.7.3.5
lynx http://arjuna.a16.com
```

## Soal 11
Selain menggunakan Nginx, lakukan konfigurasi Apache Web Server pada worker Abimanyu dengan web server www.abimanyu.yyy.com. Pertama dibutuhkan web server dengan DocumentRoot pada /var/www/abimanyu.yyy

#### Langkah 1: Konfigurasi DNS - Yudhistira

Langkah pertama yang kami lakukan adalah mengkonfigurasi DNS untuk mengarahkan domain abimanyu.a16.com ke alamat IP Abimanyu (10.7.3.3) supaya domain www.abimanyu.yyy.com dapat diakses dengan benar.

1. Jalankan script berikut di server Yudhistira:

```bash
#!/bin/bash

# Konfigurasi DNS Abimanyu
echo '
; BIND data file for local loopback interface
;
$TTL 604800
@   IN  SOA abimanyu.a16.com. root.abimanyu.a16.com. (
    2       ; Serial
    604800  ; Refresh
    86400   ; Retry
    2419200 ; Expire
    604800  ; Negative Cache TTL
)
@   IN  NS  abimanyu.a16.com.
@   IN  A   10.7.3.3
www IN  CNAME abimanyu.a16.com
parikesit IN A 10.7.3.3
ns1 IN A 10.7.2.2
baratayuda IN NS ns1
' > /etc/bind/jarkom/abimanyu.a16.com

# Restart Bind9
service bind9 restart

# Konfigurasi Apache Abimanyu
cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/abimanyu.a16.com.conf

rm /etc/apache2/sites-available/000-default.conf

echo -e '<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/abimanyu.a16

  ServerName abimanyu.a16.com
  ServerAlias www.abimanyu.a16.com

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/abimanyu.a16.com.conf

a2ensite abimanyu.a16.com.conf

# Restart Apache2
service apache2 restart
```
#### Langkah 2: Konfigurasi Apache - Abimanyu 
```bash
# Konfigurasi Apache untuk Abimanyu
cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/abimanyu.a16.com.conf
rm /etc/apache2/sites-available/000-default.conf

echo -e '<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/abimanyu.a16

  ServerName abimanyu.a16.com
  ServerAlias www.abimanyu.a16.com

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/abimanyu.a16.com.conf

a2ensite abimanyu.a16.com.conf
service apache2 restart

```
Script yang kami susun akan mengkonfigurasi Apache agar mampu melayani domain www.abimanyu.yyy.com dengan menggunakan alamat IP yang telah ditentuka
#### Langkah 3: Uji Situs Web
```bash
lynx abimanyu.a16.com
```

## Soal 12
Setelah itu ubahlah agar url www.abimanyu.yyy.com/index.php/home menjadi www.abimanyu.yyy.com/home.

#### Langkah 1: Konfigurasi Apache - Abimanyu

1. Jalankan script berikut di server Abimanyu untuk mengubah konfigurasi Apache:

   ```bash
   # Konfigurasi Apache untuk Abimanyu dengan URL yang diubah
   echo -e '<VirtualHost *:80>
     ServerAdmin webmaster@localhost
     DocumentRoot /var/www/abimanyu.a16
     ServerName abimanyu.a16.com
     ServerAlias www.abimanyu.a16.com

     <Directory /var/www/abimanyu.a16/index.php/home>
       Options +Indexes
     </Directory>

     Alias "/home" "/var/www/abimanyu.a16/index.php/home"

     ErrorLog ${APACHE_LOG_DIR}/error.log
     CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>' > /etc/apache2/sites-available/abimanyu.a16.com.conf

   service apache2 restart
   ```

#### Langkah 2: Uji Situs Web
   ```bash
lynx abimanyu.a16.com/home
curl abimanyu.a16.com/home
   ```

## Soal 13
Selain itu, pada subdomain www.parikesit.abimanyu.yyy.com, DocumentRoot disimpan pada /var/www/parikesit.abimanyu.yyy

#### Langkah 1: Konfigurasi Apache - Abimanyu

Jalankan script berikut di server Abimanyu untuk menambahkan konfigurasi subdomain:

   ```bash
   # Konfigurasi Apache untuk subdomain parikesit.abimanyu.yyy.com
   echo -e '<VirtualHost *:80>
     ServerAdmin webmaster@localhost
     DocumentRoot /var/www/parikesit.abimanyu.a16
     ServerName parikesit.abimanyu.a16.com
     ServerAlias www.parikesit.abimanyu.a16.com

     ErrorLog ${APACHE_LOG_DIR}/error.log
     CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.a16.com.conf

   a2ensite parikesit.abimanyu.a16.com.conf
   service apache2 restart
```

#### Langkah 2: Konfigurasi Apache - Abimanyu
Untuk mengjui subdomain, kami menggunakna perintah beriut di client nakula:
```bash
lynx parikesit.abimanyu.a16.com
lynx parikesit.abimanyu.a16.com
```
## Soal 14
Pada subdomain tersebut folder /public hanya dapat melakukan directory listing sedangkan pada folder /secret tidak dapat diakses (403 Forbidden).

### Cara Pengerjaan
#### Langkah 1: Konfigurasi Apache - Abimanyu

Jalankan script berikut di server Abimanyu:

```bash
# Konfigurasi Apache untuk Subdomain parikesit.abimanyu.yyy.com
echo -e '<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/parikesit.abimanyu.a16
  ServerName parikesit.abimanyu.a16.com
  ServerAlias www.parikesit.abimanyu.a16.com

  <Directory /var/www/parikesit.abimanyu.a16/public>
    Options +Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.a16/secret>
    Options -Indexes
  </Directory>

  Alias "/public" "/var/www/parikesit.abimanyu.a16/public"
  Alias "/secret" "/var/www/parikesit.abimanyu.a16/secret"

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.a16.com.conf

service apache2 restart
```
#### Langkah 2: Konfigurasi Apache - Abimanyu
Kami menguji konfigurasi dengan menggunakan perintah untuk folder public dan secret:
```bash
lynx parikesit.abimanyu.a16.com/public
lynx parikesit.abimanyu.a16.com/secret

```

## Soal 15
Buatlah kustomisasi halaman error pada folder /error untuk mengganti error kode pada Apache. Error kode yang perlu diganti adalah 404 Not Found dan 403 Forbidden.
### Cara Pengerjaan
#### Langkah 1: Konfigurasi Apache - Abimanyu
```bash
# Konfigurasi Apache untuk Kustomisasi Halaman Error
echo -e '<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/parikesit.abimanyu.a16
  ServerName parikesit.abimanyu.a16.com
  ServerAlias www.parikesit.abimanyu.a16.com

  <Directory /var/www/parikesit.abimanyu.a16/public>
    Options +Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.a16/secret>
    Options -Indexes
  </Directory>

  Alias "/public" "/var/www/parikesit.abimanyu.a16/public"
  Alias "/secret" "/var/www/parikesit.abimanyu.a16/secret"

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.a16.com.conf

service apache2 restart

```
#### Langkah 2: Uji Kustomisasi Halaman Error
Berikut kami gunakan untuk menguji kustomisasi halaman error dengan menjalankan perintah berikut di client Nakula:
```bash
lynx parikesit.abimanyu.a16.com/testerror
lynx parikesit.abimanyu.a16.com/secret

```
## Soal 16
Buatlah suatu konfigurasi virtual host agar file asset www.parikesit.abimanyu.yyy.com/public/js menjadi 
www.parikesit.abimanyu.yyy.com/js 

**Penyelesaian**
Sebelum memulai, pastikan untuk melakukan konfigurasi awal terlebih dahulu. Di sini, kita hanya perlu menetapkan Alias "/js" ke "/var/www/parikesit.abimanyu.a16/public/js" untuk mempersingkat konfigurasi virtual host. Selain itu, kami juga memanfaatkan ServerName dan ServerAlias untuk memastikan virtual host berjalan dengan baik.

**Node Abimanyu**
```bash
echo -e '<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/parikesit.abimanyu.a16
  ServerName parikesit.abimanyu.a16.com
  ServerAlias www.parikesit.abimanyu.a16.com

  <Directory /var/www/parikesit.abimanyu.a16/public>
          Options +Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.a16/secret>
          Options -Indexes
  </Directory>

  Alias "/public" "/var/www/parikesit.abimanyu.a16/public"
  Alias "/secret" "/var/www/parikesit.abimanyu.a16/secret"
  Alias "/js" "/var/www/parikesit.abimanyu.a16/public/js"

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.a16.com.conf
```

**Node Client (Sadewa)***
```bash
lynx parikesit.abimanyu.a16.com/js

```
## Soal 17

Agar aman, buatlah konfigurasi agar www.rjp.baratayuda.abimanyu.yyy.com hanya dapat diakses melalui port 14000 dan 14400.

**Penyelesaian**

Sebelum mulai, diperlukan persiapan awal. Ini melibatkan penyesuaian pada port-port khusus. Cukup ubah berkas ports.conf dengan menambahkan Listen 14000 dan Listen 14400. Selain itu, perlu modifikasi pada <VirtualHost *:14000 *:14400>.
**Node Abimanyu**
```bash
echo -e '<VirtualHost *:14000 *:14400>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/rjp.baratayuda.abimanyu.a16
  ServerName rjp.baratayuda.abimanyu.a16.com
  ServerAlias www.rjp.baratayuda.abimanyu.a16.com

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/rjp.baratayuda.abimanyu.a16.com.conf

echo -e '# If you just change the port or add more ports here, you will likely also
# have to change the VirtualHost statement in
# /etc/apache2/sites-enabled/000-default.conf

Listen 80
Listen 14000
Listen 14400

<IfModule ssl_module>
        Listen 443
</IfModule>

<IfModule mod_gnutls.c>
        Listen 443
</IfModule>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet' > /etc/apache2/ports.conf

a2ensite rjp.baratayuda.abimanyu.a16.com.conf

service apache2 restart
```

**Node Client (Sadewa)**
```bash
lynx rjp.baratayuda.abimanyu.a16.com:14000
lynx rjp.baratayuda.abimanyu.a16.com:14400
```
Result
Port 14000 atau 14400 image

Port yang tidak sesuai image

## Soal 18
Untuk mengaksesnya buatlah autentikasi username berupa “Wayang” dan password “baratayudayyy” dengan yyy merupakan kode kelompok. Letakkan DocumentRoot pada /var/www/rjp.baratayuda.abimanyu.yyy.

**Penyelesaian**
Sebelum memulai tugas, langkah awalnya adalah melakukan konfigurasi. Untuk mengamankan server, diperlukan pengaturan AuthType dan Require Valid-User. Kemudian, AuthUserFile akan menentukan lokasi untuk melakukan penulisan. Sementara AuthName merupakan jenis konten otentikasi pada apache2.

**Node Abimanyu**
```bash
echo -e '<VirtualHost *:14000 *:14400>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/rjp.baratayuda.abimanyu.a16
  ServerName rjp.baratayuda.abimanyu.a16.com
  ServerAlias www.rjp.baratayuda.abimanyu.a16.com

  <Directory /var/www/rjp.baratayuda.abimanyu.a16>
          AuthType Basic
          AuthName "Restricted Content"
          AuthUserFile /etc/apache2/.htpasswd
          Require valid-user
  </Directory>

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/rjp.baratayuda.abimanyu.a16.com.conf

a2ensite rjp.baratayuda.abimanyu.a16.com.conf

service apache2 restart
```
Tambahkan autentikasi dengan menggunakan command htpasswd. Lalu untuk -c itu adalah created dan -b yang merupakan bcrypt agar password yang kita isi akan dilakukan hash terlebih dahulu sebelum disimpan.

```bash
htpasswd -c -b /etc/apache2/.htpasswd Wayang baratayudaa16
```
**Node Client (Sadewa)**
```bash
lynx rjp.baratayuda.abimanyu.a16.com:14000
lynx rjp.baratayuda.abimanyu.a16.com:14400
```

## Soal 19
Buatlah agar setiap kali mengakses IP dari Abimanyu akan secara otomatis dialihkan ke www.abimanyu.yyy.com (alias)

**Penyelesaian**

Sebelum memulai tindakan ini, pastikan untuk melakukan konfigurasi awal terlebih dahulu. Untuk memastikan bahwa ketika mengakses IP dari abimanyu, secara otomatis akan diarahkan ke www.abimanyu.a16.com, kita perlu menggunakan file Redirect yang akan menunjuk ke halaman yang diinginkan. Saya akan memasukkan konfigurasi ini ke dalam file 000-default.conf karena merupakan pengaturan default dari layanan Apache.

**Node Abimanyu**
```bash
echo -e '<VirtualHost *:80>
    ServerAdmin webmaster@abimanyu.a16.com
    DocumentRoot /var/www/html

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    Redirect / http://www.abimanyu.a16.com/
</VirtualHost>' > /etc/apache2/sites-available/000-default.conf
Config test

apache2ctl configtest
service apache2 restart
```
**Node Client (Sadewa)**
```bash
lynx 10.7.3.3
```

## Soal 20
Karena website www.parikesit.abimanyu.yyy.com semakin banyak pengunjung dan banyak gambar gambar random, maka ubahlah request gambar yang memiliki substring “abimanyu” akan diarahkan menuju abimanyu.png.

**Penyelesaian**

Langkah pertama perlu untuk melakukan setup terlebih dahulu.


**Node Abimanyu** 
Jangan lupa untuk menjalankan perintah berikut agar dapat melakukan rewrite modul
```bash
a2enmod rewrite
Lalu jalankan perintah tersebut untuk melakukan rewrite terhdap directory parikesit.abimanyu.a16

echo 'RewriteEngine On
RewriteCond %{REQUEST_URI} ^/public/images/(.*)abimanyu(.*)
RewriteCond %{REQUEST_URI} !/public/images/abimanyu.png
RewriteRule abimanyu http://parikesit.abimanyu.a16.com/public/images/abimanyu.png$1 [L,R=301]' > /var/www/parikesit.abimanyu.a16/.htaccess
Ubah konfigurasi dan gunakan AllowOverride All untuk mengkonfigurasi nya dengan .htaccess sebelumnya.

echo -e '<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/parikesit.abimanyu.a16

  ServerName parikesit.abimanyu.a16.com
  ServerAlias www.parikesit.abimanyu.a16.com

  <Directory /var/www/parikesit.abimanyu.a16/public>
          Options +Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.a16/secret>
          Options -Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.a16>
          Options +FollowSymLinks -Multiviews
          AllowOverride All
  </Directory>

  Alias "/public" "/var/www/parikesit.abimanyu.a16/public"
  Alias "/secret" "/var/www/parikesit.abimanyu.a16/secret"
  Alias "/js" "/var/www/parikesit.abimanyu.a16/public/js"

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.a16.com.conf

service apache2 restart
```

**Node Client (Sadewa)**
```bash
lynx parikesit.abimanyu.a16.com/public/images/not-abimanyu.png
lynx parikesit.abimanyu.a16.com/public/images/abimanyu-student.jpg
lynx parikesit.abimanyu.a16.com/public/images/abimanyu.png
lynx parikesit.abimanyu.a16.com/public/images/notabimanyujustmuseum.177013
```



