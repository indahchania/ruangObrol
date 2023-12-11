# 1. Jelaskan dengan disertai penjelasan baris kode terkait perbedaan fungsi socket.on yang ada pada file index.js di folder src dan file chat.js pada folder public/js!
**Perbedaan Fungsi `socket.on` pada `index.js` dan `chat.js`**

**File: `index.js` (Server-Side - src/utils/messages.js)**
```javascript
socket.on('pesan', (message) => {
    // ... (logika untuk menangani pesan)
});

socket.on('locationMessage', (message) => {
    // ... (logika untuk menangani pesan lokasi)
});

socket.on('roomData', ({ room, users }) => {
    // ... (logika untuk menangani data ruangan)
});
```

**File: `chat.js` (Client-Side - public/js/chat.js)**
```javascript
socket.on('pesan', (message) => {
    // ... (logika untuk menangani pesan pada sisi klien)
});

socket.on('locationMessage', (message) => {
    // ... (logika untuk menangani pesan lokasi pada sisi klien)
});

socket.on('roomData', ({ room, users }) => {
    // ... (logika untuk menangani data ruangan pada sisi klien)
});
```

**Penjelasan:**

1. **Fungsi `socket.on` pada `index.js` (Server-Side):**
   - Digunakan untuk menangani pesan (`pesan`) yang diterima dari klien (client).
   - Menangani pesan lokasi (`locationMessage`) yang diterima dari klien.
   - Menangani data ruangan (`roomData`) yang diterima dari klien.

2. **Fungsi `socket.on` pada `chat.js` (Client-Side):**
   - Digunakan untuk menangani pesan (`pesan`) yang diterima dari server.
   - Menangani pesan lokasi (`locationMessage`) yang diterima dari server.
   - Menangani data ruangan (`roomData`) yang diterima dari server.

**Kesimpulan:**
- Fungsi `socket.on` pada `index.js` (server) digunakan untuk menangani peristiwa yang terjadi di sisi server dan berhubungan dengan pengelolaan pesan, lokasi, dan data ruangan.
- Fungsi `socket.on` pada `chat.js` (client) digunakan untuk menangani peristiwa yang terjadi di sisi klien dan berhubungan dengan pemutakhiran antarmuka pengguna (UI) ketika pesan atau lokasi baru diterima, serta memperbarui data ruangan.

# 2. Pada saat anda melakukan proses chat seperti pada langkah 12 dan 13. Bukalah inspect pada browser anda. Lalu bukalah menu console. Lakukanlah proses chat dan investigasi apa yang ditampilkan pada console tersebut. Uraikan penjelasan anda dengan mengaitkannya ke baris kode yang menurut anda berhubungan dengan hal tersebut!
Pada proses chat di aplikasi ini, beberapa pesan log ditampilkan pada console browser. Berikut adalah penjelasan terkait setiap pesan log dan kaitannya dengan baris kode yang bersangkutan:

1. **Selamat Datang!**
    - Pesan Log:
        ```
        Object { username: "Admin", text: "Selamat datang!", createdAt: 1702266416982 }
        ```
    - Penjelasan:
        - Pesan ini muncul saat koneksi pertama ke WebSocket berhasil dilakukan (`io.on('connection', ...)`) pada server-side (index.js).
        - Terkait dengan baris kode:
            ```javascript
            socket.emit('pesan', generateMessage('Admin','Selamat datang!'))
            ```
            Pada baris ini, server mengirim pesan selamat datang kepada pengguna yang baru terkoneksi.

2. **Pesan Pengguna: "Halo"**
    - Pesan Log:
        ```
        Object { username: "indah", text: "halo", createdAt: 1702266423318 }
        ```
    - Penjelasan:
        - Pesan ini muncul saat pengguna dengan nama "indah" mengirim pesan "halo".
        - Terkait dengan baris kode:
            ```javascript
            socket.on('pesan', (message) => {
                // ... (logika untuk menangani pesan)
            });
            ```

3. **Pesan Pengguna: "Hai"**
    - Pesan Log:
        ```
        Object { username: "chania", text: "hai ", createdAt: 1702266426321 }
        ```
    - Penjelasan:
        - Pesan ini muncul saat pengguna dengan nama "chania" mengirim pesan "hai ".
        - Terkait dengan baris kode yang sama seperti poin sebelumnya.

