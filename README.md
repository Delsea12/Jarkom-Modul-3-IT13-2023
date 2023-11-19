# Jarkom-Modul-3-IT13-2023

|       Nama      | NRP        | 
| -----------     | :---------: 
| Della Setyowati | 5027211044 | 
| Wisnu Adjie Saka| 5027211051 | 


### CLIENT (Untuk no. 6-12)
Ada beberapa yang harus diinstall pada client, untuk nomor 6-12
```
apt-get update
apt install -y lynx
apt-get install apache2-utils
apt-get install htop -y
```

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

### No. 7
Kepala suku dari Bredt Region memberikan resource server sebagai berikut:
Lawine, 4GB, 2vCPU, dan 80 GB SSD.
Linie, 2GB, 2vCPU, dan 50 GB SSD.
Lugner 1GB, 1vCPU, dan 25 GB SSD.
aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second.

### Jawaban No.7
Pada nomer 7 ini kita diminta untuk membuat load balancer dan melakukan testing dengan kententuan "1000 request dan 100 request/second". Karena konfigurasi sudah di jelaskan di ```Load Balancer``` 



