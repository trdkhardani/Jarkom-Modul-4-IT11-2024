# Jarkom-Modul-4-IT11-2024

## Kelompok IT11
| NRP | Nama |
| ------ | ------ |
| 5027211049 | Tridiktya Hardani Putra |
| 5027221008 | Jeany Aurellia Putri Dewati |

## Daftar isi
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
  - [Tree](#tree)
  - [Pembagian IP](#pembagian-ip)
  - [Testing](#testing)
 
## Implementasi
Kelompok kamu mengimplementasikan `VLSM` menggunakan `GNS3` dan `CIDR` dengan menggunakan `Cisco`

## Topologi
### Topologi GNS3 VLSM
![image](https://github.com/trdkhardani/Jarkom-Modul-4-IT11-2024/assets/115559151/44e394d6-19a5-482c-8e8b-707647a63508)


### Topologi PKT CIDR


## Prefix IP
Kelompok kami menggunakan prefik IP `10.69`
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

## CIDR

### Penggabungan IP

### Tree

### Pembagian IP

### Testing
