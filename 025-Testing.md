Halo temen-temen! 👋

Di dunia pengembangan perangkat lunak, testing adalah langkah krusial untuk memastikan bahwa kode kita berjalan dengan baik dan tanpa bug. Salah satu metode testing yang sering digunakan adalah **unit testing**. Yuk, kita bahas secara detail tentang unit testing dan bagaimana cara menggunakan PHPUnit, salah satu framework unit testing populer di PHP.

#### **Apa Itu Unit Testing?**

Unit testing adalah proses menguji bagian-bagian kecil dari kode (disebut unit) secara terpisah untuk memastikan bahwa bagian tersebut bekerja sesuai dengan yang diharapkan. Bayangkan temen-temen sedang merakit sebuah mesin. Sebelum merakit keseluruhan mesin, temen-temen pasti akan memeriksa setiap komponen mesin secara individu untuk memastikan semuanya berfungsi dengan baik. Nah, unit testing itu mirip, tetapi dalam konteks pemrograman. 🤖

#### **Kenapa Unit Testing Itu Penting?**

1. **Menemukan Bug Lebih Awal**: Dengan unit testing, temen-temen bisa menemukan bug lebih cepat sebelum aplikasi di-deploy ke produksi.
2. **Meningkatkan Kualitas Kode**: Unit testing memaksa kita untuk menulis kode yang lebih baik dan modular.
3. **Dokumentasi Otomatis**: Unit tests bisa berfungsi sebagai dokumentasi untuk bagaimana bagian-bagian kode seharusnya bekerja.

#### **Pengenalan PHPUnit**

**PHPUnit** adalah framework unit testing untuk PHP yang membantu kita melakukan unit testing dengan cara yang terstruktur dan efisien. PHPUnit menyediakan berbagai alat untuk menulis dan menjalankan tes.

#### **Instalasi PHPUnit**

Temen-temen bisa menginstal PHPUnit menggunakan Composer, alat manajemen dependensi untuk PHP. Berikut adalah langkah-langkahnya:

1. **Install Composer**: Pastikan Composer sudah terinstal di sistem temen-temen. Jika belum, temen-temen bisa download dan install dari [getcomposer.org](https://getcomposer.org/).

2. **Install PHPUnit**: Jalankan perintah berikut di terminal untuk menginstal PHPUnit:

   ```bash
   composer require --dev phpunit/phpunit
   ```

   Ini akan menginstal PHPUnit sebagai dependensi pengembangan.

#### **Menulis Tes dengan PHPUnit**

Sekarang, mari kita buat contoh tes sederhana. Misalnya, kita punya fungsi PHP yang mengkalkulasi total harga dari sebuah produk dengan diskon. Kita ingin memastikan fungsi ini bekerja dengan benar. Berikut adalah contoh kode fungsinya:

```php
<?php
// src/Calculator.php

class Calculator {
    public function calculateTotal($price, $discount) {
        return $price - ($price * $discount / 100);
    }
}
?>
```

Fungsi `calculateTotal` menerima dua parameter: harga (`$price`) dan diskon (`$discount`), lalu mengembalikan harga setelah diskon diterapkan.

Sekarang, mari kita buat tes untuk fungsi ini. Buat file tes di direktori `tests`:

```php
<?php
// tests/CalculatorTest.php

use PHPUnit\Framework\TestCase;
require 'src/Calculator.php';

class CalculatorTest extends TestCase {
    public function testCalculateTotal() {
        $calculator = new Calculator();
        $result = $calculator->calculateTotal(100, 10);
        $this->assertEquals(90, $result);
    }
}
?>
```

**Penjelasan Kode:**

- **`use PHPUnit\Framework\TestCase;`**: Ini adalah kelas dasar dari PHPUnit yang harus di-extend oleh kelas tes kita.
- **`require 'src/Calculator.php';`**: Ini menyertakan file yang berisi kode yang akan diuji.
- **`testCalculateTotal()`**: Ini adalah metode tes yang akan menguji fungsi `calculateTotal`.
- **`$this->assertEquals(90, $result);`**: Ini memeriksa apakah hasil dari `calculateTotal` sama dengan 90.

#### **Menjalankan Tes**

Untuk menjalankan tes, buka terminal dan jalankan perintah berikut:

```bash
vendor/bin/phpunit tests/CalculatorTest.php
```

Jika tes berhasil, temen-temen akan melihat pesan bahwa semua tes telah lulus. Jika ada yang gagal, PHPUnit akan memberi tahu di bagian mana dan mengapa tes tersebut gagal.

#### **Referensi dan Sumber**

Untuk informasi lebih lanjut tentang PHPUnit dan unit testing, temen-temen bisa mengunjungi beberapa sumber berikut:

- [Dokumentasi Resmi PHPUnit](https://phpunit.de/)
- [Artikel Tutorial Unit Testing dengan PHPUnit](https://www.sitepoint.com/phpunit-tutorial/)

Semoga penjelasan ini membantu temen-temen memahami unit testing dan cara menggunakan PHPUnit! Dengan unit testing, temen-temen bisa membuat kode yang lebih andal dan berkualitas. Selamat mencoba dan jangan ragu untuk bertanya jika ada yang belum jelas! 🚀
