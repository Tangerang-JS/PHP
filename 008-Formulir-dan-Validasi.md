Temen-temen, dalam pemrograman web dengan PHP, formulir dan validasi adalah dua hal yang sangat penting. Mereka memastikan bahwa data yang dikirimkan dari pengguna benar dan aman untuk diproses. Mari kita bahas ketiga topik penting di sini: Membaca Data Formulir, Validasi Formulir, dan Sanitasi Input. 

#### 1. Membaca Data Formulir

Saat temen-temen membuat formulir di halaman web, biasanya ada input yang dikirim ke server ketika formulir tersebut dikirimkan. PHP memudahkan kita untuk mengambil data dari formulir ini menggunakan variabel superglobal seperti `$_GET` dan `$_POST`.

**Contoh Kode:**

```php
<!DOCTYPE html>
<html>
<head>
    <title>Formulir Kontak</title>
</head>
<body>
    <form method="POST" action="process.php">
        Nama: <input type="text" name="nama"><br>
        Email: <input type="email" name="email"><br>
        Pesan: <textarea name="pesan"></textarea><br>
        <input type="submit" value="Kirim">
    </form>
</body>
</html>
```

Di atas adalah contoh formulir HTML sederhana yang mengirimkan data menggunakan metode POST ke file `process.php`. Di dalam file `process.php`, kita dapat membaca data yang dikirimkan seperti ini:

```php
<?php
// process.php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $nama = $_POST['nama'];
    $email = $_POST['email'];
    $pesan = $_POST['pesan'];
    
    echo "Nama: " . htmlspecialchars($nama) . "<br>";
    echo "Email: " . htmlspecialchars($email) . "<br>";
    echo "Pesan: " . htmlspecialchars($pesan) . "<br>";
}
?>
```

**Penjelasan Kode:**

- **`$_POST['nama']`**: Mengambil data yang dikirimkan dari input dengan nama `nama`.
- **`htmlspecialchars()`**: Menghindari masalah keamanan dengan mengubah karakter-karakter khusus ke entitas HTML untuk mencegah XSS (Cross-Site Scripting).

#### 2. Validasi Formulir

Validasi formulir memastikan bahwa data yang diterima memenuhi kriteria tertentu sebelum diproses lebih lanjut. Misalnya, kita bisa memeriksa apakah email yang dimasukkan benar atau tidak.

**Contoh Kode Validasi:**

```php
<?php
// process.php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $nama = trim($_POST['nama']);
    $email = trim($_POST['email']);
    $pesan = trim($_POST['pesan']);
    
    $errors = [];

    // Validasi Nama
    if (empty($nama)) {
        $errors[] = "Nama tidak boleh kosong.";
    }

    // Validasi Email
    if (empty($email) || !filter_var($email, FILTER_VALIDATE_EMAIL)) {
        $errors[] = "Email tidak valid.";
    }

    // Validasi Pesan
    if (empty($pesan)) {
        $errors[] = "Pesan tidak boleh kosong.";
    }

    if (empty($errors)) {
        echo "Data berhasil diproses.";
        // Proses data lebih lanjut
    } else {
        foreach ($errors as $error) {
            echo "<p>$error</p>";
        }
    }
}
?>
```

**Penjelasan Kode:**

- **`trim()`**: Menghapus spasi di awal dan akhir string.
- **`empty()`**: Mengecek apakah variabel kosong.
- **`filter_var()`**: Memvalidasi email dengan filter `FILTER_VALIDATE_EMAIL`.

#### 3. Sanitasi Input

Sanitasi input adalah proses membersihkan data yang diterima untuk memastikan tidak ada data berbahaya yang dikirim ke aplikasi. Ini membantu mencegah berbagai jenis serangan, seperti SQL Injection dan XSS.

**Contoh Kode Sanitasi:**

```php
<?php
// process.php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $nama = filter_var(trim($_POST['nama']), FILTER_SANITIZE_STRING);
    $email = filter_var(trim($_POST['email']), FILTER_SANITIZE_EMAIL);
    $pesan = filter_var(trim($_POST['pesan']), FILTER_SANITIZE_STRING);

    echo "Nama: " . htmlspecialchars($nama) . "<br>";
    echo "Email: " . htmlspecialchars($email) . "<br>";
    echo "Pesan: " . htmlspecialchars($pesan) . "<br>";
}
?>
```

**Penjelasan Kode:**

- **`filter_var()`** dengan `FILTER_SANITIZE_STRING` dan `FILTER_SANITIZE_EMAIL`: Menghapus karakter berbahaya dari string dan email.
- **`htmlspecialchars()`**: Sama seperti sebelumnya, mengubah karakter khusus menjadi entitas HTML.

### Referensi

Untuk mempelajari lebih lanjut tentang formulir, validasi, dan sanitasi input di PHP, temen-temen bisa merujuk ke beberapa sumber berikut:

- [PHP Manual - Forms](https://www.php.net/manual/en/tutorial.forms.php)
- [PHP Manual - Filters](https://www.php.net/manual/en/filter.filters.sanitize.php)
- [W3Schools - PHP Form Validation](https://www.w3schools.com/php/php_form_validation.asp)

Semoga penjelasan ini membantu temen-temen memahami bagaimana cara menangani formulir dan melakukan validasi serta sanitasi input dengan PHP! Jika ada yang kurang jelas atau ada pertanyaan, jangan ragu untuk bertanya.
