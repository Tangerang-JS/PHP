Halo temen-temen! 🎉 Kali ini kita bakal bahas bagaimana cara membangun API dengan PHP. Jangan khawatir, meski terdengar agak teknis, gue bakal jelasin dengan bahasa yang mudah dipahami. Yuk, langsung aja!

#### 1. Apa itu API Restful?

API (Application Programming Interface) adalah cara aplikasi berkomunikasi satu sama lain. Bayangkan API itu seperti pelayan restoran yang mengantarkan pesanan antara dapur (server) dan meja makan (klien). RESTful API adalah jenis API yang mengikuti prinsip REST (Representational State Transfer). 

Jadi, temen-temen, RESTful API ini seperti menu restoran yang terstruktur dengan jelas. Setiap item menu memiliki URL (alamat) tertentu, dan dengan menggunakan HTTP methods (GET, POST, PUT, DELETE), kita bisa melakukan operasi pada item-menu tersebut.

#### 2. Menggunakan JSON untuk Data Transfer

JSON (JavaScript Object Notation) adalah format data ringan yang digunakan untuk mentransfer data antara server dan klien. Ini seperti bahasa universal yang bisa dimengerti oleh semua sistem.

Misalnya, kalau kita punya data pengguna, kita bisa mengirimkannya dalam format JSON seperti ini:

```json
{
  "name": "Bahrul Rozak",
  "email": "bahrul@example.com"
}
```

#### 3. Autentikasi API

Autentikasi adalah proses untuk memastikan bahwa pengguna yang mengakses API adalah orang yang berwenang. Ini penting untuk melindungi data dan sumber daya di server.

Ada beberapa metode autentikasi, tapi yang paling umum adalah menggunakan **Token**. Token ini seperti kunci untuk membuka pintu. Hanya mereka yang punya kunci yang bisa masuk.

#### Implementasi Kode Sederhana

Mari kita buat API sederhana menggunakan PHP yang dapat meng-handle data pengguna. Kita akan membuat endpoint untuk:

- Mendapatkan data pengguna (GET)
- Menambahkan pengguna baru (POST)

##### Langkah 1: Menyiapkan Database

Kita akan menggunakan database MySQL untuk menyimpan data pengguna. Buat tabel `users` dengan SQL berikut:

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE
);
```

##### Langkah 2: Membuat API

Buat file PHP `api.php` untuk menangani request API. 

```php
<?php
header("Content-Type: application/json");

// Koneksi ke database
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "test_db";

$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Mendapatkan data pengguna
if ($_SERVER['REQUEST_METHOD'] == 'GET') {
    $sql = "SELECT * FROM users";
    $result = $conn->query($sql);
    
    $users = array();
    
    while($row = $result->fetch_assoc()) {
        $users[] = $row;
    }
    
    echo json_encode($users);
}

// Menambahkan pengguna
if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $data = json_decode(file_get_contents("php://input"), true);
    
    $name = $data['name'];
    $email = $data['email'];
    
    $sql = "INSERT INTO users (name, email) VALUES ('$name', '$email')";
    
    if ($conn->query($sql) === TRUE) {
        echo json_encode(["message" => "New record created successfully"]);
    } else {
        echo json_encode(["message" => "Error: " . $sql . "<br>" . $conn->error]);
    }
}

$conn->close();
?>
```

##### Penjelasan Kode

1. **Header**: Kita set header `Content-Type` ke `application/json` supaya klien tahu bahwa data yang dikirim adalah dalam format JSON.

2. **Koneksi Database**: Kita buat koneksi ke database MySQL menggunakan kredensial yang sesuai.

3. **GET Request**: Jika request method-nya `GET`, kita ambil semua data dari tabel `users` dan encode ke JSON untuk dikirim sebagai response.

4. **POST Request**: Jika request method-nya `POST`, kita ambil data JSON dari request body, kemudian masukkan data tersebut ke database. Jika berhasil, kita kirimkan pesan sukses.

#### Autentikasi Token

Untuk menambahkan autentikasi token, kita bisa mengimplementasikan token dengan cara berikut:

```php
$headers = apache_request_headers();
$token = isset($headers['Authorization']) ? $headers['Authorization'] : '';

if ($token !== 'YOUR_SECRET_TOKEN') {
    echo json_encode(["message" => "Unauthorized"]);
    exit();
}
```

Masukkan kode ini di bagian atas skrip `api.php` untuk memeriksa token autentikasi. Ganti `YOUR_SECRET_TOKEN` dengan token rahasia yang kalian buat.

### Referensi

Untuk belajar lebih lanjut tentang API dengan PHP dan konsep-konsep lainnya, temen-temen bisa cek beberapa referensi ini:
- [PHP Manual](https://www.php.net/manual/en/)
- [REST API Tutorial](https://restfulapi.net/)
- [JSON Documentation](https://www.json.org/json-en.html)

Semoga penjelasan ini membantu temen-temen dalam membangun API dengan PHP! Jangan ragu untuk bertanya kalau ada yang kurang jelas. Happy coding! 🚀
