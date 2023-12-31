# Laporan Resmi

# Kelompok A19:
| Nama | NRP |
| ---------------------- | ---------- |
| Nayya Kamila Putri Y | 5025211183 |
| Javier Nararya Aqsa Setiyono | 5025211245 |

## Pembagian Subnet dan Topologi

![subnet](image/subnet.png)

- Richter adalah DNS Server

- Revolte adalah DHCP Server

- Sein dan Stark adalah Web Server

- Jumlah Host pada TurkRegion adalah 1022

- Jumlah Host pada LaubHills adalah 255

- Jumlah Host pada SchwerMountain adalah 64

- Jumlah Host pada GrobeForest adalah 512

## VLSM

| Subnet | Jumlah IP | Netmask |
| ---------------------- | ---------- | ---------- |
| A1 | 2 | /30 |
| A2 | 2 | /30 |
| A3 | 66 | /25 |
| A4 | 256 | /24 |
| A5 | 2 | /30 |
| A6 | 2 | /30 |
| A7 | 2 | /30 |
| A8 | 2 | /30 |
| A9 | 1023 | /21 |
| A10 | 514 | /22 |
| Total | 1871 | /20 |

## Tree
![tree](image/tree.png)

Subnet besar yang dibuat memiliki alamat jaringan (NID) 192.178.0.0 dengan netmask /20. 
Dalam konsep VLSM, subnetting dilakukan dengan menurunkan panjang netmask ke bagian atasnya. 
Dalam hal ini, netmask /20 akan diturunkan menjadi /21, dan pengalokasian alamat IP akan mengikuti 
tabel yang disediakan. Proses dilakukan dengan mengalokasikan subnet yang tersedia sebelumnya untuk 
subnet yang membutuhkan alamat IP. Langkah-langkah ini diulang secara berulang hingga seluruh subnet 
telah dialokasikan dengan benar.

## Subnet dan IP
Kemudian, akan disesuaikan pengalokasian alamat IP sesuai dengan subdivisi subnet yang telah ditentukan 
berdasarkan struktur pohon pada topologi yang diberikan. Selanjutnya, setiap node akan diberikan rentang 
alamat IP yang telah ditentukan sesuai dengan subnetnya untuk diimplementasikan dalam jaringan.

![ip](image/ip.png)

# Konfigurasi Router dan IP
## Konfigurasi ETH

- Revolte
```
auto eth0
iface eth0 inet static
	address 192.178.0.2
	netmask 255.255.255.252
	gateway 192.178.1
	up echo nameserver 192.178.0.6 > /etc/resolv.conf
```

- Richter
```
auto eth0
iface eth0 inet static
	address 192.178.0.6
	netmask 255.255.255.252
	gateway 192.178.0.5
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- Fern
```
# Static config for eth0
auto eth0
iface eth0 inet static
	address 192.178.0.130
	netmask 255.255.255.128
	gateway 192.178.0.129
	up echo nameserver 192.178.0.6 > /etc/resolv.conf


# Static config for eth1
auto eth1
iface eth1 inet static
	address 192.178.0.5
	netmask 255.255.255.252


# Static config for eth2
auto eth2
iface eth2 inet static
	address 192.178.0.1
	netmask 255.255.255.252
```

- SchewerMountain dan LaubHills
```
auto eth0
iface eth0 inet dhcp
```

- Himmel
```
# Static config for eth0
auto eth0
iface eth0 inet static
         address 192.178.0.10
         netmask 255.255.255.252
         gateway 192.178.0.9
	 up echo nameserver 192.178.0.6 > /etc/resolv.conf

auto eth1
iface eth1 inet static
         address 192.178.0.129
         netmask 255.255.255.128

auto eth2
iface eth2 inet static
         address 192.178.1.1
         netmask 255.255.255.0
```

- Frieren
```
auto eth0
iface eth0 inet static
         address 192.178.0.18
         netmask 255.255.255.252
         gateway 192.178.0.17
	 up echo nameserver 192.178.0.6 > /etc/resolv.conf

auto eth1
iface eth1 inet static
         address 192.178.0.13
         netmask 255.255.255.252

auto eth2
iface eth2 inet static
         address 192.178.0.9
         netmask 255.255.255.252
```

- Stark
```
# Static config for eth0
auto eth0
iface eth0 inet static
         address 192.178.0.14
         netmask 255.255.255.252
         gateway 192.178.0.13
	 up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

- Aura
```
auto eth0
iface eth0 inet static
    address 192.168.122.14
    netmask 255.255.255.0
    gateway 192.168.122.1

auto eth2
iface eth2 inet static
       address 192.178.0.17
       netmask 255.255.255.252

auto eth1
iface eth1 inet static
      address 192.178.0.21
      netmask 255.255.255.252
```

