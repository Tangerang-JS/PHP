
Halo temen-temen! Di artikel kali ini, kita akan bahas cara mengolah file CSV dan Excel menggunakan PHP. Yuk, kita mulai dengan memahami bagaimana kita bisa membaca dan menulis file CSV, serta menggunakan library PHPExcel untuk bekerja dengan file Excel. Untuk memudahkan penjelasan, saya akan pakai analogi yang sederhana. Bayangkan kamu sedang mengelola data tabel di spreadsheet dan ingin memindahkannya ke aplikasi PHP kita.

#### 1. Membaca dan Menulis File CSV

**File CSV (Comma-Separated Values)** adalah format file yang sering digunakan untuk menyimpan data tabular seperti tabel di spreadsheet. File CSV menyimpan data dalam format teks dengan setiap baris mewakili satu record, dan setiap kolom dipisahkan oleh koma.

##### **Membaca File CSV**

Misalnya, kita punya file CSV bernama `data.csv` yang berisi daftar kontak seperti ini:

```
nama,email,telepon
Bahrul Rozak,bahrul@example.com,123456789
Ali,ali@example.com,987654321
```

Untuk membaca file CSV menggunakan PHP, kita bisa menggunakan fungsi `fgetcsv()`. Berikut adalah contoh kode sederhana:

```php
<?php
// Nama file CSV
$filename = 'data.csv';

// Membuka file CSV untuk dibaca
if (($handle = fopen($filename, "r")) !== FALSE) {
    // Membaca baris pertama sebagai header
    $header = fgetcsv($handle);

    // Membaca setiap baris dalam file CSV
    while (($data = fgetcsv($handle)) !== FALSE) {
        // Menampilkan data
        echo "Nama: " . $data[0] . "<br>";
        echo "Email: " . $data[1] . "<br>";
        echo "Telepon: " . $data[2] . "<br><br>";
    }
    // Menutup file
    fclose($handle);
} else {
    echo "Tidak bisa membuka file.";
}
?>
```

**Penjelasan Kode:**

1. `fopen($filename, "r")` membuka file CSV dalam mode baca.
2. `fgetcsv($handle)` membaca baris pertama sebagai header (judul kolom).
3. Dalam loop `while`, `fgetcsv($handle)` membaca setiap baris data.
4. Data dari setiap baris ditampilkan ke browser.
5. `fclose($handle)` menutup file setelah selesai dibaca.

##### **Menulis File CSV**

Sekarang, kita akan membuat dan menulis data ke file CSV. Berikut contohnya:

```php
<?php
// Nama file CSV
$filename = 'data_baru.csv';

// Data yang akan ditulis
$data = [
    ['nama', 'email', 'telepon'],
    ['Bahrul Rozak', 'bahrul@example.com', '123456789'],
    ['Ali', 'ali@example.com', '987654321']
];

// Membuka file CSV untuk ditulis
if (($handle = fopen($filename, "w")) !== FALSE) {
    // Menulis setiap baris data
    foreach ($data as $row) {
        fputcsv($handle, $row);
    }
    // Menutup file
    fclose($handle);
    echo "File CSV berhasil ditulis.";
} else {
    echo "Tidak bisa membuka file untuk ditulis.";
}
?>
```

**Penjelasan Kode:**

1. `fopen($filename, "w")` membuka file CSV dalam mode tulis (akan membuat file baru atau menimpa file yang ada).
2. `fputcsv($handle, $row)` menulis setiap baris data ke file.
3. `fclose($handle)` menutup file setelah selesai ditulis.

#### 2. Menggunakan Library PHPExcel untuk File Excel

PHPExcel adalah library PHP yang digunakan untuk membaca dan menulis file Excel (XLSX). Meskipun PHPExcel sudah deprecated dan digantikan oleh PhpSpreadsheet, kita akan menggunakan PHPExcel untuk contoh ini. 

##### **Instalasi PHPExcel**

Untuk menginstal PHPExcel, gunakan Composer:

```bash
composer require phpoffice/phpexcel
```

##### **Membaca File Excel**

Berikut adalah contoh kode untuk membaca file Excel:

```php
<?php
require 'vendor/autoload.php';

use PHPExcel_IOFactory;

// Nama file Excel
$filename = 'data.xlsx';

// Membaca file Excel
$objPHPExcel = PHPExcel_IOFactory::load($filename);
$sheet = $objPHPExcel->getActiveSheet();
$data = $sheet->toArray();

// Menampilkan data
foreach ($data as $row) {
    echo "Nama: " . $row[0] . "<br>";
    echo "Email: " . $row[1] . "<br>";
    echo "Telepon: " . $row[2] . "<br><br>";
}
?>
```

**Penjelasan Kode:**

1. `PHPExcel_IOFactory::load($filename)` memuat file Excel.
2. `$objPHPExcel->getActiveSheet()` mengambil sheet aktif dari file Excel.
3. `$sheet->toArray()` mengonversi sheet ke array PHP.
4. Data ditampilkan ke browser.

##### **Menulis File Excel**

Berikut contoh kode untuk menulis data ke file Excel:

```php
<?php
require 'vendor/autoload.php';

use PHPExcel;
use PHPExcel_Writer_Excel2007;

// Membuat objek PHPExcel
$objPHPExcel = new PHPExcel();

// Menambahkan data ke sheet
$objPHPExcel->setActiveSheetIndex(0)
    ->setCellValue('A1', 'Nama')
    ->setCellValue('B1', 'Email')
    ->setCellValue('C1', 'Telepon')
    ->setCellValue('A2', 'Bahrul Rozak')
    ->setCellValue('B2', 'bahrul@example.com')
    ->setCellValue('C2', '123456789')
    ->setCellValue('A3', 'Ali')
    ->setCellValue('B3', 'ali@example.com')
    ->setCellValue('C3', '987654321');

// Menyimpan file Excel
$objWriter = new PHPExcel_Writer_Excel2007($objPHPExcel);
$objWriter->save('data_baru.xlsx');

echo "File Excel berhasil ditulis.";
?>
```

**Penjelasan Kode:**

1. `new PHPExcel()` membuat objek PHPExcel.
2. `setCellValue()` menetapkan nilai ke sel tertentu di sheet.
3. `PHPExcel_Writer_Excel2007` digunakan untuk menyimpan file Excel dalam format XLSX.

#### Referensi URL

- [PHP Manual: File Handling](https://www.php.net/manual/en/book.filesystem.php)
- [PHPExcel Documentation](https://phpexcel.codeplex.com/)
- [PhpSpreadsheet Documentation](https://phpspreadsheet.readthedocs.io/)

Semoga penjelasan ini membantu temen-temen dalam memahami cara mengolah file CSV dan Excel menggunakan PHP. Jika ada yang kurang jelas atau ada pertanyaan lain, jangan ragu untuk bertanya!
