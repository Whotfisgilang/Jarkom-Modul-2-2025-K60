# Jarkom-Modul-2-2025-K60

## Anggota Kelompok

| No | Nama                   | NRP         |
|----|------------------------|-------------|
| 1  | Gemilang Ananda Lingua | 5027241072  |
| 2  | Afriza Tristan Calendra Rajasa     | 5027241106  |

# Setup dan Instalasi


## Soal 1
#### Pada soal ini, kita diminta untuk memmbuat topologi dengan tiga jalur, yaitu jalur Barat  untuk Earendil dan Elwing, Jalur Timur untuk Cirdan, Elrond, dan Maglor, serta pelabuhan DMZ bagi Sirion, Tirion, Valmar, Lindon, dan Vingilot. Setelah membuat topologi, kita diminta untuk menetapkan alamat dan default gateway tiap tokoh sesuai glosarium yang sudah diberikan.

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
	  address 192.241.3.3
	  netmask 255.255.255.0
	  gateway 192.241.3.1
- Valmar
  ```bash
  auto eth0
  iface eth0 inet static
	  address 192.241.3.4
	  netmask 255.255.255.0
	  gateway 192.241.3.1
- Lindon
  ```bash
  auto eth0
  iface eth0 inet static
	  address 192.241.3.5
	  netmask 255.255.255.0
	  gateway 192.241.3.1
- Vingilot
  ```bash
  auto eth0
  iface eth0 inet static
	  address 192.241.3.6
	  netmask 255.255.255.0
	  gateway 192.241.3.1

## Soal 2
#### Pada soal ini, kita diminta untuk memastikan jalur WAN router aktif dan NAT meneruskan trafik keluar bagi seluruh alamat internal sehingga host di dalam dapat mencapai layanan di luar menggunakan IP address.

- Agar dapat mengakses jalur WAN tambahkan nameserver di setiap nodes:
```
echo "nameserver 192.168.122.1" > /etc/resolv.conf
```
- Untuk meneruskan jalur WAN ke semua alamat internal, lakukan perintah berikut:
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.241.0.0/16
```
- Untuk melakukan pengujian di setiap alamat internal, lakukan ping google.com
```
ping google.com
```
<img width="953" height="253" alt="image" src="https://github.com/user-attachments/assets/2e9722a1-e085-4391-8137-99256a04eb08" />

## Soal 3
#### Pada soal ini, kami diminta untuk memastikan setiap klien bisa saling berkomunikasi lintas jalur (routing internal via Eonwe berfungsi), dan memastikan setiap host non-router menambahkan resolver 192.168.122.1.

- Agar bisa setiap klien berkomunikasi lintas jalur, cek apakah resolver sudah di tambahkan ke semua nodes
```
cat /etc/resolv.conf
```

- Jika sudah ditambahkan, lakukan ping ke IP yang ingin dituju untuk melakukan pengujian komunikasi lintas jalur
```
ping 192.241.2.2
```
<img width="699" height="250" alt="image" src="https://github.com/user-attachments/assets/bdaf99cf-2113-4a30-b405-926decfcb884" />

## Soal 4
#### Pada soal ini, kita diminta untuk membuat record A untuk ns1.<xxxx>.com dan ns2.<xxxx>.com yang mengarah ke alamat Tirion dan Valmar sesuai glosarium, serta A record apex <xxxx>.com yang mengarah ke alamat Sirion (front door). Lalu, kita diminta untuk aktifkan notify dan allow-transfer ke Valmar, set forwarders ke 192.168.122.1. Di Valmar (ns2/slave) tarik zona <xxxx>.com dari Tirion dan pastikan menjawab authoritative. Pada seluruh host non-router ubah urutan resolver menjadi IP dari ns1.<xxxx>.com → ns2.<xxxx>.com → 192.168.122.1. Verifikasi query ke apex dan hostname layanan dalam zona dijawab melalui ns1/ns2.

- Install server DNS untuk menghubungkannya
```
apt update
apt install bind9 -y
```
- Agar lebih mudah, kami membuat link simbolik agar service named menunjuk ke bind9
```
ln -s /etc/init.d/named /etc/init.d/bind9
```

- Buat file konfigurasi utama BIND9 agar server DNS bisa menerima permintaan dari mana saja dan menereuskan query ke DNS (192.168.122.1)
```
cat <<EOF > /etc/bind/named.conf.options
```
**Lakukan perintah tersebut di nodes Tirion dan Valmar**

### Tirion
- Buat direktori untuk menyimpan file zona DNS untuk domain [k55.com]
```
mkdir -p /etc/bind/k60
```

- Untuk memulai proses pembuatan file teks baru dengan isi yang akan dimasukkan sampai baris EOF, lakukan perintah berikut
```
cat <<EOF > /etc/bind/k60/k60.com
```

- Beri izin server 192.241.3.4 (Valmar) menjadi slave DNS yang menerima pembaruan otomatis
```
cat <<EOF > /etc/bind/named.conf.local
```

- Setiap kali mengubah konfigurasi DNS, lakukan perintah berikut memulai ulang service bind9
```
service bind9 restart
```

- Untuk mengatur DNS resolver sistem menjadi DNS lokal, lakukan perintah berikut
```
echo "nameserver 192.241.3.3" > /etc/resolv.conf 
echo "nameserver 192.241.3.4" >> /etc/resolv.conf 
echo "nameserver 192.168.122.1" >> /etc/resolv.conf
```

- Tes apakah DNS server lokal sudah berjalan dengan benar
```
dig @192.241.3.3 k60.com
```

### Valmar
- Buat direktori untuk menyimpan salinan dari file zona DNS utama
```
mkdir -p /var/lib/bind/k60
```

- Ubah kepemilikan folder menjadi milik user dan grup bind
```
chown bind:bind /var/lib/bind/k60
```

- Tulis konfigurasi zona ke file /etc/bind/named.conf.local
```
cat <<EOF > /etc/bind/named.conf.local
```

- Untuk melihat konfigurasi zona DNS yang dijalankan oleh server BIND9, lakukan perintah berikut
```
cat named.conf.local
```

- Setiap kali mengubah konfigurasi DNS, lakukan perintah berikut memulai ulang service bind9
```
service bind9 restart
```

- Tes apakah DNS server lokal sudah berjalan dengan benar
```
dig @192.241.3.4 k55.com
```

- Lakukan perintah berikut ke semua node
```
echo "nameserver 192.241.3.3" > /etc/resolv.conf
echo "nameserver 192.241.3.4" >> /etc/resolv.conf
echo "nameserver 192.168.122.1" >> /etc/resolv.conf
```

## Soal 5
#### Pada soal ini, kita diminta untuk membuat setiap domain untuk masing masing node sesuai dengan namanya dan assign IP masing-masing node. Lakukan pengecualian untuk node yang bertanggung jawab atas ns1 dan ns2
- Menambahkan domain di masing masing node sesuai dengan namanya dan assign IP di masing masing node
```
cat <<EOF >> /etc/bind/k60/k60.com
```
- Setiap kali mengubah konfigurasi DNS, lakukan perintah berikut memulai ulang service bind9
```
service bind9 restart
```

## Soal 6
#### Pada soal ini, kita diminta untuk memastikan Valmar (ns2) telah menerima salinan zona terbaru dari Tirion (ns1) dan nilai serial SOA di keduanya harus sama
- Memeriksa apakah DNS slave (192.241.3.4) sudah menyalin data dari master (192.241.3.3)

**Tirion**
```
dig @192.241.3.3 k55.com SOA +short
```
**Valmar**
```
dig @192.241.3.4 k55.com SOA +short
```

## Soal 7 
###

