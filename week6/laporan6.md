# Laporan Praktikum Jaringan Komputer

## Modul 6 – TCP

**Nama:** Yustinus Yendy S.A  
**NIM:** 103072400065  

---

## Tujuan
Memahami cara kerja protokol TCP menggunakan Wireshark, termasuk proses three-way handshake, sequence number, acknowledgment, serta mekanisme pengiriman data.

---

## Percobaan Praktikum

### 6.2

#### Langkah - Langkah
### 6.2 

#### Langkah - Langkah
1. Membuka aplikasi Wireshark pada komputer/laptop.  
2. Memilih interface jaringan yang sedang aktif (Wi-Fi atau Ethernet), kemudian memulai proses capture dengan melakukan double click pada interface tersebut.  
3. Membiarkan proses capture berjalan selama beberapa detik untuk memastikan paket jaringan mulai terekam.  
4. Membuka browser dan mengakses halaman berikut:  
   http://gaia.cs.umass.edu/wireshark-labs/TCP-wireshark-file1.html  
   ![Tampilan link web](../assets/week6/week6(1).png)
5. Menyalin seluruh teks yang terdapat pada halaman tersebut, kemudian menempelkannya ke dalam aplikasi Notepad.  
6. Menyimpan file tersebut dengan nama **alice.txt**.  
7. Pada halaman website, memilih opsi upload file, kemudian mengunggah file **alice.txt** yang telah dibuat.  
8. Menekan tombol submit/upload dan menunggu hingga proses upload selesai (ditandai dengan munculnya halaman sukses).  
   ![halaman sukses](../assets/week6/week6(2).png)
9. Setelah proses upload selesai, kembali ke Wireshark dan menghentikan proses capture.  
10. Menggunakan filter `tcp` pada bagian display filter untuk menampilkan paket TCP saja.  
![TCP alice.txt](../assets/week6/week6(3).png)


---

### 6.3

#### Langkah - Langkah
1. Membuka hasil capture Wireshark dari percobaan sebelumnya.  
2. Menuliskan filter `tcp` pada kolom display filter untuk menampilkan paket TCP saja.  
3. Mengamati bagian awal paket untuk menemukan proses **three-way handshake**.  
4. Mengidentifikasi tiga paket utama yaitu **SYN**, **SYN-ACK**, dan **ACK**.  
5. Memilih paket pertama (SYN) untuk mengetahui informasi klien dan server.  
6. Mengamati kolom **Source** dan **Destination** untuk mendapatkan alamat IP.  
7. Mengamati bagian **Info** untuk mengetahui nomor port yang digunakan.  
8. Memverifikasi koneksi dengan melihat paket SYN-ACK dan ACK sebagai balasan dari server dan klien.  
![3 way handshake](../assets/week6/week6(4).png)

---

#### Jawab Pertanyaan

**1. Alamat IP dan Port TCP Klien**

Alamat IP Klien: `192.168.1.102`  
Port TCP Klien: `1161`  

Analisis:  
Berdasarkan paket pertama dengan flag SYN, terlihat bahwa klien dengan IP 192.168.1.102 memulai koneksi ke server menggunakan port 1161 sebagai source port. Port ini bersifat dinamis (random) yang digunakan untuk komunikasi TCP.

---

**2. Alamat IP dan Port TCP Server**

Alamat IP Server: `128.119.245.12`  
Port TCP Server: `80`  

Analisis:  
Server dengan IP 128.119.245.12 merespon permintaan dari klien melalui port 80 yang merupakan port standar untuk layanan HTTP. Hal ini terlihat pada paket SYN-ACK di mana server mengirim balasan ke klien.

---

#### Analisis Three-Way Handshake

Berdasarkan hasil capture, proses pembentukan koneksi TCP terjadi melalui tiga tahap:

1. **SYN (Client → Server)**  
   Klien mengirimkan segmen SYN untuk memulai koneksi dengan sequence number = 0.

2. **SYN-ACK (Server → Client)**  
   Server merespon dengan SYN-ACK, sequence number = 0 dan acknowledgment number = 1, yang merupakan hasil dari sequence number klien + 1.

3. **ACK (Client → Server)**  
   Klien mengirimkan ACK sebagai konfirmasi bahwa koneksi telah berhasil terbentuk, dengan acknowledgment number = 1.

