# Laporan Praktikum Jaringan Komputer

## Modul 11 – DHCP

**Nama:** Yustinus Yendy S.A  
**NIM:** 103072400065  

## Tujuan
memahami atau mengetahui cara kerja protokol DHCP menggunakan Wireshark

## Langkah Praktikum
1. Membuka aplikasi Wireshark.
2. Memilih interface jaringan yang aktif.
3. Memulai proses capture paket.
4. Menjalankan perintah berikut pada Command Prompt:
ipconfig /release
ipconfig /renew
5. Menghentikan proses capture.
6. Memberikan filter dhcp pada Wireshark.
7. Mengamati paket DHCP Discover, Offer, Request, dan ACK.


## Hasil Pengamatan

### DHCP Discover
DHCP Discover merupakan paket pertama yang dikirim oleh client untuk mencari server DHCP yang tersedia pada jaringan.

### DHCP Offer
DHCP Offer merupakan respons dari server DHCP yang menawarkan alamat IP kepada client.

### DHCP Request
DHCP Request dikirim oleh client sebagai tanda bahwa client menerima penawaran alamat IP dari server DHCP.

### DHCP ACK
DHCP ACK merupakan konfirmasi akhir dari server DHCP bahwa alamat IP berhasil diberikan kepada client.

## Analisis
Berdasarkan hasil pengamatan, proses DHCP berjalan menggunakan mekanisme DORA (Discover, Offer, Request, Acknowledgement). Seluruh proses dilakukan secara otomatis sehingga client dapat memperoleh alamat IP tanpa konfigurasi manual.

Wireshark memungkinkan pengguna untuk melihat secara detail setiap paket DHCP yang dipertukarkan antara client dan server. Informasi yang dapat diamati meliputi alamat IP yang diberikan, subnet mask, gateway, DNS server, serta tipe pesan DHCP yang digunakan.

## Kesimpulan
DHCP digunakan untuk memberikan konfigurasi jaringan secara otomatis.
DHCP bekerja menggunakan mekanisme DORA.
Wireshark dapat digunakan untuk menganalisis paket DHCP secara detail.
DHCP mempermudah administrasi jaringan dan mengurangi kesalahan konfigurasi alamat IP.
Dokumentasi

### 1. Perintah ipconfig /release
![](../assets/modul11/modul11(1).png)

### 2. Perintah ipconfig /renew
![](../assets/modul11/modul11(2).png)

### 3. Filter DHCP pada Wireshark
![](../assets/modul11/modul11(3).png)

### 4. DHCP Discover
![](../assets/modul11/modul11(4).png)

### 5. DHCP Offer
![](../assets/modul11/modul11(5).png)

### 6. DHCP Request
![](../assets/modul11/modul11(6).png)

### 7. DHCP ACK
![](../assets/modul11/modul11(7).png)
