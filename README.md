# Jarkom-Modul-2-2025-K60

## Anggota Kelompok

| No | Nama                   | NRP         |
|----|------------------------|-------------|
| 1  | Gemilang Ananda Lingua | 5027241072  |
| 2  | Afriza Tristan Calendra Rajasa     | 5027241106  |

## Topologi
<img width="1710" height="1112" alt="image" src="https://github.com/user-attachments/assets/58251ca9-7c86-4aa4-bfc3-6d4095f3ef8a" />

## Configuration

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

## Setup dan Instalasi
