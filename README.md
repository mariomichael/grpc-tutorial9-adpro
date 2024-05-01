## REFLECTION

### 1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?
Perbedaan utama antara metode unary, server streaming, dan bi-directional streaming RPC terletak pada jumlah dan arah komunikasi antara client dan server. Pada Unary RPC terjadi komunikasi satu kali antara client dan server. Di sini client akan mengirim satu permintaan dan menerima satu response. Metode ini biasa dipakai untuk transaksi sederhana seperti pengambilan data yang tidak membutuhkan pertukaran data lanjutan. Sedangkan pada server streaming, server akan menerima satu permintaan kemudian bisa mengirimkan sekumpulan response. Hal ini cocok jika data perlu dikirim secara kontinu dari server ke client/ Sedangkan untuk bi-directional streaming, client dan server dapat saling mengirim dan menerima data secara bebas dalam sesi yang sama, jadi terjadi komunikasi dua arah. Hal ini biasanya cocok untuk aplikasi yang memerlukan interaksi kontinu dan real-time.

### 2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?
Pertimbangan keamanan yang terlibat dalam pengimplementasian gRPC di Rust untuk autentikasi adalah pastikan pengguna terverifikasi menggunakan mekanisme seperti token JWT atau OAuth sebelum memproses panggilan RPC. Sedangkan untuk otorisasi, tentukan hak akses yang tepat untuk setiap pengguna. Pastikan setiap pengguna hanya dapat mengakses data yang sesuai dengan peran mereka. Sedangkan untuk enkripsi data, gunakan TLS/SSL untuk enkripsi data yang dikirim melalui jaringan agar data sensitif terlindungi dari akses yang tidak sah selama transmisi.

### 3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?
Tantangan potensial yang mungkin muncul saat menangani bidirectional streaming di Rust gRPC pada skenario aplikasi chat adalah manajemen state dimana server harus dipertahankan keadaannya dari antara berbagai pesan yang dikirim dan diterima yang sangat kompleks. Selain itu juga ada tantangan untuk memastikan bahwa sistem dapat mengangani interupsi dan kesalahan jaringan tanpa kehilangan data. Terakhir, ada tantangan untuk menangani beban tinggi jika banyak pesan yang masuk dan keluar secara terus-menerus tanpa adanya penurunan performa aplikasi.

### 4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?
Kelebihan menggunakan `tokio_stream::wrappers::ReceiverStream` untuk streaming response di layanan gRPC Rust adalah adanya efisiensi pengolahan stream dengan memanfaatkan fitur asynchronous yang kuat dari Tokio. Selain itu penggunaannya memungkinkan pengolahan data yang masuk secara real-time memiliki overhead minimal. Sedangkan untuk kekurangannya, adanya kompleksitas sehingga diperlukan pemahaman lebih mengenai asynchronous programming dan handling stream dan penggunaannya dapat memakan sumber daya memori dan CPU yang intensif tergantung beban data.

### 5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?
Kode gRPC Rust bisa disusun untuk memudahkan penggunaan ulang kode dan modularitas dengan penggunaan traits dan modul dimana harus mendefinisikan fungsionalitas yang umum dalam traits dan mengatur kode dalam modul yang jelas untuk meningkatkan reusability. Selain itu bisa dilakukan pengimplementasian middleware atau interceptor untuk logika yang bisa digunakan beberapa kali. Terakir, bisa memanfaatkan makro Rust untuk menghasilkan kode boilerplate yang bisa digunakan kembali untuk mempercepat pengembangan.

### 6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?
Langkah tambahan yang mungkin diperlukan untuk menangani logika pemrosesan pembayaran yang lebih kompleks adalah penambahan validasi input data lanjutan untuk memastikan data input valid. Selain itu diperlukan pengintegrasian dengan sistem pembayaran atau bank (pihak ketiga). Dapat juga dilakukan penambahan logika untuk melakukan konfirmasi pembayaran berdasarkan response dari sistem pembayaran. Hal terakhir yang tak kalah penting adalah pengimplementasian enkripsi dan keamanan tambahan untuk melindungi data sensitif.

### 7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?
Dampak adopsi gRPC pada kasus tersebut adalah terjadinya peningkatan performa karena terjadinya peningkatan efisiensi komunikasi antar-servis dengan adanya header compression dan multiplexing. Selain itu adanya interoperability yang lebih baik sehingga semakin mudah intuk melakukan integrasi antarsistem dengan basis teknologi yang berbeda. Terakhir, akan ada desain yang lebih terstruktur dan ketat karena adanya validasi tipe di berbagai platform.

### 8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?
Kelebihan menggunakan HTTP/2 dibanding HTTP/1.1 atau HTTP/1 adalah adanya kemampuan pengiriman beberapa request dan response secara simultan dalam satu koneksi sehingga mengurangi latensi (multiplexing). Selain itu HTTP/2 mendukung kompresi header dan server push untuk mengurangi overhead koneksi dan memungkinkan server mengirim data ke client sebelum diminta untuk meningkatkan efisiensi. Sedangkan untuk kekurangannya, adanya kompleksitas yang lebih tinggi untuk melakukan konfigurasi dan pengelolaan HTTP/2 dibanding HTTP/1.1. Kekurangan lainnya adalah tidak semua perangkat lunak mendukung HTTP/2 secara utuh sehingga penggunaan HTTP/2 lebih terbatas.

### 9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?
Model request-responsenya berbeda dimana model request-response dari REST biasanya bersifat stateless dan cocok untuk kasus penggunaan, pengambilan, atau modifikasi sumber daya. Namun REST kurang efisien untuk komunikasi real-time karena setiap operasi memerlukan request terpisah. Sedangkan untuk bidirectional streaming gRPC, dimungkinkan komunikasi berkelanjutan dan real-time antara client dan server. Hal ini akan meningkatkan interaktivitas dan responsivitas aplikasi untuk aplikasi dengan fitur utama seperti chat, streaming, atau gaming.

### 10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?
Pendekatan berbasis skema gRPC menghasilkan ketepatan dan konsistensi karena skema yang ketat menjamin bahwa data yang dikirimkan memenuhi definisi yang jelas, yang mengurangi kesalahan runtime. Selain itu, protokol buffer dalam format biner akan menghasilkan payload yang lebih kecil dan diproses lebih cepat dibandingkan JSON, sehingga mengurangi beban aplikasi dan meningkatkan efisiensi. JSON, di sisi lain, tidak fleksibel seperti JSON, yang dapat digunakan dalam berbagai bahasa pemrograman tanpa dicompile terlebih dahulu. Ini menunjukkan bahwa JSON lebih cocok untuk API publik yang membutuhkan fleksibilitas data untuk pelanggan.