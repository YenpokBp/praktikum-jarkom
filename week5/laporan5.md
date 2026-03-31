# Laporan Praktikum Jaringan Komputer  
## Modul 5 - UDP  

### Nama: Yustinus Yendy S.A  
### NIM: 103072400065  
### Kelas: IF-04-02  

---

## 1. Tujuan Praktikum  
Mahasiswa dapat menginvestigasi cara kerja protokol UDP menggunakan Wireshark.

---

## 2. Dasar Teori  
UDP (User Datagram Protocol) adalah protokol transport yang bersifat connectionless, artinya tidak memerlukan proses koneksi sebelum pengiriman data. UDP tidak menjamin keandalan pengiriman data, tidak melakukan retransmisi, serta tidak memiliki mekanisme kontrol aliran maupun kontrol kemacetan. Oleh karena itu, UDP memiliki performa yang lebih cepat dibandingkan TCP dan sering digunakan pada layanan seperti DNS, streaming, dan protokol modern seperti QUIC.

---

## 3. Percobaan  

### 3.1 Capture Paket UDP  

#### Langkah:
1. Membuka aplikasi Wireshark  
2. Memilih interface jaringan (WiFi)  
3. Memulai proses capture  
4. Melakukan aktivitas jaringan (mengakses internet)  
5. Menghentikan capture  
6. Menggunakan filter:
   ```bash
   udp
   ```

---

#### Hasil Capture:
![UDP List](../assets/week5/week5(1).png)

---

#### Analisis:  
Berdasarkan hasil capture dengan filter `udp`, terlihat beberapa paket yang menggunakan protokol UDP. Hal ini menunjukkan bahwa terdapat komunikasi data yang berlangsung tanpa proses koneksi terlebih dahulu.

UDP tidak memiliki mekanisme handshake seperti pada TCP (SYN, ACK), sehingga pengiriman data dilakukan secara langsung tanpa membangun koneksi terlebih dahulu.

---

### 3.2 Analisis Header UDP  

#### Hasil Capture:
![UDP Detail](../assets/week5/week5(2).png)

---

#### Analisis:  
Pada hasil capture terlihat paket UDP dengan **source port 49945** dan **destination port 443**.

Bagian header UDP terdiri dari beberapa komponen utama, yaitu:

- **Source Port (49945)**: menunjukkan port asal dari client  
- **Destination Port (443)**: menunjukkan tujuan komunikasi, yaitu layanan HTTPS  
- **Length (37)**: menunjukkan panjang total datagram UDP  
- **Checksum**: digunakan untuk mendeteksi adanya error pada data  

Struktur header UDP yang sederhana menunjukkan bahwa UDP tidak memiliki mekanisme kompleks seperti TCP.

Selain itu, tidak ditemukan adanya proses handshake seperti SYN dan ACK, yang menandakan bahwa UDP bersifat connectionless.

Penggunaan port 443 pada UDP menunjukkan bahwa paket ini kemungkinan digunakan oleh protokol modern seperti **QUIC (HTTP/3)** yang berjalan di atas UDP.

---

### 3.3 UDP dalam DNS  

#### Hasil Capture:
![DNS UDP](../assets/week5/week5(3).png)

---

#### Analisis:  
Berdasarkan hasil capture Wireshark, terlihat paket DNS response yang dikirim menggunakan protokol UDP dengan source port 53.

Pada paket tersebut terdapat informasi bahwa query berhasil diproses tanpa error, yang ditunjukkan oleh status "Standard query response, No error".

Selain itu, terdapat 4 jawaban (Answer RRs: 4) yang menunjukkan bahwa DNS memberikan beberapa hasil pemetaan domain.

Hal ini membuktikan bahwa DNS menggunakan protokol UDP dalam proses komunikasi karena membutuhkan kecepatan dalam melakukan query dan response tanpa melalui proses koneksi terlebih dahulu.

---

## 4. Analisis Pertanyaan  

### 1. Apakah UDP menggunakan koneksi?  
Tidak, UDP bersifat connectionless.

### 2. Apakah UDP memiliki mekanisme handshake?  
Tidak.

### 3. Apakah UDP menjamin data sampai?  
Tidak, UDP tidak menjamin keandalan pengiriman data.

### 4. Mengapa UDP lebih cepat dari TCP?  
Karena UDP tidak memiliki mekanisme handshake, kontrol aliran, dan retransmisi, sehingga proses pengiriman data menjadi lebih cepat.

---

## 5. Kesimpulan  
UDP merupakan protokol transport yang sederhana dan cepat karena tidak menggunakan mekanisme koneksi maupun kontrol seperti TCP. Berdasarkan hasil praktikum, terlihat bahwa UDP langsung mengirim data tanpa proses handshake dan digunakan dalam berbagai layanan seperti DNS dan protokol modern seperti QUIC pada HTTP/3.