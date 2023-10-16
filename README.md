# Jarkom-Modul-2-E23-2023

Laporan Resmi Praktikum Jaringan Komputer Modul 2
***
## Anggota Kelompok
1. Ilham Insan Wafi (5025211255)
2. Elmira Farah Azalia (5025211197)

---
### Soal 1
---
Membuat topologi sesuai deskripsi : Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni.

---
### Jawaban
---
- Buat topologi sesuai dengan soal, yaitu Tambahkan beberapa node ethernet switch dan ubuntu, lalu buat hubungan antar node dan nama-nama dari node disesuaikan dengan ketentuan soal.

![soal1.0](img/1.0.png)

- Lakukan konfigurasi pada setiap node

Pandudewanata:
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.48.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.48.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 10.48.3.1
	netmask 255.255.255.0
```

Yudhistira:
```
auto eth0
iface eth0 inet static
	address 10.48.3.2
	netmask 255.255.255.0
	gateway 10.48.3.1
```
Sadewa:
```
auto eth0
iface eth0 inet static
	address 10.48.1.2
	netmask 255.255.255.0
	gateway 10.48.1.1
```
Nakula:
```
auto eth0
iface eth0 inet static
	address 10.48.1.3
	netmask 255.255.255.0
	gateway 10.48.1.1
```
Werkudara:
```
auto eth0
iface eth0 inet static
	address 10.48.2.2
	netmask 255.255.255.0
	gateway 10.48.2.1
```
Arjuna:
```
auto eth0
iface eth0 inet static
	address 10.48.2.3
	netmask 255.255.255.0
	gateway 10.48.2.1
```
Abimanyu:
```
auto eth0
iface eth0 inet static
	address 10.48.2.4
	netmask 255.255.255.0
	gateway 10.48.2.1
```
Wisanggeni:
```
auto eth0
iface eth0 inet static
	address 10.48.2.5
	netmask 255.255.255.0
	gateway 10.48.2.1
```
Prabakusuma:
```
auto eth0
iface eth0 inet static
	address 10.48.2.6
	netmask 255.255.255.0
	gateway 10.48.2.1
```

- Lakukan config berikut agar topologi yang dibuat bisa mengakses jaringan keluar:
> Ketikkan command dibawah ini pada router Pandudewanata
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s [Prefix IP].0.0/16
```
> Lalu cek IP DNS, dengan mengetikkan command dibawah ini pada pandudewanata
```
cat /etc/resolv.conf
```
Hasilnya adalah:
```
nameserver 192.168.122.1
```
> Lalu ketikkan command dibawah ini di node ubuntu yang lain
```
echo nameserver 192.168.122.1 > /etc/resolv.conf.
```
- Cek semua node sekarang seharusnya sudah bisa melakukan ping ke google, pada contoh dibawah mencoba ping google di Yudhistira
  
![soal1.1](img/1.1.png)

---
### Soal 2
---
Buatlah website utama pada node arjuna dengan akses ke arjuna.yyy.com dengan alias www.arjuna.yyy.com dengan yyy merupakan kode kelompok.
---
### Jawaban
---
- Buka Yudhistira dan update package lists dengan menjalankan command:
```
apt-get update
```
- Setalah melakukan update silahkan install aplikasi bind9 pada Yudhistira dengan perintah:
```
 apt-get install bind9 -y
```
- Lakukan perintah pada Yudhistira. Isikan seperti berikut:
```
nano /etc/bind/named.conf.local
```
- Isikan configurasi domain arjuna.e23.com sesuai dengan syntax berikut:
```
zone "arjuna.e23.com" {
	type master;
	file "/etc/bind/prak2/arjuna.e23.com";
};
```
- Buat folder `prak2` di dalam `/etc/bind`
```
mkdir /etc/bind/prak2
```
- Copykan file db.local pada path `/etc/bind` ke dalam folder prak2 yang baru saja dibuat dan ubah namanya menjadi arjuna.e23.com
```
cp /etc/bind/db.local /etc/bind/prak2/arjuna.e23.com
```
- Kemudian buka file arjuna.e23.com dan edit seperti gambar berikut dengan IP Yudhistira 
```
nano /etc/bind/prak2/arjuna.e23.com
```

![soal2.0](img/2.0.png)

- Restart bind9 dengan perintah
```
service bind9 restart
```
- Cek dengan melakukan ping www.arjuna.e23.com pada client sadewa
  
![soal2.1](img/2.1.png)

---
### Soal 3
---
Buatlah website utama pada node arjuna dengan akses ke abimanyu.yyy.com dengan alias www.abimanyu.yyy.com dengan yyy merupakan kode kelompok.
---
### Jawaban
---
- Lakukan perintah pada Yudhistira. Isikan seperti berikut:
```
nano /etc/bind/named.conf.local
```
- Isikan configurasi domain abimanyu.e23.com sesuai dengan syntax berikut:
```
zone "abimanyu.e23.com" {
	type master;
	file "/etc/bind/prak2/abimanyu.e23.com";
};
```
- Copykan file db.local pada path `/etc/bind` ke dalam folder prak2 yang baru saja dibuat dan ubah namanya menjadi abimanyu.e23.com
```
cp /etc/bind/db.local /etc/bind/prak2/abimanyu.e23.com
```
- Kemudian buka file abimanyu.e23.com dan edit seperti gambar berikut dengan IP Yudhistira 
```
nano /etc/bind/prak2/abimanyu.e23.com
```

![soal3.0](img/3.0.png)

- Restart bind9 dengan perintah
```
service bind9 restart
```
- Cek dengan melakukan ping www.abimanyu.e23.com pada client sadewa
  
![soal1.1](img/3.1.png)

