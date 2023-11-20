# Jarkom-Modul-3-IT13-2023

|       Nama      | NRP        | 
| -----------     | :---------: 
| Della Setyowati | 5027211044 | 
| Wisnu Adjie Saka| 5027211051 | 


## Daftar Isi

- [Soal No.0](#0)
- [Soal No.1](#1)
- [Soal No.2](#2)
- [Soal No.3](#3)
- [Soal No.4](#4)
- [Soal No.5](#5)
- [Soal No.6](#6)
- [Soal No.7](#7)
- [Soal No.8](#8)
- [Soal No.9](#9)
- [Soal No.10](#10)
- [Soal No.11](#11)
- [Soal No.12](#12)
- [Soal No.13](#13)
- [Soal No.14](#14)
- [Soal No.15](#15)
- [Soal No.16](#16)
- [Soal No.17](#17)
- [Soal No.18](#18)
- [Soal No.19](#19)
- [Soal No.20](#20)

## <a name="0"></a> Soal 0
Melakukan register domain berupa ```riegel.canyon.yyy.com``` untuk worker Laravel dan ```granz.channel.yyy.com``` untuk worker PHP dan mengarah pada worker yang memiliki IP [prefix IP].x.1.
## Jawaban No.0
Pada server DNS (Heither), lakukan beberapa perintah berikut

```
apt-get update
apt-get install bind9 -y
```
Setelah itu, dapat dilakukan konfigurasi untuk riegel dan granz
```
 zone "riegel.canyon.it13.com" {
        type master;
        file "/etc/bind/jarkom/riegel.canyon.it13.com";
};

zone "granz.channel.it13.com" {
        type master;
        file "/etc/bind/jarkom/granz.channel.it13.com";
};
```
```
# granz.channel.it13.com
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.it13.com. granz.channel.it13.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.it13.com.
@       IN      A       10.70.1.2 //dns server
@       IN      AAAA    ::1

#  riegel.canyon.it13.com
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.it13.com. riegel.canyon.it13.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.it13.com.
@       IN      A       10.70.1.2
@       IN      AAAA    ::1
```
- Lakukan restart untuk DNS dengan perintah berikut 
```
service bind9 restart
```
- Lakukan testing pada client dengan cara ping riegel 
![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176038734404255754/riegel-revolte.png?ex=656d6a6c&is=655af56c&hm=9dfd6759192fe45278a163709d3be1aeac252483fcc865a7c10164a6c3a0349a&)

- Ping granz
![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176038890449154088/granz-sein.png?ex=656d6a91&is=655af591&hm=741a8c839af8e8fb5040c902bc545e8804004052c2aefe730a672c39bef960fa&)

## <a name="1"></a> Soal No.1
Lakukan konfigurasi sesuai dengan peta yang sudah diberikan. 
## Jawaban No.1
- Aura (DHCP Relay)
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.70.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.70.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 10.70.3.12
	netmask 255.255.255.0


auto eth4
iface eth4 inet static
	address 10.70.4.12
	netmask 255.255.255.0
```
- Himmel (DHCP Server)
```
auto eth0
iface eth0 inet static
	address 10.70.1.2
	netmask 255.255.255.0
	gateway 10.70.1.1
```
- Heiter (DNS Server)
```
auto eth0
iface eth0 inet static
	address 10.70.1.3
	netmask 255.255.255.0
	gateway 10.70.1.1

```
- Denken (Database Server)
```
auto eth0
iface eth0 inet static
	address 10.70.2.2
	netmask 255.255.255.0
	gateway 10.70.2.1

```
- Eisen (Load Balancer)
```
auto eth0
iface eth0 inet static
	address 10.70.2.3
	netmask 255.255.255.0
	gateway 10.70.2.1
```
- Frieren (Laravel Worker)
```
auto eth0
iface eth0 inet static
	address 10.70.4.1
	netmask 255.255.255.0
	gateway 10.70.4.12
```
- Flamme (Laravel Worker)
```
auto eth0
iface eth0 inet static
	address 10.70.4.2
	netmask 255.255.255.0
	gateway 10.70.4.12
```
- Fern (Laravel Worker)
```
auto eth0
iface eth0 inet static
	address 10.70.4.3
	netmask 255.255.255.0
	gateway 10.70.4.12
```
- Lawine (PHP Worker)
```
auto eth0
iface eth0 inet static
	address 10.70.3.1
	netmask 255.255.255.0
	gateway 10.70.3.12
```
- Linie (PHP Worker)
```
auto eth0
iface eth0 inet static
	address 10.70.3.2
	netmask 255.255.255.0
	gateway 10.70.3.12

```
- Lugner (PHP Worker)
```
auto eth0
iface eth0 inet static
	address 10.70.3.3
	netmask 255.255.255.0
	gateway 10.70.3.12
```
- Revolte (Client)
```
auto eth0
iface eth0 inet dhcp
```
- Richter (Client)
```
auto eth0
iface eth0 inet dhcp
```
- Sein (Client)
```
auto eth0
iface eth0 inet dhcp
```
- Stark (Client)
```
auto eth0
iface eth0 inet dhcp
```
![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176043671284629594/image.png?ex=656d6f05&is=655afa05&hm=5c8b398dc46ae0206160301a681a1a96241c1c894fc501fbf23f56565d313e35&)


## <a name="2"></a> Soal No.2
Semua **CLIENT** harus menggunakan konfigurasi dari DHCP Server. Dan client yang melalui Switch3 mendapatkan range IP dari **[prefix IP].3.16 - [prefix IP].3.32** dan **[prefix IP].3.64 - [prefix IP].3.80**
## Jawaban No.2
- Lakukan penginstallan pada Aura (DHCP Relay)
```
apt-get update
apt-get install isc-dhcp-relay -y
service isc-dhcp-relay start
```
- Lakukan konfigurasi pada Aura (DHCP Relay)
```
echo 'SERVERS="10.70.1.2"
INTERFACES="eth1 eth3 eth4"
OPTIONS=""' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' > /etc/sysctl.conf
```
- Pada Himmel (DHCP Server) dilakukan konfigurasi
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install isc-dhcp-server

# DHCP Server
echo 'INTERFACESv4="eth0"
INTERFACESv6="" ' > /etc/default/isc-dhcp-server
echo 'subnet 10.70.1.0 netmask 255.255.255.0 {}

subnet 10.70.3.0 netmask 255.255.255.0 { # [prefix.ip] switch 3
    range 10.70.3.16 10.70.3.32; # range ip
    range 10.70.3.64 10.70.3.80; # range ip
    option routers 10.70.3.12; # [prefix ip]. switch 3. bebas
}
service isc-dhcp-server restart
service isc-dhcp-server status
```
## <a name="3"></a> Soal No.3
Client yang melalui Switch4 mendapatkan range IP dari **[prefix IP].4.12 - [prefix IP].4.20** dan **[prefix IP].4.160 - [prefix IP].4.168**
## Jawaban No.3
- Dilakukan konfigurasi untuk switch 4 pada Himmel (DHCP Server)
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install isc-dhcp-server

# DHCP Server
echo 'INTERFACESv4="eth0"
INTERFACESv6="" ' > /etc/default/isc-dhcp-server
echo 'subnet 10.70.1.0 netmask 255.255.255.0 {}

subnet 10.70.4.0 netmask 255.255.255.0 {
    range 10.70.4.12 10.70.4.20;
    range 10.70.4.160 10.70.4.168;
    option routers 10.70.4.12;
}' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
service isc-dhcp-server status
```
## <a name="4"></a> Soal No.4
Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut
## Jawaban No.4
- Melakukan konfigurasi pada Himmel (DHCP Server) untuk DNS 

```
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install isc-dhcp-server

# DHCP Server
echo 'INTERFACESv4="eth0"
INTERFACESv6="" ' > /etc/default/isc-dhcp-server
echo 'subnet 10.70.1.0 netmask 255.255.255.0 {}

subnet 10.70.3.0 netmask 255.255.255.0 { # [prefix.ip] switch 3
    range 10.70.3.16 10.70.3.32; # range ip
    range 10.70.3.64 10.70.3.80; # range ip
    option routers 10.70.3.12; # [prefix ip]. switch 3. bebas
    option broadcast-address 10.70.3.255; 
    option domain-name-servers 10.70.1.3; #[prefix.ip].dns
}

subnet 10.70.4.0 netmask 255.255.255.0 {
    range 10.70.4.12 10.70.4.20;
    range 10.70.4.160 10.70.4.168;
    option routers 10.70.4.12;
    option broadcast-address 10.70.4.255;
    option domain-name-servers 10.70.1.3;
}' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
service isc-dhcp-server status
```
- Melakukan ping
![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176053631653519390/riegel-stark.png?ex=656d784b&is=655b034b&hm=a1296d863ee5a5ed5b2949ddad307037e6ea5aa116dde6fbfcfe35b8fae9a9f9&)

![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176053693381091348/granz-stark.png?ex=656d785a&is=655b035a&hm=030681a7759113c82cfe6df2e7fcadee5e54ebcfed1a4f994baa3bce7c28c971&)
## <a name="5"></a> Soal No.5
Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit 
## Jawaban No.5
- Melakukan setup pada Himmel (DNS Server) 
```
echo 'subnet 10.70.1.0 netmask 255.255.255.0 {}

subnet 10.70.3.0 netmask 255.255.255.0 { # [prefix.ip] switch 3
    range 10.70.3.16 10.70.3.32; # range ip
    range 10.70.3.64 10.70.3.80; # range ip
    option routers 10.70.3.12; # [prefix ip]. switch 3. bebas
    option broadcast-address 10.70.3.255; 
    option domain-name-servers 10.70.1.3; #[prefix.ip].dns
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 10.70.4.0 netmask 255.255.255.0 {
    range 10.70.4.12 10.70.4.20;
    range 10.70.4.160 10.70.4.168;
    option routers 10.70.4.12;
    option broadcast-address 10.70.4.255;
    option domain-name-servers 10.70.1.3;
    default-lease-time 720;
    max-lease-time 5760;
}' > /etc/dhcp/dhcpd.conf
```
- Melakukan pengecekan waktu pada switch3
![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176047712639131668/switch3-no_5.png?ex=656d72c8&is=655afdc8&hm=46ef94c0d7bca444eaa5ab03222236f5d1ba8e66baf933d914fff837cfe1ef73&)

- Melakukan pengecekan waktu pada switch4
![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176047822378913792/stark-switch4.png?ex=656d72e2&is=655afde2&hm=3571b305167715f690674b6f992ed03b48c8049f0274c9fd8a96237a1d56e53f&)

---
### CLIENT (Untuk no. 6-12)
Ada beberapa yang harus diinstall pada client, untuk nomor 6-12
```
apt-get update
apt install -y lynx
apt-get install apache2-utils
apt-get install htop -y
```

---
## <a name="6"></a> Soal No.6
Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3.

### Jawaban No.6
Yang harus kita lakukan untuk menjawab soal ini, pertama kita harus membuka web console pada ketiga php worker, yaitu lawine, linie, dan lugner. Setelah itu ada beberapa hal yang harus kita install : 
```
apt update
apt install -y nginx
apt install -y php7.3-fpm
apt-get install -y unzip
```

Setelah itu pada masing-masing worker kita akan melakukan download, unzip, dan memasukan file resource website nya dari google drive yang telah diberikan, berikut perintah nya : 
```
mkdir /var/www/lugner
curl -k -s -L "https://drive.google.com/uc?export=download&id=1ViSkRq7SmwZgdK64eRbr5Fm1EGCTPrU1" -o /var/www/lugner/website.zip
unzip /var/www/lugner/website.zip -d /var/www/lugner
chown -R www-data:www-data /var/www/lugner
chmod -R 755 /var/www/lugner
```

Setelah itu buat file konfigurasi pada path "/etc/nginx/sites-available/namaworker--" dengan isi konfigarasi sebagai berikut : 

- Lawine
```
server {
    listen 80;
    server_name _;
    root /var/www/lawine/modul-3;
    
    index index.php index.html index.htm;

   location / {
 			try_files $uri $uri/ /index.php?$query_string;
 	}

 	# pass PHP scripts to FastCGI server
 	location ~ \.php$ {
 	include snippets/fastcgi-php.conf;
 	fastcgi_pass unix:/var/run/php/php7.3-fpm.sock;
 	}

 location ~ /\.ht {
 			deny all;
 	}

 	error_log /var/log/nginx/jarkom_error.log;
 	access_log /var/log/nginx/jarkom_access.log;
 }
```

- Linie
```
server {
    listen 80;
    server_name _;
    root /var/www/linie/modul-3;
    
    index index.php index.html index.htm;

     location / {
 			try_files $uri $uri/ /index.php?$query_string;
 	}

 	# pass PHP scripts to FastCGI server
 	location ~ \.php$ {
 	include snippets/fastcgi-php.conf;
 	fastcgi_pass unix:/var/run/php/php7.3-fpm.sock;
 	}

 location ~ /\.ht {
 			deny all;
 	}

 	error_log /var/log/nginx/jarkom_error.log;
 	access_log /var/log/nginx/jarkom_access.log;
 }
```

- Lugner
```
server {
    listen 80;
    server_name _;
    root /var/www/lugner/modul-3;
    
    index index.php index.html index.htm;

    location / {
 			try_files $uri $uri/ /index.php?$query_string;
 	}

 	# pass PHP scripts to FastCGI server
 	location ~ \.php$ {
 	include snippets/fastcgi-php.conf;
 	fastcgi_pass unix:/var/run/php/php7.3-fpm.sock;
 	}

 location ~ /\.ht {
 			deny all;
 	}

 	error_log /var/log/nginx/jarkom_error.log;
 	access_log /var/log/nginx/jarkom_access.log;
 }
```

Setelah itu pada setiap console worker jalankan perintah berikut
```
ln -s /etc/nginx/sites-available/namaworker-- /etc/nginx/sites-enabled/
```
```
unlink /etc/nginx/sites-enabled/default
```
```
service nginx restart
```

##### Output
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/52e7ae4a-8bea-42d5-baf5-ea41e416509a)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/05ae529e-6235-4932-9cb8-3a68cd032d41)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/7b6dce63-5f80-47bb-8878-5edf8db65f0b)
-


---
### Load Balancer
Untuk nomor 7-12 saya membuat di satu konfigurasi yang sama, dikarenakan nomor 7-12 terdapat di node  yang sama yaitu node load balancer aka Eisen. Pertama ada beberapa hal yang harus kita install
```
apt update
apt install -y nginx
apt install -y apache2-utils
```

Karena nomer 10 diminta untuk memasukan password, berikut perintah yang harus kita masukan
```
mkdir /etc/nginx/rahasisakita
htpasswd -b -c /etc/nginx/rahasisakita/htpasswd netics ajkit13
```

Berikut adalah konfigurasi untuk nomer 7-12, disini saya membuat file nya pada path "/etc/nginx/sites-available/load-balancer"
```
upstream roundrobin {
    server 10.70.3.1; # IP Lawine
    server 10.70.3.2; # IP Linie
    server 10.70.3.3; # IP Lugner
}

upstream roundrobin1 {
    server 10.70.3.1; # IP Lawine
    server 10.70.3.2; # IP Linie
    server 10.70.3.3; # IP Lugner
}

upstream roundrobin2 {
    server 10.70.3.1; # IP Lawine
    server 10.70.3.2; # IP Linie
    server 10.70.3.3; # IP Lugner
}

upstream leastconn {
    least_conn;	
    server 10.70.3.1; # IP Lawine
    server 10.70.3.2; # IP Linie
    server 10.70.3.3; # IP Lugner
}

upstream ip_hash {
    ip_hash;
    server 10.70.3.1; # IP Lawine
    server 10.70.3.2; # IP Linie
    server 10.70.3.3; # IP Lugner
}

upstream generic_hash {
    hash $request_uri consistent;
    server 10.70.3.1; # IP Lawine
    server 10.70.3.2; # IP Linie
    server 10.70.3.3; # IP Lugner
}

upstream worker1 {
    server 10.70.3.1; # IP Lawine
}

upstream worker2 {
    server 10.70.3.1; # IP Lawine
    server 10.70.3.2; # IP Linie
}

upstream worker3 {
    server 10.70.3.1; # IP Lawine
    server 10.70.3.2; # IP Linie
    server 10.70.3.3; # IP Lugner
}



server {
    listen 80;
    server_name _;

    location / {
	auth_basic "Restricted Content";
	auth_basic_user_file /etc/nginx/rahasisakita/htpasswd;

        proxy_pass http://roundrobin;
    }

    location /its {
        proxy_pass https://www.its.ac.id;
    }
}

server {
    listen 801;
    server_name _;

    location / {
        proxy_pass http://roundrobin1;

	allow 10.70.3.69;
	allow 10.70.3.70;
	allow 10.70.4.167;
	allow 10.70.4.168;
	deny all;
    }
}

server {
    listen 802;
    server_name _;

    location / {
        proxy_pass http://leastconn;
    }
}

server {
    listen 803;
    server_name _;

    location / {
        proxy_pass http://ip_hash;
    }
}

server {
    listen 804;
    server_name _;

    location / {
        proxy_pass http://generic_hash;
    }
}


server {
    listen 805;
    server_name _;

    location / {
        proxy_pass http://roundrobin2;
    }
}


server {
    listen 81;
    server_name _;

    location / {
        proxy_pass http://worker1;
    }
}

server {
    listen 82;
    server_name _;

    location / {
        proxy_pass http://worker2;
    }
}

server {
    listen 83;
    server_name _;

    location / {
        proxy_pass http://worker3;
    }
}
```

Setelah memasukan konfigurasi nya lakukan perintah ini 
```
ln -s /etc/nginx/sites-available/load-balancer /etc/nginx/sites-enabled/
```
```
unlink /etc/nginx/sites-enabled/default
```
```
service nginx restart
```

---
## <a name="7"></a> Soal No.7
Kepala suku dari Bredt Region memberikan resource server sebagai berikut:
Lawine, 4GB, 2vCPU, dan 80 GB SSD.
Linie, 2GB, 2vCPU, dan 50 GB SSD.
Lugner 1GB, 1vCPU, dan 25 GB SSD.
aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second.

### Jawaban No.7
Pada nomer 7 ini kita diminta untuk membuat load balancer dan melakukan testing dengan kententuan "1000 request dan 100 request/second". Setelah melakukan konfigurasi yang sudahdi jelaskan di ```Load Balancer``` , pada client kita akan menjalankan perintah 
```
ab -n 1000 -c 100 http://10.70.2.3:805/ 
```
Dan bisa kita liat output nya adalah sebagai berikut
![ss mod3 7](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/061a7c09-f938-4e99-b8ff-784add86b7da)
Request per Second nya adalah 335.55

---
## <a name="8"></a> Soal No.8
Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
- Nama Algoritma Load Balancer
- Report hasil testing pada Apache Benchmark
- Grafik request per second untuk masing masing algoritma. 
- Analisis


### Jawaban No.8
Pada nomor ini kita diminta untuk membuat laporan analisis (Grimoire) dengan beberapa ketentuan pada soal. Ini adalah link untuk Grimoire kelompok kami "[Grimoire IT13](https://drive.google.com/file/d/14h0cMQdB2nH8Dd5lOG7M1XEUZ4dOiO1M/view?usp=sharing)". Berikut adalah hasil dari analisis nya : 

#### Round Robin
##### Perintah
```
ab -n 200 -c 10 http://10.70.2.3:805/
```
##### Hasil 
![ss 8_ab_rr](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/42e4dd01-6b0b-4be3-b742-fb93fd66d8a9)
-
![ss 8_ht_1](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/c9e26270-4e00-4a8b-9a0b-32acfdd777c3)
-
![ss 8_ht_2](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/1694b32c-50ee-4ef5-8b8c-5a12e7f41890)
-
![ss 8_ht_3](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/663f2cf4-263c-4a92-b0bf-430270c73d91)
-

#### Leastconn
##### Perintah
```
ab -n 200 -c 10 http://10.70.2.3:802/
```
##### Hasil 
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/4a2458b8-53d8-4871-bcb2-eee3fbf9b110)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/68ca54c1-7326-4168-a69b-74f8e87c63b0)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/f2657ad1-37cd-48dd-9f91-ce228d4c8644)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/caa5e09b-ed95-4bb7-9044-f515f59e58ad)
-

#### Ip Hash
##### Perintah
```
ab -n 200 -c 10 http://10.70.2.3:803/
```
##### Hasil 
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/468d206c-798e-4fd3-a277-9c735e5e6d0a)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/0cb3ac6a-9110-44e4-bdb2-826cef38987a)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/be12be9e-3413-44a5-b1d2-a1318f92ba17)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/e6d601ca-6e33-4f63-b378-7568b8bb87e5)
-

#### Generic Hash
##### Perintah
```
ab -n 200 -c 10 http://10.70.2.3:804/
```
##### Hasil 
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/649607cf-d75d-42d9-bd69-39a1cf95a05a)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/e59f4613-0870-4ac2-a632-e89b43d7aee4)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/70ef56dc-cfc7-4e47-9508-f98f7a464094)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/06fda7f8-f2ba-4974-b639-70b82bedca3c)
-

#### Grafik
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/693c8d6c-279d-491b-bedc-df757fba14ae)
-

#### Analisis
Berdasarkan hasil testing dengan Apache Benchmark menggunakan 200 request
dan 10 request/second, algoritma Load Balancer "Leastconn" menunjukkan kinerja
tertinggi dengan throughput sebesar 379.96 request per second, diikuti oleh "Ip
Hash" (382.66 req/s), "Generic Hash" (383.15 req/s), dan "Round Robin" (364.83
req/s).


---
## <a name="9"></a> Soal No.9
Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire.

### Jawaban No.9
Sama seperti nomor 8, kita diminta untuk membuat laporan analisis (Grimoire) dengan beberapa ketentuan pada soal. Ini adalah link untuk Grimoire kelompok kami "[Grimoire IT13](https://drive.google.com/file/d/14h0cMQdB2nH8Dd5lOG7M1XEUZ4dOiO1M/view?usp=sharing)". Berikut adalah hasil dari analisis nya :

#### Worker 1
##### Perintah
```
ab -n 100 -c 10 http://10.70.2.3:81/
```
##### Hasil 
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/93855ee5-112a-4480-9fae-b5a6ef0e3d18)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/bdab134c-e178-4913-af16-8312ecb7463d)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/901815c2-5336-494e-bc73-f51984e3b152)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/982b7a8a-ab5a-4ae5-80f8-e8e9583c9ff3)
-

#### Worker 2
##### Perintah
```
ab -n 100 -c 10 http://10.70.2.3:82/
```
##### Hasil 
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/9f1d09b1-e907-4363-b1cc-9efbd311340d)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/e464a207-59de-4db7-9018-f25bdf03ebda)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/6dda9e55-2f46-4d6d-a48a-d07ba3b2eed2)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/3e783e51-1561-43b0-99d9-c690fd735d63)
-

#### Worker 3
##### Perintah
```
ab -n 100 -c 10 http://10.70.2.3:83/
```
##### Hasil 
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/15dd46a8-9e89-48d7-8e71-f632f1f530a5)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/b0037af0-1176-49a7-896d-a06c53f5a74c)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/dd1d86d6-de13-4f79-bdb6-5bc371d62230)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/2e2872a4-197c-467c-b54e-6d15e06957ca)
-

#### Grafik
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/5915f99b-542a-4ac8-814b-6dbe32db3125)
-

#### Analisis
Dalam pengujian menggunakan algoritma Round Robin dengan 100 request dan 10
request/second, terlihat bahwa kinerja Load Balancer meningkat seiring dengan
peningkatan jumlah worker, dengan throughput sebesar 393.67 request per second
untuk 1 worker, 380.04 request per second untuk 2 worker, dan 383.79 request per
second untuk 3 worker.



---
## <a name="10"></a> Soal No.10
Selanjutnya coba tambahkan konfigurasi autentikasi di LB dengan dengan kombinasi username: “netics” dan password: “ajkyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/rahasisakita/

### Jawaban No.10
Pada nomor 10 ini kita diminta untuk memasukan konfigurasi autentikasi pada load balancer, untuk konfigurasi nya sudah di jelaskan di ```Load Balancer```. Setelah melakukan konfigurasi kita akan melakukan pengetesan dengan masuk ke website nya dan memasukan id dan password sesuai yang kita buat di konfigurasi nya. ID : netics , password : ajkit13
```
lynx 10.70.2.3:80
```

##### Output
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/00ab5eda-8e00-40e1-bf00-690a6bc58de5)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/dacce817-c747-4666-86ad-8ac5092fb1b5)
-
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/cebb0d35-442a-492c-ba51-808520466a7a)
-



---
## <a name="11"></a> Soal No.11
Lalu buat untuk setiap request yang mengandung /its akan di proxy passing menuju halaman https://www.its.ac.id.

### Jawaban No.11
Pada soal ini kita diminta untuk membuat request yang mengandung /its akan di proxy passing menuju halaman https://www.its.ac.id. Untuk konfigurasi nomor ini sudah dijelaskan di ```Load Balancer```. Setelah melakukan konfigurasi jalankan perintah ini untuk melihat apakah berhasil atau tidak
```
lynx 10.70.2.3/its
```

##### Output
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/fbcf9451-0846-4a3c-9579-4671986ce5c4)
-


---
## <a name="12"></a> Soal No.12
Selanjutnya LB ini hanya boleh diakses oleh client dengan IP [Prefix IP].3.69, [Prefix IP].3.70, [Prefix IP].4.167, dan [Prefix IP].4.168.

### Jawaban No.12
Pada soal ini kita diminta untuk membatasi akses website kita, client dengan IP tertentu saja yang dapat masuk (ketentuan ada pada soal). Jika kita menjalankan perintah dibawah ini, dikarenakan bukan IP yang dapat melakukan akses, maka output nya akan "Forbidden"
```
lynx 10.70.2.3:801
```

##### Output
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/97e337ce-f39b-4af7-8326-b910482b4765)
-



##
Karena para petualang kehabisan uang, mereka kembali bekerja untuk mengatur ```riegel.canyon.yyy.com.```

## <a name="13"></a> Soal No.13
Semua data yang diperlukan, diatur pada Denken dan harus dapat diakses oleh Frieren, Flamme, dan Fern
## Jawaban No.13
- Melakukan setup pada denken
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install mariadb-server -y
service mysql start
```
```
mysql
CREATE USER 'kelompokit13'@'%' IDENTIFIED BY 'passwordit13';
CREATE USER 'kelompokit13'@'localhost' IDENTIFIED BY 'passwordit13';
CREATE DATABASE dbkelompokit13;
GRANT ALL PRIVILEGES ON *.* TO 'kelompokit13'@'%';
GRANT ALL PRIVILEGES ON *.* TO 'kelompokit13'@'localhost';
FLUSH PRIVILEGES;

SHOW DATABASES;
```
```
echo '
!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mariadb.conf.d/
[mysqld]
skip-networking=0
skip-bind-address' > /etc/mysql/my.cnf
```
- Melakukan testing pada Laravel Worker
```
mariadb --host=10.70.2.2 --port=3306 --user=kelompokit13 --password
```
![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176057169376968755/flameel-no13.png?ex=656d7b97&is=655b0697&hm=42f43fc43c55047a6874b2eb5454c6750ecceefc33e80df98a7e31074aca0897&)

## <a name="14"></a> Soal No.14
Frieren, Flamme, dan Fern memiliki Riegel Channel sesuai dengan quest guide berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer
## Jawaban No.14
- Melakukan installasi depensi dasar
```
apt-get update

apt-get install -y lsb-release ca-certificates apt-transport-https software-properties-common gnupg2

curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
```
- Melakukan instalasi PHP
```
apt-get update
apt-get install php8.0-mbstring php8.0-xml php8.0-cli php8.0-common php8.0-intl php8.0-opcache php8.0-readline php8.0-mysql php8.0-fpm php8.0-curl unzip wget -y
apt install curl
apt install php-curl
apt install php-xml
```

- Melakukan instalasi Composer
```
wget https://getcomposer.org/download/2.0.13/composer.phar
chmod +x composer.phar
mv composer.phar /usr/bin/composer
```
- Melakukan composer update
```
apt-get install git -y
cd /var/www
git clone https://github.com/martuafernando/laravel-praktikum-jarkom.git
cd laravel-praktikum-jarkom
composer update
```
- Setelah melakukan composer update, lakukan konfigurasi pada worker
```
cp .env.example .env
nano .env

APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=10.70.2.2
DB_PORT=3306
DB_DATABASE=dbkelompokit13
DB_USERNAME=kelompokit13
DB_PASSWORD=passwordit13

BROADCAST_DRIVER=log
CACHE_DRIVER=file
FILESYSTEM_DISK=local
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

MEMCACHED_HOST=127.0.0.1

- /var/www/laravel-praktikum-jarkom
php artisan migrate:fresh
php artisan db:seed --class=AiringsTableSeeder
php artisan key:generate
php artisan config:cache
php artisan migrate
php artisan db:seed
php artisan storage:link
php artisan jwt:secret
php artisan config:clear
chown -R www-data.www-data /var/www/laravel-praktikum-jarkom/storage
```

```
cd /etc/nginx/sites-available/implementasi
echo ' server {
 	listen 8001;

 	root /var/www/laravel-praktikum-jarkom/public;

 	index index.php index.html index.htm;
 	server_name _;

 	location / {
 			try_files $uri $uri/ /index.php?$query_string;
 	}

 	# pass PHP scripts to FastCGI server
 	location ~ \.php$ {
 	include snippets/fastcgi-php.conf;
 	fastcgi_pass unix:/var/run/php/php8.0-fpm.sock;
 	}

    location ~ /\.ht {
 			deny all;
 	}

    error_log /var/log/nginx/implementasi_error.log;
    access_log /var/log/nginx/implementasi_access.log;
 }
' > /etc/nginx/sites-available/implementasi
ln -s /etc/nginx/sites-available/implementasi /etc/nginx/sites-enabled/
chown -R www-data.www-data /var/www/laravel-praktikum-jarkom/storage
service php8.0-fpm start
service nginx start
```
- Untuk port, pada kelompok kami membagi dengan 

    1. Fern : 8001
    2. Flamme : 8002
    3. Frieren : 8003

- Setelah melakukan konfigurasi, cek dengan ```lynx localhost:<port worker>``` (contoh : lynx localhost:8001)
![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176060089128460289/frieren-no14.png?ex=656d7e4f&is=655b094f&hm=fb7a0b40a0ec6664efd6071938672aafb087a33cb05478c7f7bddb7e18b51d19&)

## Soal No.15 - 17
Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second.
## <a name="15"></a> Soal No.15
POST /auth/register
## Jawaban No.15
- Buat file register.json yang nantinya akan dikirimkan dalam perintah /POST pada client
- Jalankan perintah berikut pada ***client***
- Untuk bagian http://10.69.4.2:8001 disesuaikan dengan ip worker:portnya yang ingin diuji
```
ab -n 100 -c 10 -p register.json -T application/json http://10.70.4.3:8001/api/auth/register
```
- ```ip:port``` worker yang dipakai sebagai contoh disini frieren
![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176064505650876497/no_15.png?ex=656d826c&is=655b0d6c&hm=bebc81beb7879ec3be6cfc3e07baa1731d39387e2ae994401ca5084a2249c60a&)

## <a name="16"></a> Soal No.16
POST /auth/login 
## Jawaban No.16
- Buat file login.json yang nantinya akan dikirimkan dalam perintah /POST pada client
- Jalankan perintah berikut pada ***client***
-lakukan testing seperti No.15 dengan menggunakan htop
```
ab -n 100 -c 10 -p login.json -T application/json http://10.70.4.3:8001/api/auth/login
```
![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176064571757314068/login-no15.png?ex=656d827c&is=655b0d7c&hm=c9a9483995f8cd70d3cc573813d853a6a4c1d7df1edab61afced1e8d7abebb6f&)

![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176064596444983407/htop_no_15.png?ex=656d8282&is=655b0d82&hm=24be83a3046b13b501b53f49e4e1e9cb25cea9e30a09d75bb9692508d5d768cb&)

![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176064505650876497/no_15.png?ex=656d826c&is=655b0d6c&hm=bebc81beb7879ec3be6cfc3e07baa1731d39387e2ae994401ca5084a2249c60a&)
## <a name="17"></a> Soal No.17
GET /me 
## Jawaban No.17
- Untuk mendapatkan tokennya jalankan 
```
curl -X POST -H "Content-Type: application/json" -d @login.json http://10.70.4.3:8001/api/auth/login > login_output.txt
```
- Lalu lakukan set token dengan perintah berikut 
```
token=$(cat login_output.txt | jq -r '.token')
```
- Lakukan testing dengan cara menjalankan perintah berikut 
```
ab -n 100 -c 10 -H "Authorization: Bearer $token" http://10.70.4.3:8001/api/me
```
![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176066790045012009/no17-1.png?ex=656d848d&is=655b0f8d&hm=5d78bfc35ce843db905dd8bee55c6bb83b22a1d291aaea5299a8e547cbeeb51c&)

![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176066814493610004/no17-2.png?ex=656d8492&is=655b0f92&hm=b86137c30d640b8b3284eec9136e517113b8f8d604fcf067f9586803b1335f30&)

## <a name="18"></a> Soal No.18
Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur Riegel Channel maka implementasikan Proxy Bind pada Eisen untuk mengaitkan IP dari Frieren, Flamme, dan Fern
## Jawaban No.18
- Melakukan konfigurasi pada Eisen
```
echo '#Default menggunakan Round Robin
upstream worker {
    server 10.70.4.3:8001;
    server 10.70.4.2:8002;
    server 10.70.4.1:8003;
}

server {
    listen 80;
    server_name riegel.canyon.it13.com;

    location / {
        proxy_pass http://worker;
    }
}' > /etc/nginx/sites-available/laravel
ln -s /etc/nginx/sites-available/laravel /etc/nginx/sites-enabled/
service nginx restart
```
- Lakukan testing dengan cara 
```
ab -n 100 -c 10 -p login.json -T application/json http://riegel.canyon.it13.com/api/auth/login 
```
- Maka outputnya 

![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176068045874143292/no_18_client.png?ex=656d85b8&is=655b10b8&hm=279b3b19778abe81b4b196da3e70ea1e84b0405b482682ffe3b68112a9e148b2&)

- Untuk mengecek lognya gunakan perintah
```
cat /var/log/nginx/implementasi_access.log
```
![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176068001427112016/flammel-no18_.png?ex=656d85ad&is=655b10ad&hm=9d9f13f471daf9039c1e479db079cc3639faad9a8569d9c1918c9ab90a4810d0&)

![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176068742833262693/fern-no18.png?ex=656d865e&is=655b115e&hm=e2306858414b15416921834011cf0001a04d1cf581b6034a57cb93c1f87d9ec7&)

![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176068833262436373/frieren-no18.png?ex=656d8674&is=655b1174&hm=a5ad8ff40c06eddbde33ae683ae6386072ded4de8cdf570306c25562d77ef7f4&)

## <a name="19"></a> Soal No.19
Untuk meningkatkan performa dari Worker, coba implementasikan PHP-FPM pada Frieren, Flamme, dan Fern. Untuk testing kinerja naikkan 
- pm.max_children
- pm.start_servers
- pm.min_spare_servers
- pm.max_spare_servers
sebanyak tiga percobaan dan lakukan testing sebanyak 100 request dengan 10 request/second 
## Jawaban No.19
- Membuat file konfigurasi sebanyak 3 percobaan 
- melakukan testing dengan cara 
```
ab -n 100 -c 10 -p login.json -T application/json http://riegel.canyon.it13.com/api/auth/login 
```
- Script1.sh
```
#!/bin/bash
# Setup Awal
echo '[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 8
pm.start_servers = 4
pm.min_spare_servers = 3
pm.max_spare_servers = 7' > /etc/php/8.0/fpm/pool.d/www.conf

service php8.0-fpm restart
```
- Script2.sh
```
#!/bin/bash
# Setup Awal
echo '[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 10
pm.start_servers = 6
pm.min_spare_servers = 5
pm.max_spare_servers = 9' > /etc/php/8.0/fpm/pool.d/www.conf

service php8.0-fpm restart
```

- test3.sh
```
#!/bin/bash
# Setup Awal
echo '[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 15
pm.start_servers = 8
pm.min_spare_servers = 7
pm.max_spare_servers = 13' > /etc/php/8.0/fpm/pool.d/www.conf

service php8.0-fpm restart
```
- Maka hasilnya akan sebagai berikut
![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176071156386779207/test1-no_19.png?ex=656d889e&is=655b139e&hm=593e7d5635df88f6437486593a1568720e35af88f2d174827303958caa4aa139&)

![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176071207842484244/test2-no_19.png?ex=656d88aa&is=655b13aa&hm=64276cfeeaa3355c3912fb25eb5a8acd362041a5c90918488b3309fc73db3865&)

![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176071226993672223/test3-no_19.png?ex=656d88ae&is=655b13ae&hm=97e1924b0dde741598d11068df3af83f99f598f075f182219f4fa80fb3fcbe5a&)

- Penjelasan :
```pm.max_children``` : Menentukan jumlah maksimum proses anak (child processes) yang PHP-FPM dapat buat untuk melayani permintaan.

```pm.start_servers```: Menentukan jumlah proses anak yang akan dibuat saat PHP-FPM pertama kali dijalankan.

```pm.min_spare_servers```: Menentukan jumlah minimum proses anak yang akan dijaga hidup oleh PHP-FPM saat tidak ada permintaan yang diterima.

```pm.max_spare_servers```: Menentukan jumlah maksimum proses anak yang diizinkan tetap hidup oleh PHP-FPM saat tidak ada permintaan yang diterima.

- pada hasil testing, dapat dilihat bahwa rata-rata waktu processing semakin meningkat tiap script

## <a name="20"></a> Soal No.20
Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Eisen. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second
## Jawaban No.20
- Melakukan modifikasi pada Eisen dengan menambahkan ```least_conn;```

```
echo '#Default menggunakan Round Robin
upstream worker {
    least_conn;
    server 10.70.4.3:8001;
    server 10.70.4.2:8002;
    server 10.70.4.1:8003;
}

server {
    listen 80;
    server_name riegel.canyon.it13.com;

    location / {
        proxy_pass http://worker;
    }
}' > /etc/nginx/sites-available/laravel
```
- Maka didapatkan Output sebagai berikut
![untitled](https://cdn.discordapp.com/attachments/901344920361656355/1176072467387781160/no_20.png?ex=656d89d6&is=655b14d6&hm=5528a47bcabb005fe239617a5ccd8abd451eaf9f90c1bd55ccc32fa3cfdd03cc&)

- Jika dibandingkan script1 sebelum ditambahkan ```least_conn``` dengan sesudah ditambahkan, ```least_conn``` dapat bekerja dengan baik karena hasil yang didapatkan lebih signifikan