- Heiter
```
auto eth0
iface eth0 inet static
         address 192.178.0.22
         netmask 255.255.255.252
         gateway 192.178.0.21
	 up echo nameserver 192.168.122.1 > /etc/resolv.conf

auto eth2
iface eth2 inet static
         address 192.178.8.1
         netmask 255.255.248.0

auto eth1
iface eth1 inet static
         address 192.178.4.1
         netmask 255.255.252.0
```

- TurkRegion dan GrabForest
```
auto eth0
iface eth0 inet dhcp
```

- Sein
```
auto eth0
iface eth0 inet static
	address 192.178.4.2
	netmask 255.255.252.0
	gateway 192.178.4.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

## Routing
- Himmel
```
route add -net 192.178.0.0 netmask 255.255.255.252 gw 192.178.0.130
route add -net 192.178.0.4 netmask 255.255.255.252 gw 192.178.0.130
```

- Frieren
```
route add -net 192.178.0.0 netmask 255.255.255.252 gw 192.178.0.10
route add -net 192.178.0.4 netmask 255.255.255.252 gw 192.178.0.10
route add -net 192.178.0.128 netmask 255.255.255.128 gw 192.178.0.10
route add -net 192.178.1.0 netmask 255.255.255.0 gw 192.178.0.10
```

- Aura
```
route add -net 192.178.0.0 netmask 255.255.255.252 gw 192.178.0.18
route add -net 192.178.0.4 netmask 255.255.255.252 gw 192.178.0.18
route add -net 192.178.0.128 netmask 255.255.255.128 gw 192.178.0.18
route add -net 192.178.1.0 netmask 255.255.255.0 gw 192.178.0.18
route add -net 192.178.0.8 netmask 255.255.255.252 gw 192.178.0.18
route add -net 192.178.0.12 netmask 255.255.255.252 gw 192.178.0.18

route add -net 192.178.8.0 netmask 255.255.248.0 gw 192.178.0.22
route add -net 192.178.4.0 netmask 255.255.252.0 gw 192.178.0.22
```

## Konfigurasi DHCP
Pertama-tama, install isc-dhcp-server dengan perintah berikut
```
apt-get update
wait
apt-get install isc-dhcp-server -y
wait

echo '
INTERFACESv4="eth0"
INTERFACESv6=""
' > /etc/default/isc-dhcp-server

cp ~/dhcpd.conf /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

Lalu konfigurasikan perintah ini pada file dhcpd.conf
```
option domain-name "example.org";
option domain-name-servers ns1.example.org, ns2.example.org;

default-lease-time 600;
max-lease-time 7200;

ddns-update-style none;

subnet 192.178.0.0 netmask 255.255.255.252 {
}

subnet 192.178.0.128 netmask 255.255.255.128 {
    range 192.178.0.131 192.178.0.254;
    option routers 192.178.0.129;
    option broadcast-address 192.178.0.255;
    option domain-name-servers 192.178.0.6;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 192.178.1.0 netmask 255.255.255.0 {
    range 192.178.1.2 192.178.1.254;
    option routers 192.178.1.1;
    option broadcast-address 192.178.1.255;
    option domain-name-servers 192.178.0.6;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 192.178.8.0 netmask 255.255.248.0 {
    range 192.178.8.2 192.178.15.254;
    option routers 192.178.8.1;
    option broadcast-address 192.178.15.255;
    option domain-name-servers 192.178.0.6;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 192.178.4.0 netmask 255.255.252.0 {
    range 192.178.4.3 192.178.7.254;
    option routers 192.178.4.1;
    option broadcast-address 192.178.7.255;
    option domain-name-servers 192.178.0.6;
    default-lease-time 180;
    max-lease-time 5760;
}
```

`option domain-name-servers` adalah konfigurasi untuk menentukan DNS Server yang akan digunakan

`default-lease-time` adalah waktu standar untuk lease suatu alamat IP

`max-lease-time` adalah waktu maksimum untuk lease suatu alamat IP

`subnet` adalah jaringan subnet yang akan digunakan dalam konfigurasi

`range` adalah rentang alamat IP yang akan dialokasikan

`option routers` adalah pengaturan IP router yang akan dijadikan referensi

`option broadcast-address` adalah konfigurasi alamat IP broadcast yang akan dipakai

## DHCP Relay
Pasang isc-dhcp-relay di router Himmel dan Heiter menggunakan perintah ini
```
# Configuration DHCP Relay
apt-get update
wait
apt-get install isc-dhcp-relay -y
wait

echo '
SERVERS="192.178.0.2"
INTERFACES="eth0 eth1 eth2"
OPTIONS="-m replace"
' >  /etc/default/isc-dhcp-relay

echo '
net.ipv4.ip_forward=1
' >  /etc/sysctl.conf
```

`SERVERS` adalah alamat IP dari DHCP Server yang akan digunakan

`INTERFACES` adalah antarmuka yang akan dipakai untuk DHCP Relay

`OPTION` adalah pilihan atau konfigurasi spesifik yang digunakan untuk DHCP Relay

`net.ipv4.ip_forward=1` adalah untuk mengaktifkan fungsi ip forwarding

