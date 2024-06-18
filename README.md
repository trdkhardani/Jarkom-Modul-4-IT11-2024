# Jarkom-Modul-4-IT11-2024

## Kelompok IT11
| NRP | Nama |
| ------ | ------ |
| 5027211049 | Tridiktya Hardani Putra |
| 5027221008 | Jeany Aurellia Putri Dewati |

## Daftar isi
- [Jarkom-Modul-4-IT11-2024](#jarkom-modul-4-it11-2024)
  - [Kelompok IT11](#kelompok-it11)
  - [Daftar isi](#daftar-isi)
  - [Implementasi](#implementasi)
  - [Topologi](#topologi)
    - [Topologi GNS3 VLSM](#topologi-gns3-vlsm)
    - [Topologi PKT CIDR](#topologi-pkt-cidr)
  - [Prefix IP](#prefix-ip)
  - [Rute](#rute)
  - [VLSM](#vlsm)
    - [Tree](#tree)
    - [Pembagian IP](#pembagian-ip)
    - [Konfigurasi Network](#konfigurasi-network)
    - [Routing](#routing)
    - [Testing](#testing)
  - [CIDR](#cidr)
    - [Penggabungan IP](#penggabungan-ip)
    - [Tree](#tree-1)
    - [Pembagian IP](#pembagian-ip-1)
    - [Konfigurasi Network](#konfigurasi-network-1)
      - [A1](#a1)
      - [A2](#a2)
      - [A3](#a3)
      - [A4](#a4)
      - [A5](#a5)
      - [A6](#a6)
      - [A7](#a7)
      - [A8](#a8)
      - [A9](#a9)
      - [A10](#a10)
      - [A11](#a11)
      - [A12](#a12)
      - [A13](#a13)
      - [A14](#a14)
      - [A15](#a15)
      - [A16](#a16)
      - [A17](#a17)
      - [A18](#a18)
      - [A19](#a19)
      - [A20](#a20)
      - [A21](#a21)
    - [Routing](#routing-1)
      - [A1](#a1-1)
      - [A2 \& A3](#a2--a3)
      - [A4 \& A5](#a4--a5)
      - [A6](#a6-1)
      - [A7](#a7-1)
      - [A9 \& A10](#a9--a10)
      - [A11 \& A12](#a11--a12)
      - [A13](#a13-1)
      - [A14](#a14-1)
      - [A15](#a15-1)
      - [A17](#a17-1)
      - [A18](#a18-1)
      - [A19](#a19-1)
      - [A20](#a20-1)
      - [A21](#a21-1)
    - [Testing](#testing-1)
      - [Client-Client](#client-client)
      - [Router-Client (vice versa)](#router-client-vice-versa)
      - [Router-Router](#router-router)
      - [Server-Client (vice versa)](#server-client-vice-versa)
      - [Server-Server](#server-server)
 
## Implementasi
Kelompok kamu mengimplementasikan `VLSM` menggunakan `GNS3` dan `CIDR` dengan menggunakan `Cisco`

## Topologi
### Topologi GNS3 VLSM
![image](https://github.com/trdkhardani/Jarkom-Modul-4-IT11-2024/assets/115559151/44e394d6-19a5-482c-8e8b-707647a63508)


### Topologi PKT CIDR
![image](/images/topologi-cidr.png)

## Prefix IP
Kelompok kami menggunakan prefix IP `10.69`
## Rute
Hasil dari `rute` yang kami dapatkan adalah sebagai berikut
![image](https://github.com/trdkhardani/Jarkom-Modul-4-IT11-2024/assets/115559151/c36f8183-cf36-41d5-badd-f301428d75cf)

## VLSM

### Tree
Berikut merupakan hasil `pemecahan` subnet besar yang dibentuk menjadi `jaringan` yang lebih kecil
![TREE VLSM](https://github.com/trdkhardani/Jarkom-Modul-4-IT11-2024/assets/115559151/a613cfae-6482-469a-8028-446c42f8ca44)

### Pembagian IP
Berikut adalah hasil dari pembagian `IP` yang telah kami peroleh berdasarkan hasil `pemecahan` sebelumnya 
![image](https://github.com/trdkhardani/Jarkom-Modul-4-IT11-2024/assets/115559151/2d08f155-f527-4e86-a2c0-7ae437b7dd9d)

### Konfigurasi Network
- JAWA
  ```
  auto lo
  iface lo inet loopback
  
  auto eth0
  iface eth0 inet dhcp
  
  #A1 > SUMATERA
  auto eth1
  iface eth1 inet static
      address 10.69.21.177
      netmask 255.255.255.252
  
  #A8 > KALIMANTAN
  auto eth2
  iface eth2 inet static
      address 10.69.21.189
      netmask 255.255.255.252
  
  #A16 > SULAWESI
  auto eth3
  iface eth3 inet static
      address 10.69.21.205
      netmask 255.255.255.252
  ```
- SUMATERA
  ```
  auto lo
  iface lo inet loopback
  
  #A1 > JAWA
  auto eth0
  iface eth0 inet static
      address 10.69.21.178
      netmask 255.255.255.252
      gateway 10.69.21.177
  
  #A2 > LAMPUNG
  auto eth1
  iface eth1 inet static
      address 10.69.21.181
      netmask 255.255.255.252
  
  #A4 > SW-TOBA
  auto eth2
  iface eth2 inet static
      address 10.69.21.65
      netmask 255.255.255.224
  ```
- LAMPUNG
  ```
  auto lo
  iface lo inet loopback
  
  #A2 > SUMATERA
  auto eth0
  iface eth0 inet static
      address 10.69.21.182
      netmask 255.255.255.252
      gateway 10.69.21.181
  
  #A3 > SW-BANDAR-LAMPUNG
  auto eth1
  iface eth1 inet static
      address 10.69.19.1
      netmask 255.255.255.0
  ```
- PC-SEBUKU (186 HOST)
  ```
  #A3 > SW-BANDAR-LAMPUNG
  auto eth0
  iface eth0 inet static
      address 10.69.19.2
      netmask 255.255.255.0
      gateway 10.69.19.1
  ```
- SEBESI
  ```
  #A3 > SW-BANDAR-LAMPUNG
  auto eth0
  iface eth0 inet static
      address 10.69.19.3
      netmask 255.255.255.0
      gateway 10.69.19.1
  ```
- PC-SIBANDANG (11 HOST)
  ```
  #A4 > SW-TOBA
  auto eth0
  iface eth0 inet static
      address 10.69.21.66
      netmask 255.255.255.224
      gateway 10.69.21.65
  ```
- PC-SAMOSIR (14 HOST)
  ```
  #A4 > SW-TOBA
  auto eth0
  iface eth0 inet static
      address 10.69.21.67
      netmask 255.255.255.224
      gateway 10.69.21.65
  ```
- SUMATERA-UTARA
  ```
  auto lo
  iface lo inet loopback
  
  #A4 > SW-TOBA
  auto eth0
  iface eth0 inet static
      address 10.69.21.68
      netmask 255.255.255.224
      gateway 10.69.21.65
  
  #A5 > ACEH
  auto eth1
  iface eth1 inet static
      address 10.69.21.185
      netmask 255.255.255.252
  ```
- ACEH
  ```
  auto lo
  iface lo inet loopback
  
  #A5 > SUMATERA-UTARA
  auto eth0
  iface eth0 inet static
      address 10.69.21.186
      netmask 255.255.255.252
      gateway 10.69.21.185
  
  #A6 > SW-BLANGKARAI
  auto eth1
  iface eth1 inet static
      address 10.69.20.1
      netmask 255.255.255.128
  
  #A7 > SW-BANDA-ACEH
  auto eth2
  iface eth2 inet static
      address 10.69.21.129
      netmask 255.255.255.224
  ```
- PC-BERAWAN-TAMPU (53 HOST)
  ```
  #A6 > SW-BLANGKARAL
  auto eth0
  iface eth0 inet static
      address 10.69.20.2
      netmask 255.255.255.128
      gateway 10.69.20.1
  ```
- PC-ENANG-ENANG (27 HOST)
  ```
  #A6 > SW-BLANGKARAL
  auto eth0
  iface eth0 inet static
      address 10.69.20.3
      netmask 255.255.255.128
      gateway 10.69.20.1
  ```
- PC-STARLAND (44 HOST)
  ```
  #A6 > SW-BLANGKARAL
  auto eth0
  iface eth0 inet static
      address 10.69.20.4
      netmask 255.255.255.128
      gateway 10.69.20.1
  ```
- PC-SABANG (6 HOST)
  ```
  #A7 > SW-BANDA-ACEH
  auto eth0
  iface eth0 inet static
      address 10.69.21.130
      netmask 255.255.255.224
      gateway 10.69.21.129
  ```
- PC-LAMBARO (8 HOST)
  ```
  #A7 > SW-BANDA-ACEH
  auto eth0
  iface eth0 inet static
      address 10.69.21.131
      netmask 255.255.255.224
      gateway 10.69.21.129
  ```
- KALIMANTAN
  ```
  auto lo
  iface lo inet loopback
  
  #A8 > JAWA
  auto eth0
  iface eth0 inet static
      address 10.69.21.190
      netmask 255.255.255.252
      gateway 10.69.21.189
  
  #A9 > KALIMANTAN-UTARA
  auto eth1
  iface eth1 inet static
      address 10.69.21.193
      netmask 255.255.255.252
  ```
- KALIMANTAN-UTARA
  ```
  auto lo
  iface lo inet loopback
  
  #A9 > KALIMANTAN
  auto eth0
  iface eth0 inet static
      address 10.69.21.194
      netmask 255.255.255.252
      gateway 10.69.21.193
  
  #A10 > SW-TANJUNG-SELOR
  auto eth1
  iface eth1 inet static
      address 10.69.18.1
      netmask 255.255.255.0
  
  #A11 > KALIMANTAN-TIMUR
  auto eth2
  iface eth2 inet static
      address 10.69.21.197
      netmask 255.255.255.252
  ```
- PC-SELIMAU
  ```
  #A10 > SW-TANJUNG-SELOR
  auto eth0
  iface eth0 inet static
      address 10.69.18.2
      netmask 255.255.255.0
      gateway 10.69.18.1
  ```
- KALIMANTAN-TIMUR
  ```
  auto lo
  iface lo inet loopback
  
  #A11 > KALIMANTAN-UTARA
  auto eth0
  iface eth0 inet static
      address 10.69.21.198
      netmask 255.255.255.252
      gateway 10.69.21.197
  
  #A12 > SW-BALIKPAPAN
  auto eth1
  iface eth1 inet static
      address 10.69.16.1
      netmask 255.255.254.0
  
  #A13 > KALIMANTAN-SELATAN
  auto eth2
  iface eth2 inet static
      address 10.69.21.201
      netmask 255.255.255.252
  ```
- BANGKIRAI
  ```
  #A12 > SW-BALIKPAPAN
  auto eth0
  iface eth0 inet static
      address 10.69.16.2
      netmask 255.255.254.0
      gateway 10.69.16.1
  ```
- PC-LAMARU (468 HOST)
  ```
  #A12 > SW-BALIKPAPAN
  auto eth0
  iface eth0 inet static
      address 10.69.16.3
      netmask 255.255.254.0
      gateway 10.69.16.1
  ```
- KALIMANTAN-SELATAN
  ```
  auto lo
  iface lo inet loopback
  
  #A13 > KALIMANTAN-TIMUR
  auto eth0
  iface eth0 inet static
      address 10.69.21.202
      netmask 255.255.255.252
      gateway 10.69.21.201
  
  #A14 > SW-BOENATI
  auto eth1
  iface eth1 inet static
      address 10.69.21.97
      netmask 255.255.255.224
  
  #A13 > SW-BANJARMASIN
  auto eth2
  iface eth2 inet static
      address 10.69.0.1
      netmask 255.255.248.0
  ```
- PC-ANGSANA (15 HOST)
  ```
  #A14 > KALIMANTAN-SELATAN
  auto eth0
  iface eth0 inet static
      address 10.69.21.98
      netmask 255.255.255.224
      gateway 10.69.21.97
  ```
- PC-BAJUIN (511 HOST)
  ```
  #A15 > SW-BANJARMASIN
  auto eth0
  iface eth0 inet static
      address 10.69.0.2
      netmask 255.255.248.0
      gateway 10.69.0.1
  ```
- PC-TAKISUNG (513 HOST)
  ```
  #A15 > SW-BANJARMASIN
  auto eth0
  iface eth0 inet static
      address 10.69.0.3
      netmask 255.255.248.0
      gateway 10.69.0.1
  ```
- PC-BATAKAN 1020 HOST)
  ```
  #A15 > SW-BANJARMASIN
  auto eth0
  iface eth0 inet static
      address 10.69.0.4
      netmask 255.255.248.0
      gateway 10.69.0.1
  ```
- SULAWESI
  ```
  auto lo
  iface lo inet loopback
  
  #A16 > JAWA
  auto eth0
  iface eth0 inet static
      address 10.69.21.206
      netmask 255.255.255.252
      gateway 10.69.21.205
  
  #A17 > SW-SULSEL
  auto eth1
  iface eth1 inet static
      address 10.69.21.161
      netmask 255.255.255.248
  
  #A18 > SW-GORONTALO
  auto eth2
  iface eth2 inet static
      address 10.69.20.129
      netmask 255.255.255.128
  ```
- MAKASAR
  ```
  auto lo
  iface lo inet loopback
  
  #A17 > SULAWESI
  auto eth0
  iface eth0 inet static
      address 10.69.21.162
      netmask 255.255.255.248
      gateway 10.69.21.161
  
  #A18 > SW-LIMBUNG
  auto eth1
  iface eth1 inet static
      address 10.69.21.169
      netmask 255.255.255.248
  ```
- TOPEJAWA-TAKALAR
  ```
  #A18 > SW-LIMBUNG
  auto eth0
  iface eth0 inet static
      address 10.69.21.170
      netmask 255.255.255.252
      gateway 10.69.21.169
  ```
- GALESONG
  ```
  #A18 > SW-LIMBUNG
  auto eth0
  iface eth0 inet static
      address 10.69.21.171
      netmask 255.255.255.252
      gateway 10.69.21.169
  ```
- BELAWA
  ```
  auto lo
  iface lo inet loopback
  
  #A17 > SW-SULSEL
  auto eth0
  iface eth0 inet static
      address 10.69.21.163
      netmask 255.255.255.248
      gateway 10.69.21.161
  
  #A18 > SW-TEMPE
  auto eth1
  iface eth1 inet static
      address 10.69.21.1
      netmask 255.255.255.192
  ```
- PC-BARU (30 HOST)
  ```
  #A18 > SW-TEMPE
  auto eth0
  iface eth0 inet static
      address 10.69.21.2
      netmask 255.255.255.192
      gateway 10.69.21.1
  ```
- PC-MADINI (30 HOST)
  ```
  #A18 > SW-TEMPE
  auto eth0
  iface eth0 inet static
      address 10.69.21.3
      netmask 255.255.255.192
      gateway 10.69.21.1
  ```
- PC-MARISA (30 HOST)
  ```
  #A20 > SULAWESI
  auto eth0
  iface eth0 inet static
      address 10.69.20.130
      netmask 255.255.255.128
      gateway 10.69.20.129
  ```
- PC-GORONTALO (30 HOST)
  ```
  #A20 > SULAWESI
  auto eth0
  iface eth0 inet static
      address 10.69.20.131
      netmask 255.255.255.128
      gateway 10.69.20.129
  ```
- MALUKU-UTARA
  ```
  auto lo
  iface lo inet loopback
  
  #A20> SW-GORONTALO
  auto eth0
  iface eth0 inet static
      address 10.69.20.130
      netmask 255.255.255.128
      gateway 10.69.20.129
  
  #A21 > SW-MALUKU
  auto eth1
  iface eth1 inet static
      address 10.69.8.1
      netmask 255.255.248.0
  ```
- PC-TERNATE (511 HOST)
  ```
  #A21 > SW-MALUKU
  auto eth0
  iface eth0 inet static
      address 10.69.8.2
      netmask 255.255.248.0
      gateway 10.69.8.1
  ```
- MOROTAI
  ```
  #A21 > SW-MALUKU
  auto eth0
  iface eth0 inet static
      address 10.69.8.3
      netmask 255.255.248.0
      gateway 10.69.8.1
  ```
- PC-TOBETO (511 HOST)
  ```
  #A21 > SW-MALUKU
  auto eth0
  iface eth0 inet static
      address 10.69.8.4
      netmask 255.255.248.0
      gateway 10.69.8.1
  ```
### Routing
- ACEH
  ```
  #KE SUMATERA UTARA
  route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.69.21.185
  ```
- LAMPUNG
  ```
  #KE SUMATERA
  route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.69.21.181
  ```
- KALIMANTAN-SELATAN
  ```
  #KE KALIMANTAN-TIMUR
  route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.69.21.201
  ```
- MAKASAR
  ```
  #KE SULAWESI
  route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.69.21.161
  ```
- BELAWA
  ```
  #KE SULAWESI
  route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.69.21.161
  ```
- MALUKU-UTARA
  ```
  #KE SULAWESI
  route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.69.20.129
  ```
- SUMATERA-UTARA
  ```
  route add -net 10.69.20.0 netmask 255.255.255.128 gw 10.69.21.186 #SW-BLANGKARAI
  route add -net 10.69.21.128 netmask 255.255.255.224 gw 10.69.21.186 #SW-BANDA-ACEH
  ```
- SUMATERA
  ```
  #KE SUMATERA-UTARA
  route add -net 10.69.21.184 netmask 255.255.255.252 gw 10.69.21.68
  route add -net 10.69.20.0 netmask 255.255.255.128 gw 10.69.21.68
  route add -net 10.69.21.128 netmask 255.255.255.224 gw 10.69.21.68
  
  #KE LAMPUNG
  route add -net 10.69.19.0 netmask 255.255.255.0 gw 10.69.21.182
  ```
- KALIMANTAN-TIMUR
  ```
  route add -net 10.69.21.96 netmask 255.255.255.224 gw 10.69.21.202
  route add -net 10.69.0.0 netmask 255.255.248.0 gw 10.69.21.202
  ```
- KALIMANTAN-UTARA
  ```
  route add -net 10.69.16.0 netmask 255.255.254.0 gw 10.69.21.198
  route add -net 10.69.21.200 netmask 255.255.255.252 gw 10.69.21.198
  route add -net 10.69.21.96 netmask 255.255.255.224 gw 10.69.21.198
  route add -net 10.69.0.0 netmask 255.255.248.0 gw 10.69.21.198
  ```
- KALIMANTAN
  ```
  route add -net 10.69.18.0 netmask 255.255.255.0 gw 10.69.21.194
  route add -net 10.69.21.196 netmask 255.255.255.252 gw 10.69.21.194
  route add -net 10.69.16.0 netmask 255.255.254.0 gw 10.69.21.194
  route add -net 10.69.21.200 netmask 255.255.255.252 gw 10.69.21.194
  route add -net 10.69.21.96 netmask 255.255.255.224 gw 10.69.21.194
  route add -net 10.69.0.0 netmask 255.255.248.0 gw 10.69.21.194
  ```
- SULAWESI
  ```
  #KE MALUKU-UTARA
  route add -net 10.69.8.0 netmask 255.255.248.0 gw 10.69.20.130
  
  #KE MAKASAR
  route add -net 10.69.21.168 netmask 255.255.255.248 gw 10.69.21.162
  
  #KE BELAWA
  route add -net 10.69.21.0 netmask 255.255.255.192 gw 10.69.21.163
  ```
- JAWA
  ```
  #arah ke SUMATERA, eth0 ip SUMATERA A1-A4
  route add -net 10.69.21.180 netmask 255.255.255.252 gw 10.69.21.178
  route add -net 10.69.19.0 netmask 255.255.255.0 gw 10.69.21.178
  route add -net 10.69.21.64 netmask 255.255.255.224 gw 10.69.21.178
  route add -net 10.69.21.184 netmask 255.255.255.252 gw 10.69.21.178
  route add -net 10.69.20.0 netmask 255.255.255.128 gw 10.69.21.178
  route add -net 10.69.21.128 netmask 255.255.255.224 gw 10.69.21.178
  
  #Ke arah KALIMANTAN, eth0 ip KALIMANTAN A8-A15
  route add -net 10.69.21.192 netmask 255.255.255.252 gw 10.69.21.190
  route add -net 10.69.18.0 netmask 255.255.255.0 gw 10.69.21.190
  route add -net 10.69.21.196 netmask 255.255.255.252 gw 10.69.21.190
  route add -net 10.69.16.0 netmask 255.255.254.0 gw 10.69.21.190
  route add -net 10.69.21.200 netmask 255.255.255.252 gw 10.69.21.190
  route add -net 10.69.21.96 netmask 255.255.255.224 gw 10.69.21.190
  route add -net 10.69.0.0 netmask 255.255.248.0 gw 10.69.21.190
  
  #Ke arah SULAWESI eth0 ip SULAWESI A16,A17,A20
  route add -net 10.69.21.160 netmask 255.255.255.248 gw 10.69.21.206
  route add -net 10.69.21.168 netmask 255.255.255.248 gw 10.69.21.206
  route add -net 10.69.21.0 netmask 255.255.255.192 gw 10.69.21.206
  route add -net 10.69.20.128 netmask 255.255.255.128 gw 10.69.21.206
  route add -net 10.69.8.0 netmask 255.255.248.0 gw 10.69.21.206
  ```
### Testing

https://github.com/trdkhardani/Jarkom-Modul-4-IT11-2024/assets/115559151/0e26743b-7008-4a9d-89d4-8191fcb4cbc7

## CIDR

### Penggabungan IP
Berikut merupakan hasil `penggabungan` subnet yang telah kami lakukan

![image](/images/penggabungan-cidr_1.png)

![image](/images/penggabungan-cidr_2.png)

![image](/images/penggabungan-cidr_3.png)

### Tree
Berikut merupakan hasil `pemecahan` subnet besar yang dibentuk menjadi `jaringan` yang lebih kecil

![image](/images/CIDR%20Tree.png)

### Pembagian IP
Berikut adalah hasil dari pembagian `IP` yang telah kami peroleh berdasarkan hasil `pemecahan` sebelumnya

![image](/images/pembagian-cidr.png)

### Konfigurasi Network
**Note: Setiap setelah melakukan konfigurasi, jangan lupa menghidupkan port (khusus Router).**

![image](/images/turn-on-port.png)

#### A1
JAWA (Router)
```
Fa1/1
IPv4 Address: 10.69.196.33 
Subnet Mask: 255.255.255.252
```

SUMATERA (Router)
```
Fa0/0
IPv4 Address: 10.69.196.34
Subnet Mask: 255.255.255.252
```

#### A2
SUMATERA (Router)
```
Fa1/0
IPv4 Address: 10.69.67.1
Subnet Mask: 255.255.255.252
```

LAMPUNG (Router)
```
Fa0/0
IPv4 Address: 10.69.67.2
Subnet Mask: 255.255.255.252
```

#### A3
LAMPUNG (Router)
```
Fa0/1
IPv4 Address: 10.69.66.1
Subnet Mask: 255.255.255.0
```

Sebuku (Client)
```
Fa0
IPv4 Address: 10.69.66.2
Gateway: 10.69.66.1
Subnet Mask: 255.255.255.0
```

Sebesi (Server)
```
Fa0
IPv4 Address: 10.69.66.3
Gateway: 10.69.66.1
Subnet Mask: 255.255.255.0
```

#### A4
SUMATERA (Router)
```
Fa0/1
IPv4 Address: 10.69.196.1
Subnet Mask: 255.255.255.224
```

SUMATERA-UTARA (Router)
```
Fa0/0
IPv4 Address: 10.69.196.2
Subnet Mask: 255.255.255.224
```

Samosir (Client)
```
Fa0
IPv4 Address: 10.69.196.3
Gateway: 10.69.196.1
Subnet Mask: 255.255.255.224
```

Sibandang (Client)
```
Fa0
IPv4 Address: 10.69.196.4
Gateway: 10.69.196.1
Subnet Mask: 255.255.255.224
```

#### A5
SUMATERA-UTARA (Router)
```
Fa0/1
IPv4 Address: 10.69.65.1
Subnet Mask: 255.255.255.252
```

ACEH (Router)
```
Fa0/0
IPv4 Address: 10.69.65.2
Subnet Mask: 255.255.255.252
```

#### A6
ACEH (Router)
```
Fa0/1
IPv4 Address: 10.69.64.1
Subnet Mask: 255.255.255.128
```

Berawan-Tampu (Client)
```
Fa0
IPv4 Address: 10.69.64.2
Gateway: 10.69.64.1
Subnet Mask: 255.255.255.128
```

Starland (Client)
```
Fa0
IPv4 Address: 10.69.64.3
Gateway: 10.69.64.1
Subnet Mask: 255.255.255.128
```

Enang-Enang (Client)
```
Fa0
IPv4 Address: 10.69.64.4
Gateway: 10.69.64.1
Subnet Mask: 255.255.255.128
```

#### A7
ACEH (Router)
```
Fa1/0
IPv4 Address: 10.69.64.129
Subnet Mask: 255.255.255.128
```

Lambaro (Client)
```
Fa0
IPv4 Address: 10.69.64.130
Gateway: 10.69.64.129
Subnet Mask: 255.255.255.128
```

Sabang (Client)
```
Fa0
IPv4 Address: 10.69.64.131
Gateway: 10.69.64.129
Subnet Mask: 255.255.255.128
```

#### A8
JAWA (Router)
```
Fa1/0
IPv4 Address: 10.69.194.1
Subnet Mask: 255.255.255.252
```

KALIMANTAN (Router)
```
Fa0/0
IPv4 Address: 10.69.194.2
Subnet Mask: 255.255.255.252
```

#### A9
KALIMANTAN (Router)
```
Fa0/1
IPv4 Address: 10.69.193.1
Subnet Mask: 255.255.255.252
```

KALIMANTAN-UTARA (Router)
```
Fa0/0
IPv4 Address: 10.69.193.2
Subnet Mask: 255.255.255.252
```

#### A10
KALIMANTAN-UTARA (Router)
```
Fa0/1
IPv4 Address: 10.69.192.1
Subnet Mask: 255.255.255.0
```

Selimau (Client)
```
Fa0
IPv4 Address: 10.69.192.2
Gateway: 10.69.192.1
Subnet Mask: 255.255.255.0
```

#### A11
KALIMANTAN-UTARA (Router)
```
Fa1/0
IPv4 Address: 10.69.34.1
Subnet Mask: 255.255.255.252
```

KALIMANTAN-TIMUR (Router)
```
Fa0/0
IPv4 Address: 10.69.34.2
Subnet Mask: 255.255.255.252
```

#### A12
KALIMANTAN-TIMUR (Router)
```
Fa0/1
IPv4 Address: 10.69.32.1
Subnet Mask: 255.255.254.0
```

Lamaru (Client)
```
Fa0
IPv4 Address: 10.69.32.2
Gateway: 10.69.32.1
Subnet Mask: 255.255.254.0
```

Bangkirai (Server)
```
Fa0
IPv4 Address: 10.69.32.3
Gateway: 10.69.32.1
Subnet Mask: 255.255.254.0
```

#### A13
KALIMANTAN-TIMUR (Router)
```
Fa1/0
IPv4 Address: 10.69.16.1
Subnet Mask: 255.255.255.252
```

KALIMANTAN-SELATAN (Router)
```
Fa0/1
IPv4 Address: 10.69.16.2
Gateway: 10.69.16.1
Subnet Mask: 255.255.255.252
```

#### A14
KALIMANTAN-SELATAN (Router)
```
Fa0/0
IPv4 Address: 10.69.8.1
Subnet Mask: 255.255.255.224
```

Angsana (Client)
```
Fa0
IPv4 Address: 10.69.8.2
Gateway: 10.69.8.1
Subnet Mask: 255.255.255.224
```

#### A15
KALIMANTAN-SELATAN (Router)
```
Fa1/0
IPv4 Address: 10.69.0.1
Subnet Mask: 255.255.248.0
```

Batakan (Client)
```
Fa0
IPv4 Address: 10.69.0.2
Gateway: 10.69.0.1
Subnet Mask: 255.255.248.0
```

Takisung (Client)
```
Fa0
IPv4 Address: 10.69.0.3
Gateway: 10.69.0.1
Subnet Mask: 255.255.248.0
```

Bajuin (Client)
```
Fa0
IPv4 Address: 10.69.0.4
Gateway: 10.69.0.1
Subnet Mask: 255.255.248.0
```

#### A16
JAWA (Router)
```
Fa0/1
IPv4 Address: 10.69.144.1
Subnet Mask: 255.255.255.252
```

SULAWESI (Router)
```
Fa0/0
IPv4 Address: 10.69.144.2
Subnet Mask: 255.255.255.252
```

#### A17
SULAWESI (Router)
```
Fa1/0
IPv4 Address: 10.69.160.65
Subnet Mask: 255.255.255.248
```

BELAWA (Router)
```
Fa0/0
IPv4 Address: 10.69.160.66
Subnet Mask: 255.255.255.248
```

MAKASAR (Router)
```
Fa0/1
IPv4 Address: 10.69.160.67
Subnet Mask: 255.255.255.248
```

#### A18
MAKASAR (Router)
```
Fa0/0
IPv4 Address: 10.69.160.129
Subnet Mask: 255.255.255.248
```

Galesong (Server)
```
Fa0
IPv4 Address: 10.69.160.130
Gateway: 10.69.160.129
Subnet Mask: 255.255.255.248
```

Topejawa-Takalar (Server)
```
Fa0
IPv4 Address: 10.69.160.131
Gateway: 10.69.160.129
Subnet Mask: 255.255.255.248
```

#### A19
MAKASAR (Router)
```
Fa0/1
IPv4 Address: 10.69.160.1
Subnet Mask: 255.255.255.192
```

Madini (Client)
```
Fa0
IPv4 Address: 10.69.160.2
Gateway: 10.69.160.1
Subnet Mask: 255.255.255.192
```

Baru (Client)
```
Fa0
IPv4 Address: 10.69.160.3
Gateway: 10.69.160.1
Subnet Mask: 255.255.255.192
```

#### A20
SULAWESI (Router)
```
Fa0/1
IPv4 Address: 10.69.136.1
Subnet Mask: 255.255.255.128
```

PC-Gorontalo (Client)
```
Fa0
IPv4 Address: 10.69.136.2
Gateway: 10.69.136.1
Subnet Mask: 255.255.255.128
```

PC-Marisa (Client)
```
Fa0
IPv4 Address: 10.69.136.3
Gateway: 10.69.136.1
Subnet Mask: 255.255.255.128
```

MALUKU-UTARA (Router)
```
Fa0/0
IPv4 Address: 10.69.136.4
Subnet Mask: 255.255.255.128
```

#### A21
MALUKU-UTARA (Router)
```
Fa0/1
IPv4 Address: 10.69.128.1
Subnet Mask: 255.255.248.0
```

Tobelo (Client)
```
Fa0
IPv4 Address: 10.69.128.2
Gateway: 10.69.128.1
Subnet Mask: 255.255.248.0
```

Ternate (Client)
```
Fa0
IPv4 Address: 10.69.128.3
Gateway: 10.69.128.1
Subnet Mask: 255.255.248.0
```

Morotai (Server)
```
Fa0/0
IPv4 Address: 10.69.128.4
Gateway: 10.69.128.1
Subnet Mask: 255.255.248.0
```

### Routing
#### A1
ACEH (Ke JAWA A1)
```
Network: 10.69.196.32
Netmask: 255.255.255.252
Next Hop: 10.69.65.1
```

#### A2 & A3
SUMATERA
```
Network: 10.69.66.0
Netmask: 255.255.255.0
Next Hop: 10.69.67.2
```

LAMPUNG
```
Network: 0.0.0.0
Netmask: 0.0.0.0
Next Hop: 10.69.67.1
```

ACEH (Ke LAMPUNG A2)
```
Network: 10.69.67.0
Netmask: 255.255.255.252
Next Hop: 10.69.65.1
```

ACEH (Ke LAMPUNG A3)
```
Network: 10.69.66.0
Netmask: 255.255.255.0
Next Hop: 10.69.65.1
```

SUMATERA-UTARA (Ke LAMPUNG A3)
```
Network: 10.69.66.0
Netmask: 255.255.255.0
Next Hop: 10.69.196.1
```

JAWA
```
Network: 10.69.66.0
Netmask: 255.255.255.0
Next Hop: 10.69.196.34
```

#### A4 & A5
JAWA
```
Network: 10.69.196.0
Netmask: 255.255.255.224
Next Hop: 10.69.196.34
```

SUMATERA
```
Network: 0.0.0.0
Netmask: 0.0.0.0
Next Hop: 10.69.196.33
```

SUMATERA-UTARA (Ke LAMPUNG A2)
```
Network: 10.69.67.0
Netmask: 255.255.255.252
Next Hop: 10.69.196.1
```

SUMATERA-UTARA (Ke JAWA A1)
```
Network: 10.69.196.32
Netmask: 255.255.255.252
Next Hop: 10.69.196.1
```

ACEH (Ke SUMATERA A4)
```
Network: 10.69.196.0
Netmask: 255.255.255.224
Next Hop: 10.69.65.1
```

SUMATERA (Ke ACEH A5)
```
Network: 10.69.65.0
Netmask: 255.255.255.252
Next Hop: 10.69.196.2
```

LAMPUNG (Ke ACEH A5)
```
Network: 10.69.65.0
Netmask: 255.255.255.252
Next Hop: 10.69.67.1
```

JAWA (Ke ACEH A5)
```
Network: 10.69.65.0
Netmask: 255.255.255.252
Next Hop: 10.69.196.34
```

#### A6
SUMATERA-UTARA
```
Network: 10.69.64.0
Netmask: 255.255.255.128
Next Hop: 10.69.65.2
```

ACEH
```
Network: 0.0.0.0
Netmask: 0.0.0.0
Next Hop: 10.69.65.1
```

SUMATERA (Ke ACEH A6)
```
Network: 10.69.64.0
Netmask: 255.255.255.128
Next Hop: 10.69.196.2
```

LAMPUNG (Ke ACEH A6)
```
Network: 10.69.64.0
Netmask: 255.255.255.128
Next Hop: 10.69.67.1
```

JAWA (Ke ACEH A6)
```
Network: 10.69.64.0
Netmask: 255.255.255.128
Next Hop: 10.69.196.34
```

#### A7
SUMATERA-UTARA
```
Network: 10.69.64.128
Netmask: 255.255.255.224
Next Hop: 10.69.65.2
```

ACEH
```
Network: 0.0.0.0
Netmask: 0.0.0.0
Next Hop: 10.69.65.1
```

SUMATERA (Ke ACEH A7)
```
Network: 10.69.64.128
Netmask: 255.255.255.224
Next Hop: 10.69.196.2
```

JAWA (Ke ACEH A7)
```
Network: 10.69.64.128
Netmask: 255.255.255.224
Next Hop: 10.69.196.34
```

#### A9 & A10
KALIMANTAN
```
Network: 10.69.192.0
Netmask: 255.255.255.0
Next Hop: 10.69.193.2
```

KALIMANTAN (Ke JAWA)
```
Network: 0.0.0.0
Netmask: 0.0.0.0
Next Hop: 10.69.194.1
```

KALIMANTAN (Ke KALIMANTAN-TIMUR A11)
```
Network: 10.69.192.0
Netmask: 255.255.255.0
Next Hop: 10.69.193.2
```

KALIMANTAN (Ke KALIMANTAN-SELATAN A13)
```
Network: 10.69.16.0
Netmask: 255.255.255.252
Next Hop: 10.69.193.2
```

KALIMANTAN (Ke KALIMANTAN-TIMUR A12)
```
Network: 10.69.32.0
Netmask: 255.255.254.0
Next Hop: 10.69.193.2
```

KALIMANTAN-UTARA (Ke JAWA via KALIMANTAN)
```
Network: 0.0.0.0
Netmask: 0.0.0.0
Next Hop: 10.69.193.1
```

KALIMANTAN-UTARA (Ke KALIMANTAN-SELATAN A14)
```
Network: 10.69.8.0
Netmask: 255.255.255.224
Next Hop: 10.69.34.2
```

KALIMANTAN-UTARA (Ke KALIMANTAN-SELATAN A15)
```
Network: 10.69.0.0
Netmask: 255.255.248.0
Next Hop: 10.69.34.2
```

KALIMANTAN-UTARA (Ke KALIMANTAN-SELATAN A13)
```
Network: 10.69.16.0
Netmask: 255.255.248.0
Next Hop: 10.69.34.2
```

JAWA (Ke KALIMANTAN-UTARA A10)
```
Network: 10.69.192.0
Netmask: 255.255.255.0
Next Hop: 10.69.194.2
```

#### A11 & A12
KALIMANTAN-UTARA
```
Network: 10.69.32.0
Netmask: 255.255.254.0
Next Hop: 10.69.34.2
```

KALIMANTAN-TIMUR
```
Network: 0.0.0.0
Netmask: 0.0.0.0
Next Hop: 10.69.34.1
```

JAWA (Ke KALIMANTAN-TIMUR A12)
```
Network: 10.69.32.0
Netmask: 255.255.254.0
Next Hop: 10.69.194.2
```

JAWA (Ke KALIMANTAN-TIMUR A11)
```
Network: 10.69.34.0
Netmask: 255.255.255.252
Next Hop: 10.69.194.2
```

#### A13
JAWA (Ke KALIMANTAN-SELATAN A13)
```
Network: 10.69.16.0
Netmask: 255.255.255.252
Next Hop: 10.69.194.2
```

#### A14
KALIMANTAN-TIMUR
```
Network: 10.69.8.0
Netmask: 255.255.255.224
Next Hop: 10.69.16.2
```

KALIMANTAN-SELATAN
```
Network: 0.0.0.0
Netmask: 0.0.0.0
Next Hop: 10.69.16.1
```

KALIMANTAN (Ke KALIMANTAN-SELATAN A14)
```
Network: 10.69.8.0
Netmask: 255.255.255.224
Next Hop: 10.69.193.2
```

JAWA (Ke KALIMANTAN-SELATAN A14)
```
Network: 10.69.8.0
Netmask: 255.255.255.224
Next Hop: 10.69.194.2
```

#### A15
KALIMANTAN-TIMUR
```
Network: 10.69.0.0
Netmask: 255.255.248.0
Next Hop: 10.69.16.2
```

KALIMANTAN-SELATAN
```
Network: 0.0.0.0
Netmask: 0.0.0.0
Next Hop: 10.69.16.1
```

KALIMANTAN (Ke KALIMANTAN-SELATAN A15)
```
Network: 10.69.0.0
Netmask: 255.255.248.0
Next Hop: 10.69.193.2
```

JAWA (Ke KALIMANTAN-SELATAN A15)
```
Network: 10.69.0.0
Netmask: 255.255.248.0
Next Hop: 10.69.194.2
```

#### A17
JAWA (Ke SULAWESI A17)
```
Network: 10.69.160.64
Netmask: 255.255.255.248
Next Hop: 10.69.144.2
```

#### A18
SULAWESI
```
Network: 10.69.160.128
Netmask: 255.255.255.248
Next Hop: 10.69.160.67
```

MAKASAR
```
Network: 0.0.0.0
Netmask: 0.0.0.0
Next Hop: 10.69.160.65
```

JAWA (Ke MAKASAR A18)
```
Network: 10.69.160.128
Netmask: 255.255.255.248
Next Hop: 10.69.144.2
```

#### A19
MAKASAR
```
Network: 10.69.160.0
Netmask: 255.255.255.192
Next Hop: 10.69.160.66
```

BELAWA
```
Network: 0.0.0.0
Netmask: 0.0.0.0
Next Hop: 10.69.160.67
```

JAWA (Ke BELAWA A19)
```
Network: 10.69.160.0
Netmask: 255.255.255.192
Next Hop: 10.69.144.2
```

#### A20
BELAWA
```
Network: 10.69.136.0
Netmask: 255.255.255.128
Next Hop: 10.69.160.65
```

SULAWESI
```
Network: 0.0.0.0
Netmask: 0.0.0.0
Next Hop: 10.69.160.66
```

JAWA (Ke SULAWESI A20)
```
Network: 10.69.136.0
Netmask: 255.255.255.128
Next Hop: 10.69.144.1
```

SULAWESI (Ke JAWA A16)
```
Network: 0.0.0.0
Netmask: 0.0.0.0
Next Hop: 10.69.144.1
```

#### A21
SULAWESI
```
Network: 10.69.128.0
Netmask: 255.255.248.0
Next Hop: 10.69.136.4
```

MALUKU-UTARA
```
Network: 0.0.0.0
Netmask: 0.0.0.0
Next Hop: 10.69.136.1
```

JAWA (Ke MALUKU-UTARA A21)
```
Network: 10.69.128.0
Netmask: 255.255.248.0
Next Hop: 10.69.144.2
```

### Testing
#### Client-Client
![image](/images/client-client.png)

#### Router-Client (vice versa)
![image](/images/router-client.png)

#### Router-Router
![image](/images/router-router.png)

#### Server-Client (vice versa)
![image](/images/server-client.png)

#### Server-Server
![image](/images/server-server.png)