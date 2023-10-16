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
Buat topologi sesuai dengan soal, yaitu Tambahkan beberapa node ethernet switch dan ubuntu, lalu buat hubungan antar node dan nama-nama dari node disesuaikan dengan ketentuan soal.

![soal1.0](img/1.0.png)

Lakukan konfigurasi pada setiap node

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

Lakukan config berikut agar topologi yang dibuat bisa mengakses jaringan keluar:
- Ketikkan command dibawah ini pada router Pandudewanata
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s [Prefix IP].0.0/16
```
- Lalu cek IP DNS, dengan mengetikkan command dibawah ini pada pandudewanata
```
cat /etc/resolv.conf
```
Hasilnya adalah:
```
nameserver 192.168.122.1
```
- Lalu ketikkan command dibawah ini di node ubuntu yang lain
```
echo nameserver 192.168.122.1 > /etc/resolv.conf.
```
- Cek semua node sekarang seharusnya sudah bisa melakukan ping ke google, pada contoh dibawah mencoba ping google di Yudhistira
![soal1.1](img/1.1.png)