4. **Pesan Berhasil Dikirim**
    - Pesan Log:
        ```
        Pesan berhasil dikirim chat.js:81:29
        ```
    - Penjelasan:
        - Pesan ini muncul setelah pengguna mengirim pesan dan proses pengiriman berhasil dilakukan.
        - Terkait dengan baris kode:
            ```javascript
            socket.emit('kirimPesan', pesan, (error) => {
                // ... (logika untuk menangani keberhasilan atau kesalahan pengiriman pesan)
            });
            ```

5. **Pesan Pengguna: "Apa Kabar?"**
    - Pesan Log:
        ```
        Object { username: "chania", text: "apa kabar?", createdAt: 1702266491737 }
        ```
    - Penjelasan:
        - Pesan ini muncul saat pengguna dengan nama "chania" mengirim pesan "apa kabar?".
        - Terkait dengan baris kode yang sama seperti poin sebelumnya.

6. **Pesan Berhasil Dikirim**
    - Pesan Log:
        ```
        Pesan berhasil dikirim
        ```
    - Penjelasan:
        - Pesan ini muncul setelah pengguna mengirim pesan dan proses pengiriman berhasil dilakukan.
        - Terkait dengan baris kode yang sama seperti poin sebelumnya.

# 3. Pada file chat.html dibagian akhir pada baris kode <script> terdapat penggunaan library mustache, moment dan qs. Jelaskan bagaimana ketiga library ini berfungsi dalam aplikasi yang anda buat, kaitkanlah dengan baris kode yang menurut anda berhubungan!
Pada bagian akhir file `chat.html`, terdapat penggunaan tiga library, yaitu Mustache.js, Moment.js, dan qs.js. Berikut adalah penjelasan tentang fungsi dan peran masing-masing library tersebut dalam aplikasi chat, serta kaitannya dengan baris kode yang bersangkutan:

## Mustache.js
Mustache.js adalah library templating yang memungkinkan penggunaan templat sederhana untuk merender data dinamis ke dalam HTML. Dalam konteks aplikasi obrolan ini, Mustache.js digunakan untuk membuat templat pesan, pesan lokasi, dan daftar anggota ruangan.

### Kaitan dengan Kode:
- **message-template:**
    ```html
    <script id="message-template" type ="text/html">
        <!-- Templat untuk merender pesan teks -->
    </script>
    ```
- **locationMessage-template:**
    ```html
    <script id="locationMessage-template" type ="text/html">
        <!-- Templat untuk merender pesan lokasi -->
    </script>
    ```
- **sidebar-template:**
    ```html
    <script id="sidebar-template" type ="text/html">
        <!-- Templat untuk merender daftar anggota ruangan -->
    </script>
    ```

## Moment.js
Moment.js adalah library untuk memanipulasi, menampilkan, dan memformat tanggal dan waktu dalam JavaScript. Dalam konteks aplikasi ini, Moment.js digunakan untuk memformat waktu pesan dan waktu lokasi menjadi format yang lebih mudah dibaca.

### Kaitan dengan Kode:
- **chat.js (Client-Side):**
    ```javascript
    moment(message.createdAt).format('H:mm')
    ```
    Penggunaan `moment` untuk memformat waktu pada pesan.

## qs.js
qs.js adalah library untuk mem-parsing dan mem-stringify query string dalam URL. Dalam konteks aplikasi chat, qs.js digunakan untuk mem-parsing parameter dari query string URL, khususnya untuk mendapatkan `username` dan `room` dari URL.

### Kaitan dengan Kode:
- **chat.js (Client-Side):**
    ```javascript
    const { username, room } = Qs.parse(location.search, { ignoreQueryPrefix: true })
    ```
    Menggunakan `Qs.parse` untuk mendapatkan nilai `username` dan `room` dari query string URL.

