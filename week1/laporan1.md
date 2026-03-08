# Tugas Praktikum Jaringan Komputer  
## Week 1

**Nama:** Yustinus Yendy S.A  
**NIM:** 103072400065  

## 1. Instalasi Software
Langkah pertama adalah mendownload dan menginstal **Wireshark** dan **Python** yang sudah disediakan di modul praktikum. Jika tidak tersedia di modul, software tersebut juga dapat diunduh melalui website resminya.

## 2. Menjalankan Wireshark
Setelah proses instalasi selesai, langkah selanjutnya adalah membuka aplikasi **Wireshark**.
Kemudian memilih **interface Wi-Fi**, karena koneksi internet yang digunakan berasal dari jaringan Wi-Fi. Interface ini digunakan untuk menangkap lalu lintas paket data yang melewati jaringan tersebut.

![Tampilan Wireshark](../assets/week1/week1(1).png)


## 3. Tampilan Utama Wireshark
Setelah memilih interface, akan muncul tampilan utama Wireshark yang terdiri dari beberapa bagian utama, yaitu:
### Command Menu
Menu utama yang berisi berbagai perintah untuk menjalankan fitur pada Wireshark.
### Packet Listing Window
Bagian yang menampilkan daftar paket yang berhasil ditangkap oleh Wireshark.
### Packet Details Window
Bagian yang menampilkan informasi detail dari paket yang dipilih.
### Packet Contents Window
Bagian yang menampilkan isi paket dalam bentuk **hexadecimal** maupun **ASCII**.
### Packet Display Filter Field
Kolom yang digunakan untuk melakukan penyaringan paket berdasarkan protokol tertentu.

![Tampilan Utama Wireshark](../assets/week1/week1(2).png)

## 4. Fitur Capture pada Wireshark
Beberapa fitur penting yang digunakan dalam proses capture paket yaitu:
- **Start Capturing Packet**  
  Digunakan untuk memulai proses penangkapan paket jaringan.
![Fitur Stop Capture](../assets/week1/week1(3).png)

- **Stop Capturing Packet**  
  Digunakan untuk menghentikan proses penangkapan paket.
![Fitur Capture](../assets/week1/week1(4).png)

Selain itu terdapat juga fitur **filter** yang digunakan untuk memilah paket berdasarkan protokol tertentu seperti:
- HTTP
- UDP
- TCP
- SSDP
- dan lain sebagainya.
![Filter tcp](../assets/week1/week1(6).png)

## 5. Menghasilkan Traffic Jaringan
Langkah berikutnya adalah membuka **link yang terdapat pada modul 2 poin 2.4 urutan ke-6**. Tujuan dari langkah ini adalah untuk menghasilkan lalu lintas jaringan yang nantinya dapat ditangkap oleh Wireshark.
Setelah membuka link tersebut, akan muncul halaman website yang menghasilkan traffic jaringan.

![Menghasilkan Traffic Jaringan](../assets/week1/week1(7).png)
![Menghasilkan Traffic Jaringan](../assets/week1/week1(8).png)
## 6. Analisis Paket HTTP
Setelah menghasilkan traffic jaringan, langkah selanjutnya adalah kembali ke aplikasi **Wireshark**.
1. Menghentikan proses capture dengan menekan **Stop Capturing Packet**.
2. Menggunakan fitur **filter** dengan mengetik:
3. Memilih salah satu paket **HTTP** yang memiliki informasi **GET Request**.

Kemudian melihat bagian **Source Address** dari paket tersebut.
![filter http](../assets/week1/week1(9).png)

## 7. Membandingkan IP Address
Langkah selanjutnya adalah membuka **Command Prompt (CMD)** dan mengetik perintah:
Setelah itu membandingkan **Source Address** pada Wireshark dengan **IPv4 Address** yang muncul pada CMD.
Hasil yang didapatkan menunjukkan bahwa alamat IP pada Wireshark sama dengan alamat IPv4 pada CMD, yaitu:
Hal ini menunjukkan bahwa paket **HTTP GET** tersebut berasal dari perangkat yang sedang digunakan.
![source wireshark](../assets/week1/week1(10).png)
![source cmd](../assets/week1/week1(11).png)

## Kesimpulan
Dari praktikum ini dapat dipahami bahwa **Wireshark** dapat digunakan untuk menangkap dan menganalisis paket data yang melewati jaringan. Dengan menggunakan fitur filter, pengguna dapat memfokuskan analisis pada protokol tertentu seperti HTTP.
Selain itu, melalui perbandingan **Source Address** pada Wireshark dengan **IPv4 Address** pada CMD, dapat diketahui bahwa paket yang tertangkap memang berasal dari perangkat yang sedang digunakan.
