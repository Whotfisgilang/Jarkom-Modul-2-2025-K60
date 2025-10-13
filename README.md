# Jarkom-Modul-2-2025-K60

## Anggota Kelompok

| No | Nama                   | NRP         |
|----|------------------------|-------------|
| 1  | Gemilang Ananda Lingua | 5027241072  |
| 2  | Afriza Tristan Calendra Rajasa     | 5027241106  |

## Setup dan Instalasi


## Soal !
pada soal ini, kita diminta untuk memmbuat topologi dengan tiga jalur, yaitu jalur Barat  untuk Earendil dan Elwing, Jalur Timur untuk Cirdan, Elrond, dan Maglor, serta pelabuhan DMZ bagi Sirion, Tirion, Valmar, Lindon, dan Vingilot. Setelah membuat topologi, kita diminta untuk menetapkan alamat dan default gateway tiap tokoh sesuai glosarium yang sudah diberikan.

**Topologi**
<img width="1710" height="1112" alt="image" src="https://github.com/user-attachments/assets/58251ca9-7c86-4aa4-bfc3-6d4095f3ef8a" />

**Configuration**

- Eonwe
  ```bash
  auto eth0
  iface eth0 inet dhcp

  auto eth1
  iface eth1 inet static
	  address 192.241.1.1
	  netmask 255.255.255.0

  auto eth2
    iface eth2 inet static
	  address 192.241.2.1
	  netmask 255.255.255.0

  auto eth3
  iface eth3 inet static
	  address 192.241.3.1
	  netmask 255.255.255.0
   ```
- Earendil
  ```bash
  auto eth0
  iface eth0 inet static
	  address 192.241.1.2
	  netmask 255.255.255.0
	  gateway 192.241.1.1
  ```
- Elwing
  ```bash
  auto eth0
  iface eth0 inet static
	  address 192.241.1.3
	  netmask 255.255.255.0
	  gateway 192.241.1.1
  ```
- Cirdan
  ```bash
  auto eth0
  iface eth0 inet static
	  address 192.241.2.2
	  netmask 255.255.255.0
	  gateway 192.241.2.1
- Elrond
  ```bash
  auto eth0
  iface eth0 inet static
	  address 192.241.2.3
	  netmask 255.255.255.0
	  gateway 192.241.2.1
- Maglor
  ```bash
  auto eth0
  iface eth0 inet static
	  address 192.241.2.4
	  netmask 255.255.255.0
	  gateway 192.241.2.1
- Sirion
  ```bash
  auto eth0
  iface eth0 inet static
	  address 192.241.3.2
	  netmask 255.255.255.0
	  gateway 192.241.3.1
- Tirion
  ```bash
  auto eth0
  iface eth0 inet static
	  address 192.241.4.2
	  netmask 255.255.255.0
	  gateway 192.241.4.1
- Valmar
  ```bash
  auto eth0
  iface eth0 inet static
	  address 192.241.4.3
	  netmask 255.255.255.0
	  gateway 192.241.4.1
- Lindon
  ```bash
  auto eth0
  iface eth0 inet static
	  address 192.241.4.4
	  netmask 255.255.255.0
	  gateway 192.241.4.1
- Vingilot
  ```bash
  auto eth0
  iface eth0 inet static
	  address 192.241.4.5
	  netmask 255.255.255.0
	  gateway 192.241.4.1

## Soal 2
Pada soal ini, kita diminta untuk memastikan jalur WAN router aktif dan NAT meneruskan trafik keluar bagi seluruh alamat internal sehingga host di dalam dapat mencapai layanan di luar menggunakan IP address.

- Agar dapat mengakses jalur WAN tambahkan di nameserver:
```
nameserver 192.168.122.1
```
- Untuk meneruskan jalur WAN ke semua alamat internal, ketikkan kode berikut:
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.241.0.0/16
```
- Untuk melakukan pengujian di setiap alamat internal, lakukan ping google.com
<img width="953" height="253" alt="image" src="https://github.com/user-attachments/assets/2e9722a1-e085-4391-8137-99256a04eb08" />

## Soal 3
Pada soal ini, kami diminta untuk memastikan setiap klien bisa saling berkomunikasi lintas jalur (routing internal via Eonwe berfungsi), dan memastikan setiap host non-router menambahkan resolver 192.168.122.1.

- Agar bisa setiap klien berkomunikasi lintas jalur, tambahkan nameserver di setiap IP
```
nameserver 192.168.122.1
```

- Untuk melakukan pengujian komunikasi lintas jalur, lakukan ping ke IP yang ingin dituju
<img width="699" height="250" alt="image" src="https://github.com/user-attachments/assets/bdaf99cf-2113-4a30-b405-926decfcb884" />

