# Laporan Praktikum Jaringan Komputer

## Modul 13 – Ethernet dan ARP

**Nama:** Yustinus Yendy S.A  
**NIM:** 103072400065  

## Tujuan

Memahami cara kerja Ethernet dan ARP (Address Resolution Protocol) serta menganalisis frame Ethernet dan paket ARP menggunakan Wireshark.

## Langkah Praktikum

### A. Ethernet

1. Membuka aplikasi Wireshark.
2. Memilih interface jaringan yang aktif.
3. Memulai proses capture paket.
4. Membuka browser dan mengakses halaman berikut:

```text
http://gaia.cs.umass.edu/wireshark-labs/HTTP-ethereal-lab-file3.html
```

5. Menunggu halaman selesai dimuat.
6. Menghentikan proses capture.
7. Mencari paket HTTP GET pada hasil capture.
8. Mengamati informasi pada Ethernet Frame seperti:
   - Source MAC Address
   - Destination MAC Address
   - EtherType

### B. ARP

1. Membuka Command Prompt.
2. Menampilkan isi ARP cache dengan perintah:

```bash
arp -a
```

3. Menghapus ARP cache menggunakan perintah:

```bash
arp -d *
```

4. Memulai kembali proses capture pada Wireshark.
5. Mengakses kembali halaman web yang sama.
6. Menghentikan proses capture.
7. Memberikan filter:

```text
arp
```

8. Mengamati paket ARP Request dan ARP Reply.
9. Menganalisis alamat IP dan MAC Address yang terlibat dalam proses ARP.

## Hasil Pengamatan

### Ethernet

#### Halaman Website yang Diakses
![](../assets/modul13/modul13(1).png)

#### Paket HTTP GET
![](../assets/modul13/modul13(2).png)

#### Detail Ethernet Frame
![](../assets/modul13/modul13(3).png)

### ARP

#### Isi ARP Cache
![](../assets/modul13/modul13(4).png)

#### Paket ARP Request
![](../assets/modul13/modul13(5).png)

## Analisis

### Ethernet

Berdasarkan hasil capture Wireshark, frame Ethernet digunakan untuk mengirimkan data pada jaringan lokal. Setiap frame memiliki alamat MAC sumber dan tujuan yang digunakan untuk proses komunikasi antar perangkat dalam satu jaringan.

Analisis yang dilakukan:
- Source MAC Address
- Destination MAC Address
- EtherType
- Panjang frame Ethernet

### ARP

ARP digunakan untuk menerjemahkan alamat IP menjadi alamat MAC agar paket dapat dikirimkan ke perangkat tujuan pada jaringan lokal.

Analisis yang dilakukan:
- Sender IP Address
- Sender MAC Address
- Target IP Address
- Target MAC Address
- Perbedaan ARP Request dan ARP Reply

## Kesimpulan

Berdasarkan praktikum yang telah dilakukan, dapat disimpulkan bahwa Ethernet merupakan teknologi yang digunakan pada lapisan Data Link untuk proses pengiriman frame dalam jaringan lokal. ARP berfungsi untuk menerjemahkan alamat IP menjadi alamat MAC sehingga komunikasi antar perangkat pada jaringan dapat berlangsung dengan benar. Melalui Wireshark, proses pertukaran frame Ethernet serta ARP Request dan ARP Reply dapat diamati secara langsung.