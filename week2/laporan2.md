# Laporan Praktikum Jaringan Komputer

## Modul 3 – HTTP

**Nama:** Yustinus Yendy
**NIM:** 103072400065
**Kelas:** IF-04-02

---

# Tujuan

Memahami cara kerja protokol **HTTP** dengan menganalisis komunikasi antara browser dan server menggunakan **Wireshark**.

---

# Percobaan

## 1. Basic HTTP GET / Response

### Langkah

1. Jalankan Wireshark dan gunakan filter: http
2. Mulai capture paket.
3. Buka browser dan akses:

```
http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file1.html
```

4. Hentikan capture setelah halaman muncul.

### Hasil

Terlihat dua pesan utama:
**HTTP GET (Request)**
Browser meminta file dari server.
GET /wireshark-labs/HTTP-wireshark-file1.html

**HTTP Response**
Server mengirimkan file HTML sebagai respon.
HTTP/1.1 200 OK


## 2. HTTP Conditional GET
### Langkah
1. Bersihkan cache browser.
2. Start capture Wireshark.
3. Akses:
http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file2.html
4. Refresh halaman.
5. Stop capture.

### Hasil
Browser menggunakan header:
If-Modified-Since
Jika file tidak berubah server akan mengirim respon:
304 Not Modified
Ini digunakan untuk menghemat bandwidth.


## 3. Retrieving Long Documents
### Langkah
1. Start capture.
2. Buka:
http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file3.html
3. Stop capture.

### Hasil
Pada hasil capture paket di Wireshark terlihat bahwa browser mengirimkan request HTTP ke server untuk mengambil file HTML.
Request yang terlihat pada paket:
"GET /wireshark-labs/HTTP-wireshark-file3.html HTTP/1.1"
Server kemudian merespon dengan pesan:
"HTTP/1.1 200 OK"

File HTML yang dikirim oleh server memiliki ukuran cukup besar sehingga tidak dapat dikirim dalam satu paket TCP saja. Oleh karena itu file tersebut dikirim dalam beberapa segmen TCP yang kemudian digabungkan kembali oleh Wireshark.

Hal ini terlihat pada struktur paket berikut:
[3 Reassembled TCP Segments (4864 bytes)]
Hypertext Transfer Protocol
Line-based text data: text/html

Informasi tersebut menunjukkan bahwa respon HTTP terdiri dari beberapa segmen TCP yang direassemble menjadi satu pesan HTTP lengkap.


## 4. HTML dengan Embedded Objects
### Langkah
1. Start capture.
2. Akses:
http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file4.html
3. Stop capture.

### Hasil
Saat halaman HTML diakses, browser tidak hanya mengambil file HTML utama tetapi juga objek lain yang terdapat di dalamnya seperti gambar.

Pada hasil capture Wireshark terlihat beberapa request HTTP:

GET /wireshark-labs/HTTP-wireshark-file4.html  
GET /pearson.png  
GET /8E_cover_small.jpg  
GET /favicon.ico  


## 5. HTTP Authentication
### Langkah
1. Start capture.
2. Akses:
http://gaia.cs.umass.edu/wireshark-labs/protected_pages/HTTP-wireshark-file5.html
3. Login menggunakan:
username: wireshark-students
password: network
4. Stop capture.

### Hasil
Saat halaman yang dilindungi diakses, server pertama kali memberikan respon:
HTTP/1.1 401 Unauthorized

Hal ini menunjukkan bahwa halaman membutuhkan autentikasi.
Browser kemudian mengirimkan request kembali dengan header autentikasi:
Authorization: Basic xxxxxxxxx

Header tersebut berisi username dan password yang telah diencode menggunakan Base64.


# Kesimpulan

* HTTP digunakan untuk komunikasi antara browser dan web server.
* Browser mengirim request seperti **GET** untuk meminta resource.
* Server memberikan response seperti **200 OK** jika berhasil.
* Conditional GET memungkinkan browser menggunakan cache.
* File besar dikirim melalui beberapa segmen TCP.
* Setiap objek pada halaman web diambil melalui request HTTP yang berbeda.
* HTTP Authentication menggunakan encoding Base64 sehingga tidak aman tanpa HTTPS.

# Lampiran
![HTTP GET Request](../assets/week2/week2(1).png)
![HTTP Response 200 OK](../assets/week2/week1(2).png)
![Conditional GET](../assets/week1/week2(3).png)
![TCP Segment Response](../assets/week2/week1(4).png)
![Multiple HTTP GET](../assets/week1/week2(5).png)
![HTTP Authentication](../assets/week1/week2(6).png)