# 4. Bukalah chat.js, dan perhatikan bahwa ada beberapa baris kode yang telah ditandai dengan komentar elements, templates dan options. Jelaskan baris kode tersebut dan bagaimana kode tersebut berhubungan dengan file chat.html dan file index.html!
`chat.js` adalah skrip JavaScript yang bertanggung jawab untuk mengelola logika klien (client-side) dalam aplikasi obrolan. Berikut adalah penjelasan untuk beberapa baris kode yang telah ditandai dengan komentar "elements," "templates," dan "options":

```javascript
// Elements
const $messageForm = document.querySelector('#form-pesan')
const $messageFormInput = document.querySelector('input')
const $messageFormButton = document.querySelector('button')
const $sendLocationButton = document.querySelector('#kirim-lokasi')
const $messages = document.querySelector('#messages')

// Templates
const messageTemplate = document.querySelector('#message-template').innerHTML
const locationMessageTemplate = document.querySelector('#locationMessage-template').innerHTML
const sidebarTemplate = document.querySelector('#sidebar-template').innerHTML

// Options
const { username, room } = Qs.parse(location.search, { ignoreQueryPrefix: true })
```

1. **Elements:**
   - Variabel `$messageForm`, `$messageFormInput`, `$messageFormButton`, `$sendLocationButton`, dan `$messages` digunakan untuk menyimpan referensi ke elemen-elemen HTML yang diperlukan untuk interaksi dengan formulir dan tampilan pesan.
   - Kaitannya dengan `chat.html`: Variabel-variabel ini merujuk pada elemen-elemen yang ada dalam struktur HTML `chat.html`.

2. **Templates:**
   - Variabel `messageTemplate`, `locationMessageTemplate`, dan `sidebarTemplate` menyimpan templat HTML yang akan digunakan untuk merender pesan, pesan lokasi, dan daftar anggota ruangan.
   - Kaitannya dengan `chat.html`: Variabel-variabel ini merujuk pada elemen-elemen templat yang telah didefinisikan dalam struktur HTML `chat.html`.

3. **Options:**
   - Variabel `{ username, room }` menggunakan library qs.js untuk mem-parse parameter dari query string URL. Nilai-nilai ini akan digunakan untuk mengidentifikasi pengguna dan ruangan.
   - Kaitannya dengan `chat.html` dan `index.html`: Nilai-nilai ini diperoleh dari query string URL di `chat.html` setelah pengguna bergabung dan di-input dari formulir pada `index.html`.

# Kaitan dengan File HTML
- **Kaitan dengan `chat.html`:**
    - Variabel-variabel dan templat yang telah didefinisikan di `chat.js` merujuk pada elemen-elemen dan templat yang ada dalam struktur HTML `chat.html`.

- **Kaitan dengan `index.html`:**
    - Nilai `username` dan `room` diperoleh dari formulir di `index.html` setelah pengguna mengisi dan mengirim formulir.

Dengan demikian, file `chat.js` berfungsi sebagai penghubung antara logika klien (client-side) dengan elemen-elemen dan templat yang ada dalam file `chat.html` dan `index.html`.

# 5. Jelaskan fungsi file messages.js dan users.js dan bagaimana baris kode pada kedua file ini terhubung dengan index.js, chat.js dan kedua file html (chat.html dan index.html)

## messages.js
`messages.js` berisi dua fungsi yaitu `generateMessage` dan `generateLocationMessage`. Fungsi ini bertanggung jawab untuk menghasilkan objek pesan teks dan pesan lokasi dengan memasukkan informasi seperti username, teks, dan URL, serta mencatat waktu pesan dibuat.

- **generateMessage(username, text):**
  - Menerima username dan teks sebagai parameter.
  - Mengembalikan objek pesan teks dengan properti username, teks, dan createdAt (waktu dibuat).

- **generateLocationMessage(username, url):**
  - Menerima username dan URL sebagai parameter.
  - Mengembalikan objek pesan lokasi dengan properti username, URL, dan createdAt (waktu dibuat).

## users.js
`users.js` berisi logika terkait pengelolaan pengguna dalam aplikasi, seperti menambahkan pengguna, menghapus pengguna, mengambil informasi pengguna, dan mengambil pengguna dari suatu ruangan.

