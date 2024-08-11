**Temen-temen**, pernahkah kalian mendengar tentang CLI (Command Line Interface)? Nah, di dunia pemrograman PHP, CLI adalah cara untuk menjalankan skrip PHP langsung dari command line, tanpa memerlukan server web. Ini sangat berguna, misalnya, untuk menjalankan tugas-tugas otomatis, membuat skrip batch, atau melakukan operasi yang tidak memerlukan interaksi pengguna melalui browser.

Mari kita bahas secara detail tentang bagaimana cara menulis dan menjalankan skrip PHP untuk CLI.

#### 1. **Menulis Skrip PHP untuk CLI**

Menulis skrip PHP untuk CLI tidak jauh berbeda dengan menulis skrip PHP biasa. Bedanya, kita perlu memastikan bahwa skrip tersebut dapat berjalan di lingkungan command line. Skrip ini biasanya memiliki fungsi atau logika yang tidak memerlukan antarmuka web.

**Contoh Skrip PHP CLI Sederhana:**

```php
<?php
// hello.php

// Menampilkan pesan
echo "Halo, temen-temen! Ini adalah skrip PHP CLI.\n";

// Mengecek argumen yang diberikan
if ($argc > 1) {
    echo "Argumen yang diterima: " . implode(', ', array_slice($argv, 1)) . "\n";
} else {
    echo "Tidak ada argumen yang diterima.\n";
}
?>
```

**Penjelasan Kode:**

- `<?php ... ?>`: Tag pembuka dan penutup PHP yang menandakan bahwa ini adalah skrip PHP.
- `echo`: Fungsi untuk menampilkan output ke command line.
- `$argc`: Variabel otomatis yang menyimpan jumlah argumen yang diberikan saat menjalankan skrip.
- `$argv`: Array otomatis yang menyimpan argumen-argumen yang diberikan saat menjalankan skrip.
- `implode()`: Fungsi untuk menggabungkan elemen array menjadi string.
- `array_slice()`: Fungsi untuk mengambil bagian dari array, dalam hal ini, argumen yang diberikan setelah nama skrip.

#### 2. **Menjalankan Skrip dari Command Line**

Untuk menjalankan skrip PHP di CLI, temen-temen perlu membuka terminal atau command prompt dan mengetik perintah yang sesuai. Berikut adalah langkah-langkahnya:

1. **Buka Terminal atau Command Prompt**: Temen-temen bisa membuka terminal di Linux atau macOS, atau Command Prompt di Windows.

2. **Arahkan ke Direktori Skrip**: Gunakan perintah `cd` untuk berpindah ke direktori tempat skrip PHP berada. Misalnya:

   ```sh
   cd /path/to/your/script
   ```

3. **Jalankan Skrip PHP**: Gunakan perintah `php` diikuti dengan nama file skrip. Misalnya:

   ```sh
   php hello.php
   ```

   Outputnya akan terlihat seperti ini:

   ```
   Halo, temen-temen! Ini adalah skrip PHP CLI.
   Tidak ada argumen yang diterima.
   ```

   Jika temen-temen menambahkan argumen saat menjalankan skrip, seperti:

   ```sh
   php hello.php arg1 arg2
   ```

   Outputnya akan menjadi:

   ```
   Halo, temen-temen! Ini adalah skrip PHP CLI.
   Argumen yang diterima: arg1, arg2
   ```

**Referensi URL yang Kredibel:**

- [PHP Manual - Command Line Interface](https://www.php.net/manual/en/features.commandline.php)
- [PHP CLI Basics](https://www.php.net/manual/en/features.commandline.background.php)
- [PHP CLI Tutorial](https://www.tutorialspoint.com/php/php_command_line_interface.htm)

Dengan menggunakan CLI, temen-temen bisa memanfaatkan PHP untuk banyak hal di luar pengembangan web. Misalnya, skrip-skrip otomatis yang bisa dijalankan secara terjadwal dengan `cron` di Linux atau Task Scheduler di Windows. Jadi, jangan ragu untuk eksplorasi dan coba implementasikan skrip PHP CLI dalam proyek temen-temen! 🚀

Semoga penjelasan ini bermanfaat dan membantu temen-temen dalam memahami penggunaan PHP CLI. Jika ada pertanyaan lebih lanjut atau butuh bantuan, feel free untuk bertanya! 😄
