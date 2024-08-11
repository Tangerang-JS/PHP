Halo temen-temen! Kali ini gue bakal ngebahas tentang dasar-dasar query database di PHP, khususnya empat perintah dasar yang paling sering dipakai: **SELECT**, **INSERT**, **UPDATE**, dan **DELETE**. Sebelum kita masuk ke detailnya, gue bakal kasih sedikit analogi biar temen-temen lebih mudah paham.

Bayangin temen-temen punya toko buku. Database itu kayak rak buku raksasa yang isinya semua informasi tentang buku-buku yang ada di toko temen-temen. Nah, query database ini adalah cara kita buat ngatur, cari, tambah, ubah, dan hapus buku-buku di rak itu. Mari kita bedah satu per satu!

### 1. SELECT: Memilih Buku dari Rak

**SELECT** itu kayak temen-temen lagi nyari buku di rak. Dengan perintah ini, kita bisa ngambil informasi yang kita butuhin dari database. Misalnya, kita pengen tahu semua buku yang judulnya "Belajar PHP".

Contoh Kode:

```php
<?php
// Koneksi ke database
$koneksi = new mysqli("localhost", "root", "", "toko_buku");

// Cek koneksi
if ($koneksi->connect_error) {
    die("Koneksi gagal: " . $koneksi->connect_error);
}

// Query untuk memilih buku dengan judul "Belajar PHP"
$sql = "SELECT * FROM buku WHERE judul = 'Belajar PHP'";
$hasil = $koneksi->query($sql);

// Menampilkan hasil
if ($hasil->num_rows > 0) {
    while($row = $hasil->fetch_assoc()) {
        echo "ID: " . $row["id"]. " - Judul: " . $row["judul"]. " - Pengarang: " . $row["pengarang"]. "<br>";
    }
} else {
    echo "Tidak ada buku yang ditemukan";
}

$koneksi->close();
?>
```

**Penjelasan:**

- **Koneksi ke Database:** Pertama-tama, kita harus nyambungin PHP ke database MySQL kita pake `mysqli`.
- **Query SELECT:** `SELECT * FROM buku WHERE judul = 'Belajar PHP'` ini nyari semua buku di tabel `buku` yang judulnya "Belajar PHP".
- **Menampilkan Hasil:** Kalau ada buku yang ketemu, kita tampilin deh detailnya. Kalau nggak, kita kasih tahu kalau buku itu nggak ada.

### 2. INSERT: Menambah Buku Baru ke Rak

Bayangin temen-temen baru beli buku baru dan pengen naruh buku itu di rak. **INSERT** ini adalah perintah buat nambahin data baru ke database.

Contoh Kode:

```php
<?php
// Koneksi ke database
$koneksi = new mysqli("localhost", "root", "", "toko_buku");

// Cek koneksi
if ($koneksi->connect_error) {
    die("Koneksi gagal: " . $koneksi->connect_error);
}

// Query untuk menambah buku baru
$sql = "INSERT INTO buku (judul, pengarang, penerbit) VALUES ('Belajar PHP', 'Bahrul Rozak', 'Teknologi Hebat')";

if ($koneksi->query($sql) === TRUE) {
    echo "Buku baru berhasil ditambahkan!";
} else {
    echo "Error: " . $sql . "<br>" . $koneksi->error;
}

$koneksi->close();
?>
```

**Penjelasan:**

- **Query INSERT:** `INSERT INTO buku (judul, pengarang, penerbit) VALUES ('Belajar PHP', 'Bahrul Rozak', 'Teknologi Hebat')` ini buat nambahin buku baru ke tabel `buku` dengan judul "Belajar PHP", pengarang "Bahrul Rozak", dan penerbit "Teknologi Hebat".
- **Eksekusi Query:** Kalau berhasil, kita dapet pesan sukses, kalau gagal, kita bisa lihat error-nya.

### 3. UPDATE: Mengedit Buku yang Ada di Rak

Katakanlah temen-temen mau ganti penerbit buku karena ada kesalahan cetak. **UPDATE** ini kayak temen-temen lagi ngedit informasi buku yang udah ada di rak.

Contoh Kode:

```php
<?php
// Koneksi ke database
$koneksi = new mysqli("localhost", "root", "", "toko_buku");

// Cek koneksi
if ($koneksi->connect_error) {
    die("Koneksi gagal: " . $koneksi->connect_error);
}

// Query untuk mengupdate penerbit buku
$sql = "UPDATE buku SET penerbit = 'Penerbit Baru' WHERE judul = 'Belajar PHP'";

if ($koneksi->query($sql) === TRUE) {
    echo "Data buku berhasil diupdate!";
} else {
    echo "Error: " . $sql . "<br>" . $koneksi->error;
}

$koneksi->close();
?>
```

**Penjelasan:**

- **Query UPDATE:** `UPDATE buku SET penerbit = 'Penerbit Baru' WHERE judul = 'Belajar PHP'` ini buat ngedit penerbit buku yang judulnya "Belajar PHP" jadi "Penerbit Baru".
- **Eksekusi Query:** Kalau berhasil, kita dapet pesan kalau data buku udah diupdate.

### 4. DELETE: Membuang Buku dari Rak

Kalau temen-temen mau ngebuang buku yang udah nggak relevan atau rusak, kita bisa pake perintah **DELETE** buat ngapus data dari database.

Contoh Kode:

```php
<?php
// Koneksi ke database
$koneksi = new mysqli("localhost", "root", "", "toko_buku");

// Cek koneksi
if ($koneksi->connect_error) {
    die("Koneksi gagal: " . $koneksi->connect_error);
}

// Query untuk menghapus buku
$sql = "DELETE FROM buku WHERE judul = 'Belajar PHP'";

if ($koneksi->query($sql) === TRUE) {
    echo "Buku berhasil dihapus!";
} else {
    echo "Error: " . $sql . "<br>" . $koneksi->error;
}

$koneksi->close();
?>
```

**Penjelasan:**

- **Query DELETE:** `DELETE FROM buku WHERE judul = 'Belajar PHP'` ini buat ngapus buku dengan judul "Belajar PHP" dari database.
- **Eksekusi Query:** Kalau berhasil, kita dapet pesan kalau buku udah dihapus dari database.

### Kesimpulan

Dengan menguasai empat perintah dasar ini, temen-temen udah punya pondasi yang kuat untuk ngelola data di database. Ibaratnya, temen-temen udah bisa nyari buku, nambahin buku baru, ngedit buku yang udah ada, dan ngapus buku yang nggak diperlukan lagi dari rak toko buku temen-temen.

Jika temen-temen pengen mendalami lebih lanjut, bisa cek sumber-sumber berikut untuk referensi:

- [W3Schools - PHP MySQL Select Data](https://www.w3schools.com/php/php_mysql_select.asp)
- [PHP.net - MySQLi Documentation](https://www.php.net/manual/en/book.mysqli.php)

Semoga artikel ini bermanfaat dan temen-temen makin jago ngoding PHP!
