# Laporan Praktikum Jaringan Komputer

## Modul 14 – 802.11 WiFi

**Nama:** Yustinus Yendy S.A  
**NIM:** 103072400065  

## Tujuan

Memahami dan menginvestigasi cara kerja jaringan WiFi (IEEE 802.11) menggunakan Wireshark.

## Langkah Praktikum

### A. Membuka File Capture WiFi

1. Membuka aplikasi Wireshark.
2. Membuka file capture WiFi yang disediakan oleh praktikum (`Wireshark_802_11.pcap` atau nama file yang diberikan asisten).
3. Mengamati paket-paket yang terdapat pada capture.
4. Mengidentifikasi Access Point (AP) dan client yang terlibat dalam komunikasi.

### B. Analisis Beacon Frame

1. Mencari paket dengan tipe Beacon Frame.
2. Memilih salah satu Beacon Frame.
3. Mengamati informasi:
   - SSID
   - BSSID
   - Channel
   - Supported Rates
   - Capability Information

### C. Analisis Data Transfer

1. Mencari paket yang berhubungan dengan transfer data.
2. Mengidentifikasi komunikasi antara client dan Access Point.
3. Mengamati alamat MAC sumber dan tujuan.
4. Menganalisis paket yang berkaitan dengan akses website.

### D. Analisis Association dan Disassociation

1. Mencari paket Association Request.
2. Mencari paket Association Response.
3. Mengamati proses client bergabung ke Access Point.
4. Mengidentifikasi paket Disassociation jika tersedia.
5. Menganalisis proses koneksi dan pemutusan koneksi pada jaringan WiFi.

## Hasil Pengamatan

### Tampilan Awal Capture WiFi

![](../assets/modul14/modul14(1).png)

### Beacon Frame

![](../assets/modul14/modul14(2).png)

### Detail Beacon Frame

![](../assets/modul14/modul14(3).png)

### Data Transfer

![](../assets/modul14/modul14(4).png)

### Association Request

![](../assets/modul14/modul14(5).png)

### Association Response

![](../assets/modul14/modul14(6).png)


## Analisis

### Beacon Frame

Analisis yang dilakukan:
- SSID jaringan
- BSSID Access Point
- Channel yang digunakan
- Capability Information
- Informasi yang disiarkan oleh Access Point

### Data Transfer

Analisis yang dilakukan:
- Source MAC Address
- Destination MAC Address
- Jenis frame
- Aktivitas komunikasi client dan Access Point

### Association dan Disassociation

Analisis yang dilakukan:
- Proses client melakukan koneksi ke Access Point
- Association Request
- Association Response
- Disassociation Frame
- Alur komunikasi sebelum dan sesudah koneksi

## Kesimpulan

Berdasarkan praktikum yang telah dilakukan, dapat disimpulkan bahwa protokol IEEE 802.11 menggunakan berbagai jenis frame untuk mendukung komunikasi pada jaringan WiFi. Beacon Frame digunakan untuk mengumumkan keberadaan Access Point, Association Frame digunakan saat client bergabung ke jaringan, sedangkan Data Frame digunakan untuk proses pertukaran data antara client dan Access Point.