## Konfigurasi DNS
```
apt-get update
wait

apt-get install bind9 -y
wait
cp ~/named.conf.options /etc/bind/

service bind9 restart
```

`named.conf.options` merupakan konfigurasi dari DNS Server yang isinya adalah
```
options {
        directory "/var/cache/bind";

        forwarders {
                192.168.122.1;
        };

        allow-query{any;};
        auth-nxdomain no;
        listen-on-v6 { any; };
};
```

`forwarders` adalah server DNS yang akan digunakan untuk meneruskan permintaan

`allow-query` adalah konfigurasi yang mengizinkan permintaan dari semua alamat IP

`auth-nxdomain no` adalah opsi yang memungkinkan penanganan domain yang tidak ada

## Konfigurasi Web Server
Install nginx pada Sein dan Stark
```
apt-get update
wait
apt-get install nginx -y
wait
cp ~/index.nginx-debian.html /var/www/html
service nginx start
apt-get install netcat -y
```

`index.nginx-debian.html` adalah nama file HTML yang akan ditampilkan di server web nantinya

`netcat` adalah perangkat lunak yang digunakan untuk mengirimkan data ke server web

## Soal

## Nomor 1
Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.

Pada Aura, konfigurasikan iptables
```iptables -t nat -A POSTROUTING -s 192.178.0.0/20 -o eth0 -j SNAT --to-source 192.168.122.14```

`-t nat` digunakan untuk menambahkan aturan pada tabel nat

`-A POSTROUTING` adalah menambahkan aturan pada rantai POSTROUTING

`-s` adalah opsi yang menetapkan alamat IP sumber

`-o` adalah opsi yang menetapkan antarmuka

`-j SNAT` adalah opsi yang menunjukkan aksi SNAT yang akan dilakukan

`--to-source` adalah opsi yang menunjukkan alamat IP yang akan digunakan untuk melakukan SNAT

## Nomor 2
Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.

Untuk drop semua koneksi TCP dan UDP kecuali yang menuju port 8080 pada TCP, konfigurasi iptables pada node SchewerMountain
```
# Clear semua aturan yang ada jika diperlukan
iptables -F

# Izinkan koneksi yang masuk pada port 8080 TCP
iptables -A INPUT -p tcp --dport 8080 -j ACCEPT

# Drop semua koneksi TCP yang bukan menuju ke port 8080
iptables -A INPUT -p tcp ! --dport 8080 -j DROP

# Drop semua koneksi UDP
iptables -A INPUT -p udp -j DROP
```

`iptables -F` adalah perintah yang digunakan untuk menghapus semua aturan (rule) yang ada pada iptables

`iptables -A INPUT -p tcp --dport 8080 -j ACCEPT` adalah perintah untuk menambahkan aturan pada rantai INPUT agar menerima koneksi TCP pada port 8080

`iptables -A INPUT -p tcp ! --dport 8080 -j DROP` adalah perintah untuk menambahkan aturan pada rantai INPUT agar menolak koneksi TCP yang tidak menuju ke port 8080

## Nomor 3
Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.

Untuk membatasi akses ping terhadap DHCP dan DNS Server hanya untuk maksimal tiga perangkat secara bersamaan, kita akan mengonfigurasi iptables pada node Revolte dan Richter

```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```

`iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP` menambahkan aturan pada rantai INPUT untuk menolak koneksi ICMP yang melebihi 3 buah koneksi

`--connlimit-above 3` adalah parameter yang menetapkan jumlah maksimum koneksi

`--connlimit-mask 0` adalah parameter yang menetapkan mask

## Nomor 4
Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.

Untuk membatasi koneksi SSH pada Web Server agar hanya dapat diakses oleh masyarakat yang berada di GrobeForest, konfigurasi iptables pada node Sein dan Stark perlu dilakukan
```
iptables -A INPUT -p tcp --dport 22 -s 192.178.4.0/22 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP```
```

`-s 192.178.4.0/22` menentukan rentang alamat IP sumber yang diizinkan, dalam hal ini, subnet 192.178.4.0/22 yang terletak di block A10, yang merupakan bagian dari GrobeForest

`iptables -A INPUT -p tcp --dport 22 -j DROP` adalah perintah untuk menambahkan aturan pada rantai INPUT agar menolak koneksi TCP pada port 22 yang tidak berasal dari subnet A10 (192.178.4.0/22)

## Nomor 5
Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.

Untuk membatasi akses ke Web Server agar hanya diperbolehkan pada jam kerja (Senin-Jumat) pada rentang waktu 08.00-16.00, konfigurasi iptables pada node Sein dan Stark perlu dilakukan
```
# Izinkan akses ke Web Server pada Senin-Jumat pukul 08.00-16.00
iptables -A INPUT -p tcp --dport 80 -m time --timestart 08:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT

# Menolak akses selain dari aturan yang telah ditentukan
iptables -A INPUT -p tcp --dport 80 -j DROP
```