- **Tambah Pengguna (`tambahPengguna`):**
  - Menerima objek yang berisi id, username, dan room sebagai parameter.
  - Membersihkan dan memvalidasi data pengguna.
  - Memeriksa apakah pengguna dengan username yang sama sudah ada dalam ruangan yang sama.
  - Jika data valid, menambahkan pengguna ke dalam array `users` dan mengembalikan objek pengguna.

- **Hapus Pengguna (`hapusPengguna`):**
  - Menerima id pengguna sebagai parameter.
  - Mencari pengguna dengan id yang sesuai dan menghapusnya dari array `users`.
  - Mengembalikan objek pengguna yang dihapus.

- **Ambil Pengguna (`ambilPengguna`):**
  - Menerima id pengguna sebagai parameter.
  - Mengembalikan objek pengguna berdasarkan id.

- **Ambil Pengguna dari Room (`ambilPenggunaDariRoom`):**
  - Menerima nama ruangan sebagai parameter.
  - Membersihkan dan memvalidasi nama ruangan.
  - Mengembalikan array pengguna yang berada dalam ruangan yang sesuai.

## Kaitan dengan File `index.js`, `chat.js`, `chat.html`, dan `index.html`

- **Kaitan dengan `index.js`:**
  - Fungsi-fungsi dan objek yang diekspor dari `messages.js` dan `users.js` digunakan di `index.js` untuk mengelola pesan dan pengguna.

- **Kaitan dengan `chat.js`:**
  - Fungsi `generateMessage` dan `generateLocationMessage` dari `messages.js` digunakan untuk membuat pesan pada klien (client-side) di `chat.js`.
  - Fungsi-fungsi dari `users.js` seperti `tambahPengguna`, `hapusPengguna`, `ambilPengguna`, dan `ambilPenggunaDariRoom` digunakan untuk mengelola pengguna pada klien.

- **Kaitan dengan `chat.html` dan `index.html`:**
  - Fungsi-fungsi dari `users.js` digunakan pada sisi server (`index.js`) untuk mengelola data pengguna saat pengguna bergabung atau keluar dari ruangan.
  - Pesan-pesan dan data pengguna yang dihasilkan oleh fungsi-fungsi ini digunakan untuk merender antarmuka pengguna di `chat.html` dan `index.html`.

Dengan demikian, `messages.js` dan `users.js` berperan penting dalam mengelola pesan dan pengguna di aplikasi obrolan, dan fungsionalitas mereka terintegrasi dengan baik dalam `index.js`, `chat.js`, dan file HTML (`chat.html` dan `index.html`).

# 6. Bagaimana aplikasi ini bisa mengirimkan lokasi? Jelaskan apa yang terjadi dengan disertai penjelasan baris kode!
Aplikasi ini dapat mengirimkan lokasi pengguna menggunakan fitur geolokasi yang disediakan oleh browser. Proses ini terjadi dengan langkah-langkah berikut, didukung oleh baris kode di file `chat.js`:

1. **Pengecekan Dukungan Geolokasi:**
   - Sebelum mengirim lokasi, aplikasi melakukan pengecekan apakah browser mendukung geolokasi.
   - Jika tidak mendukung, aplikasi memberikan peringatan.

   ```javascript
   $sendLocationButton.addEventListener('click', (e) => {
       if (!navigator.geolocation) {
           return alert('Browser anda tidak mendukung Geolocation')
       }
       // ...
   })
   ```

2. **Mendapatkan Lokasi Pengguna:**
   - Jika browser mendukung geolokasi, aplikasi menggunakan `navigator.geolocation.getCurrentPosition` untuk mendapatkan posisi geografis pengguna.

   ```javascript
   navigator.geolocation.getCurrentPosition((position) => {
       // ...
   })
   ```

3. **Mengirim Lokasi ke Server Melalui WebSocket:**
   - Setelah mendapatkan posisi geografis pengguna, aplikasi menggunakan `socket.emit` untuk mengirimkan data lokasi ke server.

   ```javascript
   socket.emit('kirimLokasi', {
       latitude: position.coords.latitude,
       longitude: position.coords.longitude
   }, () => {
       $sendLocationButton.removeAttribute('disabled')
       console.log('Lokasi berhasil dikirim')
   })
   ```

