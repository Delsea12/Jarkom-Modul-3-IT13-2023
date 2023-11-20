# Jarkom-Modul-3-IT13-2023

|       Nama      | NRP        | 
| -----------     | :---------: 
| Della Setyowati | 5027211044 | 
| Wisnu Adjie Saka| 5027211051 | 


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
### No. 6
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
### No. 7
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
### No. 8
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
### No. 9
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
### No. 10
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
### No. 11
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
### No. 12
Selanjutnya LB ini hanya boleh diakses oleh client dengan IP [Prefix IP].3.69, [Prefix IP].3.70, [Prefix IP].4.167, dan [Prefix IP].4.168.

### Jawaban No.12
Pada soal ini kita diminta untuk membatasi akses website kita, client dengan IP tertentu saja yang dapat masuk (ketentuan ada pada soal). Jika kita menjalankan perintah dibawah ini, dikarenakan bukan IP yang dapat melakukan akses, maka output nya akan "Forbidden"
```
lynx 10.70.2.3:801
```

##### Output
![image](https://github.com/Delsea12/Jarkom-Modul-3-IT13-2023/assets/113821220/97e337ce-f39b-4af7-8326-b910482b4765)
-



