Halo temen-temen! Kali ini gue bakal bahas tentang superglobals di PHP. Superglobals adalah variabel global yang bisa diakses dari mana saja di skrip PHP kita. Ada beberapa superglobals yang penting untuk dipahami, seperti `$_GET`, `$_POST`, `$_SESSION`, `$_COOKIE`, dan `$_FILES`. Yuk, kita bahas satu per satu dengan penjelasan yang gampang dipahami!

---

#### 1. `$_GET` dan `$_POST`

**`$_GET`** dan **`$_POST`** adalah cara PHP untuk menerima data dari form HTML. 

**`$_GET`**: Digunakan untuk mengirim data melalui URL. Data yang dikirim menggunakan metode GET ditampilkan di URL sebagai query string.

**`$_POST`**: Digunakan untuk mengirim data melalui HTTP POST. Data tidak ditampilkan di URL, sehingga lebih aman untuk data yang sensitif.

##### Contoh Penggunaan `$_GET`:

Misalnya kita punya form pencarian yang mengirimkan data ke halaman pencarian:

```html
<form action="search.php" method="get">
    <input type="text" name="query" placeholder="Cari...">
    <button type="submit">Cari</button>
</form>
```

Pada halaman `search.php`, kita bisa mengambil data dari form menggunakan `$_GET`:

```php
<?php
if (isset($_GET['query'])) {
    $query = htmlspecialchars($_GET['query']); // Mengamankan data dari XSS
    echo "Hasil pencarian untuk: " . $query;
}
?>
```

**Penjelasan**: `$_GET['query']` mengambil nilai dari input form dengan nama `query`. Fungsi `htmlspecialchars()` digunakan untuk mencegah serangan XSS dengan mengubah karakter khusus menjadi entitas HTML.

##### Contoh Penggunaan `$_POST`:

Sekarang, kita coba form dengan metode POST:

```html
<form action="submit.php" method="post">
    <input type="text" name="name" placeholder="Nama">
    <input type="email" name="email" placeholder="Email">
    <button type="submit">Kirim</button>
</form>
```

Pada halaman `submit.php`, ambil data dengan `$_POST`:

```php
<?php
if (isset($_POST['name']) && isset($_POST['email'])) {
    $name = htmlspecialchars($_POST['name']);
    $email = htmlspecialchars($_POST['email']);
    echo "Nama: " . $name . "<br>";
    echo "Email: " . $email;
}
?>
```

**Penjelasan**: `$_POST['name']` dan `$_POST['email']` mengambil data dari input form. Fungsi `htmlspecialchars()` digunakan untuk menghindari serangan XSS.

---

#### 2. `$_SESSION`

**`$_SESSION`** digunakan untuk menyimpan data selama sesi pengguna di situs web. Data ini disimpan di server dan bisa diakses di berbagai halaman selama sesi berlangsung.

##### Contoh Penggunaan `$_SESSION`:

```php
<?php
// Mulai sesi
session_start();

// Menyimpan data dalam sesi
$_SESSION['username'] = 'JohnDoe';
?>

<p>Selamat datang, <?php echo $_SESSION['username']; ?>!</p>
```

**Penjelasan**: `session_start()` memulai sesi. Setelah itu, kita bisa menyimpan data menggunakan `$_SESSION`. Di halaman lain, kita bisa mengakses data yang sama selama sesi masih aktif.

---

#### 3. `$_COOKIE`

**`$_COOKIE`** digunakan untuk mengakses cookie yang disimpan di browser pengguna. Cookie adalah data kecil yang disimpan di browser untuk mengingat informasi seperti preferensi pengguna.

##### Contoh Penggunaan `$_COOKIE`:

Menyimpan cookie:

```php
<?php
setcookie("user", "JohnDoe", time() + (86400 * 30), "/"); // Cookie berlaku selama 30 hari
?>
```

Mengakses cookie:

```php
<?php
if (isset($_COOKIE['user'])) {
    echo "Selamat datang kembali, " . $_COOKIE['user'];
} else {
    echo "Hai pengunjung baru!";
}
?>
```

**Penjelasan**: `setcookie()` menyimpan cookie dengan nama `user`. Cookie ini berlaku selama 30 hari. `$_COOKIE['user']` digunakan untuk mengambil nilai cookie di halaman lain.

---

#### 4. `$_FILES`

**`$_FILES`** digunakan untuk mengakses file yang diunggah melalui formulir HTML.

##### Contoh Penggunaan `$_FILES`:

Formulir unggah file:

```html
<form action="upload.php" method="post" enctype="multipart/form-data">
    <input type="file" name="fileToUpload">
    <button type="submit">Unggah</button>
</form>
```

Menangani file di `upload.php`:

```php
<?php
if (isset($_FILES['fileToUpload'])) {
    $file = $_FILES['fileToUpload'];

    // Menyimpan file di direktori 'uploads'
    if (move_uploaded_file($file['tmp_name'], 'uploads/' . $file['name'])) {
        echo "File berhasil diunggah!";
    } else {
        echo "Gagal mengunggah file.";
    }
}
?>
```

**Penjelasan**: `$_FILES['fileToUpload']` berisi informasi tentang file yang diunggah, seperti nama sementara, tipe file, dan ukuran file. `move_uploaded_file()` digunakan untuk memindahkan file dari lokasi sementara ke direktori yang ditentukan.

---

Semoga penjelasan ini membantu kalian memahami superglobals di PHP dengan lebih baik! Untuk referensi lebih lanjut, kalian bisa cek [PHP Manual](https://www.php.net/manual/en/reserved.variables.php) yang sangat berguna. Selamat belajar! 🚀