Proses ini menunjukkan bahwa koneksi TCP berhasil dibangun sebelum pertukaran data dilakukan.

---

### 6.4

#### Jawab Pertanyaan

**1.**  
Segmen TCP pertama (paket nomor 1) merupakan segmen SYN dengan relative sequence number sebesar 0. Hal ini dapat dilihat pada bagian Transmission Control Protocol yang menunjukkan nilai `Seq: 0`.  

Selain itu, flag SYN dalam segmen ini bernilai aktif (SYN: Set), yang menandakan bahwa klien sedang memulai koneksi ke server. Segmen ini merupakan tahap pertama dalam proses **TCP three-way handshake**.
![SYN](../assets/week6/week6(5).png)

---

**2.**  
Pada segmen kedua (paket nomor 2), server merespon dengan segmen SYN-ACK. Segmen ini memiliki relative sequence number sebesar 0 dan acknowledgment number sebesar 1.  

Nilai acknowledgment tersebut diperoleh dari sequence number klien sebelumnya (0) yang ditambahkan 1. Hal ini menunjukkan bahwa server telah menerima permintaan koneksi dari klien.  

Segmen ini disebut sebagai SYN-ACK karena kedua flag, yaitu SYN dan ACK, aktif secara bersamaan. Segmen ini merupakan tahap kedua dalam proses **TCP three-way handshake**.
![SYN, ACK](../assets/week6/week6(6).png)


---

**3.**  
Berdasarkan hasil analisis pada paket yang mengandung HTTP POST (paket nomor 199), segmen TCP yang membawa perintah POST memiliki relative sequence number sebesar **164041**.  

Hal ini dapat dilihat pada bagian Transmission Control Protocol di Wireshark, di mana field `Sequence Number (relative)` menunjukkan nilai tersebut. Selain itu, pada bagian payload juga terlihat adanya perintah **POST /ethereal-labs/lab3-1-reply.htm HTTP/1.1**, yang menandakan bahwa segmen tersebut membawa data aplikasi (HTTP).  

Dengan demikian, dapat disimpulkan bahwa sequence number 164041 merupakan posisi byte awal dari data HTTP POST yang dikirim oleh klien ke server.
![HTTP POST](../assets/week6/week6(7).png)

---

**4.**  
Berdasarkan hasil pengamatan pada beberapa segmen TCP setelah proses HTTP POST, terlihat bahwa nilai sequence number dan acknowledgment number mengalami perubahan secara bertahap dan berurutan.  

Sebagai contoh, pada paket balasan dari server, nilai acknowledgment number terus meningkat (Ack = 162309, 164041, 164091), yang menunjukkan bahwa server telah menerima data dari klien secara bertahap sesuai urutan byte yang dikirim.  
![ww](../assets/week6/week6(8).jpeg)

Hal ini menunjukkan bahwa TCP menggunakan mekanisme sequence number dan acknowledgment number untuk menjaga keutuhan dan urutan data, sehingga setiap byte yang dikirim dapat dilacak dan dikonfirmasi penerimaannya dengan tepat.
![](../assets/week6/week6(10).jpeg)

---

**5.**  
Berdasarkan hasil pengamatan pada beberapa segmen TCP awal, terlihat bahwa nilai length pada setiap segmen memiliki ukuran yang berbeda-beda, seperti 62, 62, 54, 619, dan 1514 byte.  

Perbedaan ukuran ini terjadi karena data yang dikirim oleh TCP dipecah menjadi beberapa segmen dengan ukuran yang menyesuaikan kapasitas jaringan (Maximum Segment Size/MSS). Segmen dengan ukuran kecil biasanya merupakan paket kontrol seperti SYN, SYN-ACK, dan ACK, sedangkan segmen dengan ukuran lebih besar merupakan paket yang membawa data.  

Hal ini menunjukkan bahwa TCP mengirimkan data secara bertahap dalam bentuk segmen-segmen dengan ukuran yang bervariasi, bukan dalam satu paket besar sekaligus.

![alt text](<WhatsApp Image 2026-04-01 at 08.19.52.jpeg>)
---

**6.**   
Berdasarkan hasil pengamatan pada field TCP, nilai window size (Win) menunjukkan kapasitas buffer yang tersedia pada sisi penerima.  

