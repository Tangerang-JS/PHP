Halo temen-temen! Kali ini kita bakal bahas tentang database dan bagaimana cara kita menghubungkan PHP dengan database MySQL. Jadi, mari kita mulai dengan dasar-dasarnya dulu ya.

#### Apa Itu Database?

Bayangkan database seperti sebuah lemari arsip digital di mana kita menyimpan informasi. Sebuah database memungkinkan kita untuk menyimpan, mengelola, dan mengambil data dengan cara yang terstruktur. Misalnya, jika kamu punya website toko online, kamu bisa menyimpan informasi tentang produk, pelanggan, dan pesanan di dalam database.

#### Menghubungkan PHP ke Database MySQL

Untuk bisa berinteraksi dengan database MySQL menggunakan PHP, kita perlu membuat koneksi antara keduanya. Ada beberapa cara untuk melakukannya, tapi yang paling umum adalah menggunakan ekstensi MySQLi atau PDO (PHP Data Objects). Kali ini, kita akan fokus pada MySQLi.

**Langkah-langkah Menghubungkan PHP ke MySQL:**

1. **Install dan Siapkan MySQL:**
   - Pastikan MySQL sudah terpasang di server kamu. Biasanya, MySQL sudah termasuk dalam paket instalasi XAMPP atau MAMP.

2. **Buat Database dan Tabel:**
   - Sebelum kita bisa menghubungkan PHP dengan database, kita perlu membuat database dan tabel di MySQL. Kamu bisa menggunakan phpMyAdmin atau command line untuk ini. Misalnya, kita buat database bernama `toko_online` dan tabel `produk` seperti berikut:

   ```sql
   CREATE DATABASE toko_online;
   USE toko_online;

   CREATE TABLE produk (
       id INT AUTO_INCREMENT PRIMARY KEY,
       nama VARCHAR(100) NOT NULL,
       harga DECIMAL(10, 2) NOT NULL
   );
   ```

3. **Koneksi PHP ke Database:**
   - Berikut adalah contoh skrip PHP untuk menghubungkan ke database MySQL menggunakan MySQLi:

   ```php
   <?php
   // Konfigurasi database
   $host = 'localhost'; // Host server
   $user = 'root';      // Username MySQL
   $password = '';      // Password MySQL
   $dbname = 'toko_online'; // Nama database

   // Membuat koneksi
   $koneksi = new mysqli($host, $user, $password, $dbname);

   // Mengecek koneksi
   if ($koneksi->connect_error) {
       die('Koneksi gagal: ' . $koneksi->connect_error);
   }
   echo 'Koneksi berhasil!';
   ?>
   ```

   **Penjelasan Kode:**
   - `$host`, `$user`, `$password`, dan `$dbname` adalah variabel yang menyimpan informasi koneksi ke database.
   - `new mysqli($host, $user, $password, $dbname);` membuat objek koneksi ke database.
   - `if ($koneksi->connect_error)` memeriksa jika terjadi kesalahan saat koneksi. Jika ada, program akan menampilkan pesan kesalahan.

#### CRUD dengan PHP dan MySQL

CRUD adalah singkatan dari Create, Read, Update, dan Delete—empat operasi dasar yang bisa dilakukan pada data dalam database.

1. **Create (Menyimpan Data):**

   Untuk menyimpan data baru ke dalam tabel, kamu bisa menggunakan query SQL `INSERT`. Berikut contohnya:

   ```php
   <?php
   // Menghubungkan ke database
   $koneksi = new mysqli($host, $user, $password, $dbname);

   // Menyimpan data
   $nama_produk = 'Kursi Kayu';
   $harga_produk = 150000;

   $sql = "INSERT INTO produk (nama, harga) VALUES ('$nama_produk', $harga_produk)";

   if ($koneksi->query($sql) === TRUE) {
       echo 'Data berhasil disimpan!';
   } else {
       echo 'Error: ' . $sql . '<br>' . $koneksi->error;
   }

   $koneksi->close();
   ?>
   ```

   **Penjelasan Kode:**
   - `$sql` menyimpan query SQL untuk menyimpan data produk baru.
   - `$koneksi->query($sql)` menjalankan query. Jika berhasil, menampilkan pesan bahwa data berhasil disimpan.

2. **Read (Mengambil Data):**

   Untuk mengambil data dari database, gunakan query SQL `SELECT`. Berikut contoh untuk menampilkan semua produk:

   ```php
   <?php
   // Menghubungkan ke database
   $koneksi = new mysqli($host, $user, $password, $dbname);

   // Mengambil data
   $sql = "SELECT * FROM produk";
   $result = $koneksi->query($sql);

   if ($result->num_rows > 0) {
       // Menampilkan data
       while($row = $result->fetch_assoc()) {
           echo 'ID: ' . $row['id'] . ' - Nama: ' . $row['nama'] . ' - Harga: ' . $row['harga'] . '<br>';
       }
   } else {
       echo '0 hasil';
   }

   $koneksi->close();
   ?>
   ```

   **Penjelasan Kode:**
   - `$result = $koneksi->query($sql);` menjalankan query SELECT.
   - `while($row = $result->fetch_assoc())` mengambil dan menampilkan setiap baris data.

3. **Update (Memperbarui Data):**

   Untuk memperbarui data yang sudah ada, gunakan query SQL `UPDATE`:

   ```php
   <?php
   // Menghubungkan ke database
   $koneksi = new mysqli($host, $user, $password, $dbname);

   // Memperbarui data
   $id_produk = 1;
   $harga_baru = 180000;

   $sql = "UPDATE produk SET harga=$harga_baru WHERE id=$id_produk";

   if ($koneksi->query($sql) === TRUE) {
       echo 'Data berhasil diperbarui!';
   } else {
       echo 'Error: ' . $sql . '<br>' . $koneksi->error;
   }

   $koneksi->close();
   ?>
   ```

   **Penjelasan Kode:**
   - `$sql` menyimpan query SQL untuk memperbarui harga produk berdasarkan ID.
   - `$koneksi->query($sql)` menjalankan query. Jika berhasil, menampilkan pesan bahwa data berhasil diperbarui.

4. **Delete (Menghapus Data):**

   Untuk menghapus data dari tabel, gunakan query SQL `DELETE`:

   ```php
   <?php
   // Menghubungkan ke database
   $koneksi = new mysqli($host, $user, $password, $dbname);

   // Menghapus data
   $id_produk = 1;

   $sql = "DELETE FROM produk WHERE id=$id_produk";

   if ($koneksi->query($sql) === TRUE) {
       echo 'Data berhasil dihapus!';
   } else {
       echo 'Error: ' . $sql . '<br>' . $koneksi->error;
   }

   $koneksi->close();
   ?>
   ```

   **Penjelasan Kode:**
   - `$sql` menyimpan query SQL untuk menghapus produk berdasarkan ID.
   - `$koneksi->query($sql)` menjalankan query. Jika berhasil, menampilkan pesan bahwa data berhasil dihapus.

Dengan semua informasi ini, temen-temen sekarang punya pemahaman dasar tentang bagaimana cara menghubungkan PHP ke MySQL dan melakukan operasi CRUD. Semoga bermanfaat untuk proyek kalian!

**Referensi:**
- [PHP Manual - MySQLi](https://www.php.net/manual/en/book.mysqli.php)
- [W3Schools - PHP MySQL](https://www.w3schools.com/php/php_mysql_intro.asp)
