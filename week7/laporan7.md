# Laporan Praktikum Jaringan Komputer

## Modul 6 – TCP

**Nama:** Yustinus Yendy S.A  
**NIM:** 103072400065  

## Tujuan
Memahami cara kerja komunikasi client-server menggunakan socket programming dengan protokol UDP dan TCP, serta mengimplementasikan pengiriman dan penerimaan data antara client dan server.


## 1. UDPClient.py

Program `UDPClient.py` berfungsi sebagai client dalam komunikasi jaringan menggunakan protokol UDP (User Datagram Protocol). Sesuai dengan konsep pada modul jaringan komputer, UDP merupakan protokol transport yang bersifat connectionless, artinya client tidak perlu membangun koneksi terlebih dahulu dengan server sebelum mengirim data.

Pada awal program, dilakukan import library `socket` yang menyediakan fungsi-fungsi untuk komunikasi jaringan. Library ini menjadi komponen utama dalam pembuatan aplikasi client-server karena memungkinkan pertukaran data antar perangkat melalui jaringan.

Selanjutnya, ditentukan alamat server dan port yang akan dituju. Pada kode ini, digunakan `127.0.0.1` yang merupakan alamat localhost, yaitu komputer itu sendiri, serta port `12000` sebagai endpoint komunikasi. Kombinasi antara IP address dan port ini digunakan untuk mengidentifikasi tujuan pengiriman data secara spesifik dalam jaringan.

Program kemudian membuat sebuah socket menggunakan perintah `socket(AF_INET, SOCK_DGRAM)`. Parameter `AF_INET` menunjukkan bahwa komunikasi menggunakan IPv4, sedangkan `SOCK_DGRAM` menandakan bahwa protokol yang digunakan adalah UDP. Berbeda dengan TCP, socket UDP tidak memerlukan proses koneksi seperti `connect()`, sehingga lebih sederhana dan cepat dalam pengiriman data.

Setelah socket dibuat, program meminta input dari user berupa kalimat dalam huruf kecil. Input ini akan menjadi data yang dikirimkan ke server. Sebelum dikirim, data tersebut diubah ke dalam format byte menggunakan metode `encode()`, karena komunikasi jaringan hanya dapat mengirimkan data dalam bentuk byte stream.

Pengiriman data dilakukan menggunakan fungsi `sendto()`, yang membutuhkan dua parameter, yaitu pesan dalam bentuk byte dan alamat tujuan (IP dan port server). Pada tahap ini, client langsung mengirimkan data tanpa memastikan apakah server sudah siap menerima atau tidak, yang merupakan karakteristik utama dari UDP.

Setelah mengirimkan pesan, client akan menunggu balasan dari server menggunakan fungsi `recvfrom()`. Fungsi ini menerima dua nilai, yaitu data yang dikirim oleh server dan alamat pengirim (server). Parameter `2048` menunjukkan ukuran maksimum buffer data yang dapat diterima dalam satu kali pembacaan.

Data yang diterima dari server masih dalam bentuk byte, sehingga perlu dikembalikan ke bentuk string menggunakan metode `decode()`. Hasilnya kemudian ditampilkan ke layar sebagai output dari proses komunikasi.

Terakhir, socket ditutup menggunakan `close()` untuk mengakhiri sesi komunikasi dan membebaskan resource yang digunakan. Penutupan ini penting agar tidak terjadi kebocoran resource pada sistem.

Secara keseluruhan, alur kerja `UDPClient.py` adalah menerima input dari user, mengirimkan data ke server tanpa koneksi, menunggu respon, lalu menampilkan hasil yang diterima. Proses ini mencerminkan model komunikasi client-server sederhana dengan menggunakan protokol UDP yang ringan dan cepat.
![UDPClient](../assets/week7/week7(1).png)

## 2. UDPServer.py

Program `UDPServer.py` berfungsi sebagai server dalam komunikasi jaringan menggunakan protokol UDP (User Datagram Protocol). Berbeda dengan client yang menginisiasi komunikasi, server memiliki peran utama untuk menerima permintaan (request) dari client, memprosesnya, dan mengirimkan kembali respon.

Pada awal program, dilakukan import library `socket` yang digunakan untuk membangun komunikasi jaringan. Library ini memungkinkan server untuk membuat endpoint yang dapat menerima dan mengirim data melalui jaringan.

Selanjutnya, ditentukan port server yaitu `12000`. Port ini berfungsi sebagai jalur komunikasi tempat server “mendengarkan” data yang masuk dari client. Tidak seperti client yang harus menentukan alamat tujuan, server cukup menentukan port dan melakukan binding agar siap menerima koneksi atau data yang masuk.

Server kemudian membuat socket menggunakan `socket(AF_INET, SOCK_DGRAM)`. Parameter `AF_INET` menunjukkan penggunaan IPv4, sedangkan `SOCK_DGRAM` menandakan bahwa server menggunakan protokol UDP. Karena UDP bersifat connectionless, server tidak perlu melakukan proses `listen()` atau `accept()` seperti pada TCP.

