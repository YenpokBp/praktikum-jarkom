# Laporan Praktikum Jaringan Komputer  
## Modul 4 - DNS  

### Nama: Yustinus Yendy S.A  
### NIM: 103072400065  
### Kelas: IF-04-02  

---

## 1. Tujuan Praktikum  
Mahasiswa dapat memahami dan menginvestigasi cara kerja DNS menggunakan tools seperti nslookup, ipconfig, dan Wireshark.

---

## 2. Dasar Teori  
DNS (Domain Name System) adalah sistem yang digunakan untuk menerjemahkan nama domain menjadi alamat IP. DNS bekerja dengan cara client mengirim request ke DNS server dan menerima response berupa alamat IP. Proses ini merupakan tahap awal sebelum client dapat berkomunikasi dengan server tujuan di internet.

---

## 3. Percobaan  

### 3.1 Nslookup  
Melakukan pencarian alamat IP dari domain.

#### Perintah:
```bash
nslookup www.mit.edu
```

#### Hasil:
![nslookup www.mit.edu](../assets/week4/week4(1).png)

#### Analisis:  
Perintah `nslookup` digunakan untuk mengetahui alamat IP dari suatu domain. Hasil yang diperoleh menunjukkan alamat IP dari domain tersebut serta server DNS yang digunakan untuk memberikan jawaban.

---

### 3.2 Nslookup NS Record  

#### Perintah:
```bash
nslookup -type=NS mit.edu
```

#### Hasil:
![nslookup -type=NS mit.edu](../assets/week4/week4(2).png)

#### Analisis:  
Perintah ini digunakan untuk mengetahui server DNS otoritatif dari domain *mit.edu*. Hasil menunjukkan beberapa nama server DNS yang bertanggung jawab terhadap domain tersebut.

---

### 3.3 Ipconfig  

#### Perintah:
```bash
ipconfig /all
```

#### Hasil:
![Ipconfig](../assets/week4/week4(3).png)

#### Analisis:  
Perintah ini menampilkan informasi jaringan pada perangkat, termasuk alamat IPv4 dan DNS server. Informasi ini penting untuk mengetahui alamat IP perangkat serta DNS server yang digunakan dalam proses penerjemahan domain.

---

### 3.4 DNS Cache  

#### Perintah:
```bash
ipconfig /displaydns
```

#### Hasil:
![DNS cache](../assets/week4/week4(4).png)

#### Analisis:  
Perintah ini digunakan untuk menampilkan cache DNS yang tersimpan pada komputer. Cache ini memungkinkan akses ke domain menjadi lebih cepat karena tidak perlu melakukan query ulang ke DNS server.

---

### 3.5 Wireshark DNS Capture  

#### Langkah:
1. Melakukan flush DNS cache  
2. Menjalankan Wireshark  
3. Mengakses website `http://www.ietf.org`  
4. Menghentikan capture  
5. Menggunakan filter `dns`  

#### Hasil Capture:
![DNS request](../assets/week4/week4(5).png)  
![DNS response](../assets/week4/week4(6).png)  

#### Analisis:  
Terlihat paket DNS request dan DNS response. DNS request ditunjukkan oleh paket dengan label *Standard query A www.ietf.org*, yang merupakan permintaan untuk mendapatkan alamat IP dari domain tersebut.

DNS response ditunjukkan oleh paket *Standard query response A www.ietf.org* yang berisi jawaban berupa alamat IP yaitu **104.16.44.99** dan **104.16.45.99**.

Kedua paket memiliki ID yang sama (0x129f), yang menunjukkan bahwa response merupakan balasan langsung dari request yang dikirim oleh client.

---

### 3.6 Analisis TCP SYN pada Wireshark  

#### Langkah:
1. Menggunakan filter berikut untuk menampilkan paket TCP SYN:
   ```bash
   tcp.flags.syn == 1
   ```
2. Mengidentifikasi paket TCP dengan flag **[SYN]** (bukan SYN, ACK)  
3. Memilih paket dengan tujuan ke alamat IP hasil DNS sebelumnya  
4. Mengamati detail paket pada bagian Transmission Control Protocol  

#### Hasil Capture:
![cari TCP SYN](../assets/week4/week4(7).png)

#### Analisis:  
Berdasarkan hasil capture Wireshark, terlihat paket TCP dengan flag **SYN** yang dikirimkan dari client ke server dengan alamat IP **2606:4700::6810:2d63** melalui port **443**.

Paket ini merupakan tahap awal dalam proses *three-way handshake* pada protokol TCP, yang menandakan bahwa client mulai membangun koneksi ke server tujuan.

Alamat IP tujuan pada paket TCP sesuai dengan alamat IP yang diperoleh dari DNS response, sehingga dapat disimpulkan bahwa DNS berperan dalam menentukan alamat server sebelum koneksi TCP dilakukan.

---

## 4. Analisis Pertanyaan  

### 1. DNS menggunakan protokol apa?  
DNS menggunakan protokol **UDP**.

### 2. Port yang digunakan?  
DNS menggunakan **port 53**.

### 3. Apakah DNS request memiliki jawaban?  
Tidak, DNS request hanya berisi pertanyaan.

### 4. Apakah DNS response memiliki jawaban?  
Ya, DNS response berisi jawaban berupa alamat IP.

### 5. Apakah IP pada TCP sama dengan DNS response?  
Ya, karena DNS digunakan untuk menentukan alamat tujuan sebelum koneksi TCP dilakukan.

---

## 5. Kesimpulan  
DNS berfungsi untuk menerjemahkan nama domain menjadi alamat IP. Proses ini terjadi sebelum komunikasi HTTP dilakukan. Berdasarkan hasil praktikum, dapat diamati bahwa setelah DNS memberikan alamat IP, client akan melanjutkan proses koneksi menggunakan protokol TCP ke server tujuan.