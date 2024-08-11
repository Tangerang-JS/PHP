Halo temen-temen! 🌟 Pada kesempatan kali ini, kita akan membahas topik yang sering banget dibutuhkan dalam pengembangan web, yaitu **paginasi data**. Bayangkan temen-temen punya buku besar dengan ribuan halaman, dan kita hanya mau membaca beberapa halaman saja dalam sekali waktu. Nah, paginasi itu seperti membagi buku besar itu menjadi beberapa bagian yang lebih kecil dan lebih mudah dibaca.

**Paginasi data** ini penting ketika kita bekerja dengan data yang banyak, seperti daftar produk, posting blog, atau data pengguna. Tanpa paginasi, kita harus memuat semua data sekaligus yang bisa membuat aplikasi kita lambat dan sulit diatur.

#### 1. **Apa Itu Paginasi?**

Paginasi adalah proses membagi data menjadi beberapa halaman. Misalnya, jika kita punya 100 item dan kita ingin menampilkan 10 item per halaman, kita akan membagi data menjadi 10 halaman. Halaman pertama menampilkan item 1 sampai 10, halaman kedua menampilkan item 11 sampai 20, dan seterusnya.

#### 2. **Kenapa Paginasi Itu Penting?**

Paginasi membantu:
- **Meningkatkan Kinerja:** Mengurangi beban pada server dan klien karena hanya memuat sebagian data dalam sekali waktu.
- **Mempermudah Navigasi:** Memudahkan pengguna untuk menemukan data yang mereka cari tanpa harus menggulir terlalu banyak.

#### 3. **Membuat Paginasi Sederhana di PHP**

Sekarang, mari kita lihat bagaimana cara membuat paginasi data dengan PHP. Kita akan menggunakan contoh sederhana di mana kita menampilkan daftar produk dari database. Misalnya, kita punya tabel produk dengan kolom `id`, `name`, dan `price`.

##### Langkah 1: **Membuat Koneksi ke Database**

Pertama, kita butuh koneksi ke database MySQL kita. Berikut adalah kode PHP untuk membuat koneksi:

```php
<?php
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "shop";

// Buat koneksi
$conn = new mysqli($servername, $username, $password, $dbname);

// Periksa koneksi
if ($conn->connect_error) {
    die("Koneksi gagal: " . $conn->connect_error);
}
?>
```

##### Langkah 2: **Menentukan Halaman Saat Ini dan Jumlah Data per Halaman**

Kita perlu menentukan halaman saat ini dan jumlah item yang ditampilkan per halaman:

```php
<?php
$items_per_page = 10; // Jumlah item per halaman
$page = isset($_GET['page']) ? (int)$_GET['page'] : 1; // Halaman saat ini
$offset = ($page - 1) * $items_per_page; // Menghitung offset untuk query
?>
```

##### Langkah 3: **Mengambil Data dari Database**

Selanjutnya, kita ambil data produk dari database dengan batasan yang sudah ditentukan:

```php
<?php
$sql = "SELECT * FROM products LIMIT $offset, $items_per_page";
$result = $conn->query($sql);

if ($result->num_rows > 0) {
    while($row = $result->fetch_assoc()) {
        echo "ID: " . $row["id"]. " - Name: " . $row["name"]. " - Price: " . $row["price"]. "<br>";
    }
} else {
    echo "0 results";
}
?>
```

##### Langkah 4: **Menampilkan Navigasi Paginasi**

Kita perlu menampilkan link untuk berpindah antar halaman:

```php
<?php
// Hitung jumlah total data
$sql_total = "SELECT COUNT(*) AS total FROM products";
$result_total = $conn->query($sql_total);
$row_total = $result_total->fetch_assoc();
$total_items = $row_total['total'];
$total_pages = ceil($total_items / $items_per_page);

// Tampilkan link halaman
for ($i = 1; $i <= $total_pages; $i++) {
    echo "<a href='?page=$i'>$i</a> ";
}
?>
```

##### Langkah 5: **Menutup Koneksi Database**

Jangan lupa untuk menutup koneksi setelah selesai:

```php
<?php
$conn->close();
?>
```

#### **Penjelasan Kode**

- **Koneksi ke Database:** Menggunakan `mysqli` untuk terhubung ke database.
- **Menentukan Halaman dan Offset:** `$_GET['page']` untuk mengambil nomor halaman dari URL. `LIMIT $offset, $items_per_page` membatasi data yang diambil dari database.
- **Menampilkan Data:** Menampilkan data produk berdasarkan batasan yang ditentukan.
- **Navigasi Paginasi:** Menghitung total halaman berdasarkan total data dan item per halaman, serta menampilkan link untuk berpindah antar halaman.

Dengan cara ini, temen-temen bisa membagi data menjadi beberapa halaman dan memungkinkan pengguna untuk melihat data dengan lebih mudah. Ini sangat membantu ketika bekerja dengan dataset yang besar.

#### **Referensi**

- [PHP Manual - MySQLi](https://www.php.net/manual/en/book.mysqli.php)
- [PHP Manual - Pagination](https://www.php.net/manual/en/book.pdo.php) 

Semoga penjelasan ini membantu temen-temen untuk memahami dan menerapkan paginasi data dalam aplikasi PHP. Jangan ragu untuk bertanya jika ada yang kurang jelas! 😊