Setelah socket dibuat, server melakukan binding dengan perintah `bind(('', serverPort))`. Tanda kosong `''` berarti server akan menerima data dari semua alamat IP yang tersedia pada mesin tersebut. Dengan binding ini, server secara resmi terhubung dengan port `12000` dan siap menerima data dari client.

Program kemudian mencetak pesan "The server is ready to receive" sebagai indikator bahwa server sudah aktif dan menunggu data masuk.

Server berjalan dalam loop tak terbatas menggunakan `while True`. Hal ini penting karena server harus selalu aktif dan siap melayani banyak permintaan dari client tanpa berhenti setelah satu kali proses.

Di dalam loop, server menerima data menggunakan fungsi `recvfrom(2048)`. Fungsi ini mengembalikan dua nilai, yaitu pesan yang diterima dalam bentuk byte dan alamat client yang mengirimkan pesan tersebut. Parameter `2048` menunjukkan ukuran maksimum buffer data yang dapat diterima.

Pesan yang diterima kemudian diubah dari byte menjadi string menggunakan `decode()`. Setelah itu, server memproses pesan dengan mengubah seluruh huruf menjadi kapital menggunakan metode `upper()`. Proses ini merupakan contoh sederhana dari pengolahan data pada server.

Setelah pesan dimodifikasi, server mengubah kembali data tersebut ke dalam bentuk byte menggunakan `encode()`, lalu mengirimkannya kembali ke client menggunakan fungsi `sendto()`. Alamat tujuan pengiriman diambil dari `clientAddress`, yaitu alamat client yang sebelumnya mengirim pesan.

Karena UDP tidak memiliki koneksi tetap, server tidak perlu menutup koneksi setelah mengirim respon. Server akan terus berjalan dan kembali ke awal loop untuk menunggu pesan berikutnya dari client lain atau client yang sama.

Secara keseluruhan, alur kerja `UDPServer.py` adalah menerima data dari client, memproses isi pesan, lalu mengirimkan kembali hasilnya tanpa melalui proses koneksi. Hal ini menunjukkan karakteristik utama UDP yang sederhana, cepat, dan tidak memiliki mekanisme kontrol koneksi.
![UDPServer](../assets/week7/week7(2).png)

## 3. TCPClient.py

Program `TCPClient.py` berfungsi sebagai client dalam komunikasi jaringan menggunakan protokol TCP (Transmission Control Protocol). Berbeda dengan UDP, TCP bersifat connection-oriented, artinya sebelum melakukan pertukaran data, client harus terlebih dahulu membangun koneksi dengan server.

Pada awal program, dilakukan import library `socket` yang menyediakan fungsi untuk komunikasi jaringan. Library ini memungkinkan client untuk membuat koneksi dan bertukar data dengan server melalui protokol TCP.

Selanjutnya, ditentukan alamat server dan port tujuan. Pada kode ini digunakan `localhost` atau `127.0.0.1` sebagai alamat server, yang berarti komunikasi dilakukan pada komputer yang sama, serta port `12000` sebagai endpoint komunikasi.

Program kemudian membuat socket menggunakan `socket(AF_INET, SOCK_STREAM)`. Parameter `AF_INET` menunjukkan penggunaan IPv4, sedangkan `SOCK_STREAM` menandakan bahwa protokol yang digunakan adalah TCP. Berbeda dengan UDP, socket TCP membutuhkan koneksi sebelum dapat digunakan untuk mengirim data.

Setelah socket dibuat, client melakukan koneksi ke server menggunakan fungsi `connect((serverName, serverPort))`. Pada tahap ini terjadi proses pembentukan koneksi antara client dan server, yang dalam konsep TCP dikenal sebagai handshake. Koneksi ini memastikan bahwa kedua pihak siap untuk melakukan pertukaran data secara reliable.

Setelah koneksi berhasil, program meminta input dari user berupa kalimat. Input ini akan dikirim ke server sebagai data utama. Sebelum dikirim, data diubah ke dalam bentuk byte menggunakan metode `encode()`, karena komunikasi jaringan dilakukan dalam format byte stream.

Pengiriman data dilakukan menggunakan fungsi `send()`. Berbeda dengan UDP yang menggunakan `sendto()`, pada TCP tidak perlu menyertakan alamat tujuan karena koneksi sudah terbentuk sebelumnya melalui proses `connect()`.

Setelah mengirim data, client menunggu respon dari server menggunakan fungsi `recv(1024)`. Parameter `1024` menunjukkan ukuran maksimum buffer data yang dapat diterima. TCP menjamin bahwa data yang diterima akan lengkap dan berurutan sesuai dengan data yang dikirim oleh server.

Data yang diterima masih dalam bentuk byte, sehingga perlu dikonversi kembali menjadi string menggunakan metode `decode()`. Hasilnya kemudian ditampilkan ke layar sebagai output dari komunikasi antara client dan server.

Terakhir, koneksi ditutup menggunakan `close()`. Penutupan ini penting untuk mengakhiri sesi komunikasi dan membebaskan resource yang digunakan oleh socket.