4. **Penanganan di Server (index.js):**
   - Pada sisi server (`index.js`), aplikasi menanggapi pesan `'kirimLokasi'` dengan mengirimkan pesan lokasi ke seluruh pengguna dalam ruangan melalui `io.to(user.room).emit`.

   ```javascript
   socket.on('kirimLokasi', (coords, callback) => {
       const user = ambilPengguna(socket.id)
       io.to(user.room).emit('locationMessage',
           generateLocationMessage(user.username,
               `https://www.google.com/maps?q=${coords.latitude},${coords.longitude}`))
       callback()
   })
   ```

5. **Penanganan di Klien (chat.js):**
   - Klien menerima pesan lokasi melalui `socket.on('locationMessage', ...)`, kemudian menggunakan Mustache.js untuk merender pesan lokasi dan menambahkannya ke tampilan.

   ```javascript
   socket.on('locationMessage', (message) => {
       const html = Mustache.render(locationMessageTemplate, {
           username: message.username,
           url: message.url,
           createdAt: moment(message.createdAt).format('H:mm')
       })
       $messages.insertAdjacentHTML('beforeend', html)
   })
   ```

Dengan cara ini, lokasi pengguna dikirimkan dari klien ke server, dan kemudian diteruskan ke seluruh pengguna dalam ruangan, sehingga semua orang di ruangan dapat melihat lokasi pengguna tersebut.

# 7. Kenapa aplikasi ini dijalankan menggunakan perintah npm run dev bukan menggunakan perintah node diikuti nama file seperti pada jobsheet-jobsheet sebelumnya? Coba juga jalankan aplikasi menggunakan perintah npm run start, investigasi apa yang terjadi dan apa yang membedakannya dengan npm run dev?
Aplikasi ini menggunakan dua skrip yang didefinisikan di dalam berkas `package.json` untuk menjalankan server:

1. **npm run start:**
   - Menjalankan server menggunakan perintah `node src/index.js`.
   - Tidak menggunakan nodemon, yang artinya server tidak akan restart secara otomatis setiap kali ada perubahan pada berkas kode.

2. **npm run dev:**
   - Menjalankan server menggunakan perintah `nodemon src/index.js`.
   - Menggunakan nodemon, yang memungkinkan server untuk restart secara otomatis setiap kali ada perubahan pada berkas kode.

Perbedaan antara `npm run start` dan `npm run dev` terletak pada fungsionalitas nodemon:

- **`npm run start`:**
  - Server akan berjalan satu kali, dan tidak akan melakukan restart otomatis meskipun ada perubahan pada berkas kode.
  - Cocok untuk digunakan di lingkungan produksi atau ketika tidak diperlukan fitur restart otomatis pada saat pengembangan.

- **`npm run dev`:**
  - Server akan berjalan dengan nodemon, sehingga akan melakukan restart otomatis setiap kali ada perubahan pada berkas kode.
  - Cocok untuk digunakan pada saat pengembangan (development) agar memudahkan proses pengujian dan pengembangan tanpa perlu restart manual setiap kali ada perubahan.

Jika menjalankan aplikasi menggunakan `npm run start`, server akan berjalan satu kali tanpa fitur restart otomatis. Sebaliknya, jika menggunakan `npm run dev`, server akan terus berjalan dengan nodemon, dan restart otomatis akan terjadi setiap kali ada perubahan pada berkas kode.

# 8. Selain socket.on, fungsi socket apa lagi yang digunakan dalam aplikasi ini. Silakan telusuri dan jelaskan pendapat anda disertai dengan baris kode!
Selain `socket.on`, dalam aplikasi ini juga digunakan fungsi `socket.emit`. Berikut adalah penjelasan singkat dan contoh penggunaan kedua fungsi tersebut:

1. **`socket.on`**: Fungsi ini digunakan untuk mendengarkan (listen) pesan atau peristiwa tertentu dari sisi klien atau server.

   Contoh penggunaan di `chat.js`:
   ```javascript
   socket.on('pesan', (message) => {
       // Logika penanganan pesan
       console.log(message);
       // ...
   });
   ```

2. **`socket.emit`**: Fungsi ini digunakan untuk mengirimkan (emit) pesan atau peristiwa tertentu dari sisi klien atau server.

   Contoh penggunaan di `chat.js`:
   ```javascript
   socket.emit('kirimPesan', pesan, (error) => {
       // Logika penanganan setelah pesan terkirim
       // ...
   });
   ```

   Contoh penggunaan di `chat.html`:
   ```javascript
   socket.emit('join', { username, room }, (error) => {
       // Logika penanganan setelah pengguna bergabung
       if (error) {
           alert(error);
           location.href = '/';
       }
   });
   ```

   Contoh penggunaan di `index.js`:
   ```javascript
   socket.emit('pesan', generateMessage('Admin', 'Selamat datang!'));
   ```

   Dalam contoh di atas, `socket.on` digunakan untuk mendengarkan pesan atau peristiwa seperti `'pesan'`, `'kirimPesan'`, dan `'join'`. Sementara `socket.emit` digunakan untuk mengirim pesan atau peristiwa seperti `'pesan'` dan `'join'`.

Kedua fungsi ini memungkinkan komunikasi dua arah antara sisi klien dan server, memungkinkan pertukaran informasi secara real-time dalam aplikasi chat ini.

# 9. Jelaskan terkait ini real-time bidirectional event-based communication disertai penjelasan baris kode sesuai aplikasi yang anda buat!
Real-time bidirectional event-based communication mengacu pada kemampuan aplikasi untuk mentransmisikan data secara langsung antara sisi klien dan server dalam waktu nyata. Komunikasi ini bersifat dua arah, yang berarti baik klien maupun server dapat menginisiasi pengiriman data. Model ini sangat berguna dalam konteks aplikasi yang memerlukan pembaruan cepat dan interaktif, seperti aplikasi obrolan yang dibuat dalam contoh ini.

Di aplikasi obrolan ini, Socket.IO digunakan sebagai teknologi untuk mencapai real-time bidirectional event-based communication. Berikut adalah penjelasan baris kode yang relevan dengan konsep ini:

1. **Server (index.js):**
   - Pada sisi server, `io.on('connection', ...)` digunakan untuk menanggapi setiap koneksi baru dari klien. Setelah terjadi koneksi, server dapat mendengarkan dan mengirim pesan secara real-time.

     ```javascript
     io.on('connection', (socket) => {
         // ...
         socket.on('join', (options, callback) => {
             // Logika pengelolaan pengguna yang bergabung
             // ...
         });

         socket.on('kirimPesan', (pesan, callback) => {
             // Logika pengiriman pesan ke semua pengguna dalam ruangan
             // ...
         });

         socket.on('kirimLokasi', (coords, callback) => {
             // Logika pengiriman lokasi ke semua pengguna dalam ruangan
             // ...
         });
         // ...
     });
     ```

2. **Klien (chat.js):**
   - Pada sisi klien, `socket.emit` digunakan untuk mengirim pesan atau peristiwa ke server, dan `socket.on` digunakan untuk mendengarkan pesan atau peristiwa dari server.

     ```javascript
     // Mengirim pesan teks dari klien ke server
     $messageForm.addEventListener('submit', (e) => {
         e.preventDefault();
         socket.emit('kirimPesan', pesan, (error) => {
             // Logika penanganan setelah pesan terkirim
             // ...
         });
     });

     // Mendengarkan pesan teks dari server dan merendernya di antarmuka pengguna
     socket.on('pesan', (message) => {
         // Logika penanganan pesan
         // ...
     });

     // Mengirim lokasi dari klien ke server
     $sendLocationButton.addEventListener('click', (e) => {
         socket.emit('kirimLokasi', { latitude, longitude }, () => {
             // Logika penanganan setelah lokasi terkirim
             // ...
         });
     });

     // Mendengarkan lokasi dari server dan merendernya di antarmuka pengguna
     socket.on('locationMessage', (message) => {
         // Logika penanganan pesan lokasi
         // ...
     });
     ```

Dengan Socket.IO, komunikasi real-time terjadi melalui peristiwa dan pesan yang diemit dan didengarkan oleh kedua sisi (klien dan server). Ini memungkinkan aplikasi untuk merespons perubahan data dalam waktu nyata tanpa perlu me-refresh halaman atau mengirim permintaan HTTP berulang.