Dari beberapa segmen yang diamati, nilai window size berada di atas 6000 (contohnya 6780, 8760, 17520), sehingga menunjukkan bahwa buffer penerima masih memiliki ruang yang cukup untuk menerima data.  

Selain itu, tidak ditemukan kondisi window bernilai 0, yang berarti tidak terjadi hambatan (blocking) dalam proses pengiriman data. Hal ini menunjukkan bahwa aliran data berlangsung dengan lancar tanpa adanya keterbatasan buffer dari sisi penerima.
![alt text](<WhatsApp Image 2026-04-01 at 08.22.47 (2).jpeg>)

---
**7.**  
Berdasarkan hasil pengamatan pada Wireshark, tidak ditemukan adanya segmen TCP yang mengalami retransmission. Hal ini dapat dilihat dari tidak adanya indikasi seperti “TCP Retransmission” pada kolom Info maupun hasil filter `tcp.analysis.retransmission`.  

Selain itu, aliran sequence number dan acknowledgment number berjalan secara berurutan tanpa adanya pengulangan segmen. Hal ini menunjukkan bahwa seluruh paket berhasil dikirim dan diterima dengan baik tanpa kehilangan data.  

Dengan demikian, dapat disimpulkan bahwa proses komunikasi TCP berlangsung secara normal dan stabil tanpa adanya gangguan jaringan.
![alt text](<WhatsApp Image 2026-04-01 at 08.26.45.jpeg>)
---

**8.**  
(Sesuai instruksi praktikum / kesepakatan kelas, tidak dikerjakan)

---

**9.**  
(Sesuai instruksi praktikum / kesepakatan kelas, tidak dikerjakan)

---

### 6.5

#### Jawab Pertanyaan

**1.**  
Berdasarkan grafik Time-Sequence (Stevens), terlihat bahwa proses pengiriman data TCP menunjukkan pola peningkatan sequence number secara bertahap seiring waktu.  

Pada awal grafik, kenaikan sequence number terlihat lebih cepat yang menunjukkan fase **slow start**, di mana TCP meningkatkan jumlah data yang dikirim secara agresif untuk menemukan kapasitas jaringan.  

Selanjutnya, pola kenaikan menjadi lebih stabil dan teratur, yang menunjukkan fase **congestion avoidance**, di mana TCP menyesuaikan laju pengiriman data agar tidak menyebabkan kemacetan pada jaringan.  

Tidak terlihat adanya penurunan drastis pada grafik, sehingga dapat disimpulkan bahwa tidak terjadi packet loss yang signifikan. Hal ini menunjukkan bahwa koneksi TCP berjalan dengan stabil dan efisien selama proses pengiriman data.
![alt text](<WhatsApp Image 2026-04-01 at 08.30.16.jpeg>)
---

**2.**  
(Sesuai instruksi praktikum, tidak dikerjakan)

---

## Kesimpulan

Berdasarkan hasil praktikum yang telah dilakukan, dapat disimpulkan bahwa protokol TCP bekerja secara connection-oriented dengan melalui proses three-way handshake (SYN, SYN-ACK, ACK) sebelum melakukan pertukaran data. Proses ini memastikan bahwa koneksi antara klien dan server terbentuk dengan baik.  

Selama proses pengiriman data, TCP menggunakan mekanisme sequence number dan acknowledgment number untuk menjaga urutan serta keutuhan data. Setiap segmen yang dikirim akan dikonfirmasi oleh penerima, sehingga data dapat diterima secara lengkap dan berurutan.  

Dari hasil analisis Wireshark, terlihat bahwa data dikirim dalam beberapa segmen dengan ukuran yang bervariasi sesuai dengan kapasitas jaringan. Selain itu, nilai window size menunjukkan bahwa buffer penerima tidak mengalami hambatan, sehingga aliran data berjalan dengan lancar.  

Tidak ditemukan adanya retransmission pada proses komunikasi, yang menandakan bahwa tidak terjadi kehilangan paket dan koneksi berjalan dengan stabil. Hal ini juga didukung oleh grafik Time-Sequence (Stevens) yang menunjukkan peningkatan sequence number secara konsisten tanpa penurunan signifikan.  

Dengan demikian, dapat disimpulkan bahwa TCP mampu menyediakan komunikasi yang andal, teratur, dan efisien dalam pengiriman data pada jaringan komputer.


---