Secara keseluruhan, alur kerja `TCPClient.py` adalah membangun koneksi dengan server, mengirim data, menerima respon, lalu menutup koneksi. Proses ini mencerminkan karakteristik utama TCP yang lebih terstruktur dan reliable dibandingkan UDP karena adanya mekanisme koneksi dan pengiriman data yang terjamin.
![TCPClient](../assets/week7/week7(3).png)

## 4. TCPServer.py

Program `TCPServer.py` berfungsi sebagai server dalam komunikasi jaringan menggunakan protokol TCP (Transmission Control Protocol). Berbeda dengan UDP, pada TCP server harus menangani koneksi yang dibangun oleh client sebelum melakukan pertukaran data.

Pada awal program, dilakukan import library `socket` yang digunakan untuk membangun komunikasi jaringan. Library ini memungkinkan server untuk membuat endpoint yang dapat menerima koneksi dari client.

Selanjutnya, ditentukan port server yaitu `12000`. Port ini digunakan sebagai jalur komunikasi tempat server menerima permintaan koneksi dari client.

Server kemudian membuat socket menggunakan `socket(AF_INET, SOCK_STREAM)`. Parameter `AF_INET` menunjukkan penggunaan IPv4, sedangkan `SOCK_STREAM` menandakan bahwa protokol yang digunakan adalah TCP. Berbeda dengan UDP, socket TCP membutuhkan mekanisme koneksi yang lebih kompleks.

Setelah socket dibuat, server melakukan binding dengan perintah `bind(('', serverPort))`. Tanda kosong `''` berarti server akan menerima koneksi dari semua alamat IP yang tersedia pada mesin tersebut. Dengan binding ini, server terhubung ke port `12000` dan siap menerima koneksi.

Server kemudian menjalankan fungsi `listen(1)` untuk mulai mendengarkan permintaan koneksi dari client. Angka `1` menunjukkan jumlah maksimum antrian koneksi yang dapat ditangani secara bersamaan. Pada tahap ini, server berada dalam kondisi menunggu (listening state).

Program mencetak pesan "The server is ready to receive" sebagai indikator bahwa server telah aktif dan siap menerima koneksi dari client.

Server berjalan dalam loop tak terbatas menggunakan `while True`, sehingga dapat melayani banyak client secara berulang tanpa harus dijalankan ulang.

Di dalam loop, server menerima koneksi dari client menggunakan fungsi `accept()`. Fungsi ini akan menghasilkan dua nilai, yaitu `connectionSocket` sebagai socket khusus untuk komunikasi dengan client tersebut, dan `addr` sebagai alamat client. Hal ini menunjukkan bahwa pada TCP, setiap client memiliki jalur komunikasi sendiri yang terpisah.

Setelah koneksi terbentuk, server menerima data dari client menggunakan `recv(1024)` dan mengubahnya ke bentuk string dengan `decode()`. Data yang diterima kemudian diproses dengan mengubah semua huruf menjadi kapital menggunakan metode `upper()`.

Hasil pemrosesan tersebut kemudian diubah kembali ke bentuk byte menggunakan `encode()` dan dikirimkan ke client melalui `connectionSocket.send()`.

Setelah proses komunikasi selesai, server menutup koneksi dengan client menggunakan `connectionSocket.close()`. Meskipun koneksi dengan client ditutup, server utama tetap berjalan dan kembali ke awal loop untuk menunggu koneksi berikutnya.

Secara keseluruhan, alur kerja `TCPServer.py` adalah menerima koneksi dari client, menerima dan memproses data, mengirimkan respon, lalu menutup koneksi. Proses ini mencerminkan karakteristik TCP yang connection-oriented, di mana setiap komunikasi harus melalui proses pembentukan dan penutupan koneksi secara terstruktur.
![TCPServer](../assets/week7/week7(4).png)

## Output Terminal
### UDP
![Output](../assets/week7/week7(5).png)

### TCP
![Output](../assets/week7/week7(6).png)

## Kesimpulan

Berdasarkan hasil implementasi dan pengujian program socket programming menggunakan UDP dan TCP, dapat disimpulkan bahwa kedua protokol memiliki mekanisme komunikasi client-server yang berbeda secara signifikan. UDP bekerja dengan pendekatan connectionless, di mana client dapat langsung mengirim data ke server tanpa perlu membangun koneksi terlebih dahulu, sehingga prosesnya menjadi lebih cepat dan sederhana, namun memiliki kelemahan karena tidak menjamin data akan sampai ke tujuan maupun urutan pengirimannya. Sebaliknya, TCP menggunakan pendekatan connection-oriented yang mengharuskan adanya proses koneksi antara client dan server sebelum pertukaran data dilakukan, sehingga komunikasi menjadi lebih terstruktur, aman, dan reliable karena adanya jaminan pengiriman serta pengurutan data. Melalui percobaan ini, dapat dipahami bahwa pemilihan antara UDP dan TCP harus disesuaikan dengan kebutuhan aplikasi, apakah lebih mengutamakan kecepatan dan efisiensi atau keandalan dan integritas data dalam proses komunikasi jaringan.