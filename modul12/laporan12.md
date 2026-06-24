# Laporan Praktikum Jaringan Komputer

## Modul 12 – ICMP dan Asistensi Tugas Besar

**Nama:** Yustinus Yendy S.A  
**NIM:** 103072400065  

## Tujuan
Memahami cara kerja protokol ICMP menggunakan Wireshark melalui analisis paket Ping dan Traceroute.

## Langkah Praktikum

### A. ICMP dan Ping
1. Membuka aplikasi Wireshark.
2. Memilih interface jaringan yang aktif.
3. Memulai proses capture paket.
4. Membuka Command Prompt.
5. Menjalankan perintah:

```bash
ping -n 10 www.ust.hk
```

6. Menghentikan proses capture paket.
7. Memberikan filter `icmp` pada Wireshark.
8. Mengamati paket ICMP Echo Request dan Echo Reply.

### B. ICMP dan Traceroute
1. Memulai kembali proses capture paket pada Wireshark.
2. Membuka Command Prompt.
3. Menjalankan perintah:

```bash
tracert www.inria.fr
```

4. Menghentikan proses capture paket.
5. Memberikan filter `icmp` pada Wireshark.
6. Mengamati paket ICMP yang digunakan selama proses traceroute.
7. Menganalisis hop yang dilewati paket menuju tujuan.

## Hasil Pengamatan

### Ping

#### Screenshot Ping
![](../assets/modul12/modul12(1).png)

#### Screenshot Wireshark Ping
![](../assets/modul12/modul12(2).png)

### Traceroute

#### Screenshot Traceroute
![](../assets/modul12/modul12(3).png)

#### Screenshot Wireshark Traceroute
![](../assets/modul12/modul12(4).png)

## Analisis

### ICMP Echo Request dan Echo Reply
Tuliskan hasil pengamatan mengenai:
- Source IP
- Destination IP
- Type dan Code ICMP
- Round Trip Time (RTT)
- Jumlah paket yang berhasil dikirim dan diterima

### Traceroute
Tuliskan hasil pengamatan mengenai:
- Jumlah hop yang dilewati
- Alamat IP setiap hop
- Respon ICMP pada masing-masing hop
- Waktu tempuh menuju tujuan

## Kesimpulan

Berdasarkan praktikum yang telah dilakukan, dapat disimpulkan bahwa protokol ICMP digunakan untuk proses diagnostik jaringan seperti Ping dan Traceroute. Ping memanfaatkan paket Echo Request dan Echo Reply untuk menguji konektivitas jaringan, sedangkan Traceroute digunakan untuk mengetahui jalur atau hop yang dilewati paket menuju host tujuan.