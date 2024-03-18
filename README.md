# CodeIgniter 4 Development

[![PHPUnit](https://github.com/codeigniter4/CodeIgniter4/workflows/PHPUnit/badge.svg)](https://github.com/codeigniter4/CodeIgniter4/actions/workflows/test-phpunit.yml)
[![PHPStan](https://github.com/codeigniter4/CodeIgniter4/actions/workflows/test-phpstan.yml/badge.svg)](https://github.com/codeigniter4/CodeIgniter4/actions/workflows/test-phpstan.yml)
[![Psalm](https://github.com/codeigniter4/CodeIgniter4/actions/workflows/test-psalm.yml/badge.svg)](https://github.com/codeigniter4/CodeIgniter4/actions/workflows/test-psalm.yml)
[![Coverage Status](https://coveralls.io/repos/github/codeigniter4/CodeIgniter4/badge.svg?branch=develop)](https://coveralls.io/github/codeigniter4/CodeIgniter4?branch=develop)
[![Downloads](https://poser.pugx.org/codeigniter4/framework/downloads)](https://packagist.org/packages/codeigniter4/framework)
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/codeigniter4/CodeIgniter4)](https://packagist.org/packages/codeigniter4/framework)
[![GitHub stars](https://img.shields.io/github/stars/codeigniter4/CodeIgniter4)](https://packagist.org/packages/codeigniter4/framework)
[![GitHub license](https://img.shields.io/github/license/codeigniter4/CodeIgniter4)](https://github.com/codeigniter4/CodeIgniter4/blob/develop/LICENSE)
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/codeigniter4/CodeIgniter4/pulls)
<br>

Apa itu CodeIgniter?
CodeIgniter adalah framework web full-stack PHP yang ringan, cepat, fleksibel dan aman. Informasi lebih lanjut dapat ditemukan di situs resmi .

Repositori ini hanya menyimpan kode sumber untuk CodeIgniter 4. Versi 4 adalah penulisan ulang yang lengkap untuk menghadirkan kualitas dan kode ke versi yang lebih modern, sambil tetap menjaga banyak hal tetap utuh yang telah membuat orang menyukai kerangka ini selama bertahun-tahun.

# Dokumentasi
Panduan Pengguna adalah dokumentasi utama untuk CodeIgniter 4.

Panduan Pengguna yang sedang dalam proses dapat ditemukan di sini . Seperti halnya kerangka kerja lainnya, kerangka ini masih dalam proses, dan akan mengalami perubahan seiring berjalannya waktu pada struktur, penjelasan, dan lain-lain.

# Pemula Aplikasi
Repositori starter aplikasi CodeIgniter 4 menyimpan aplikasi kerangka, dengan ketergantungan komposer pada versi kerangka terbaru yang dirilis.

Teknik instalasi ini cocok untuk pengembang yang ingin memulai proyek baru berbasis CodeIgniter4.

### Instalasi
Di folder di atas root proyek Anda:

```bash
composer create-project codeigniter4/appstarter Tugas1_pbf
```
Perintah di atas akan membuat folder Tugas1_pbf.

Jika Anda menghilangkan argumen “Tugas1_pbf”, perintah akan membuat folder “appstarter”, yang dapat diganti namanya sesuai kebutuhan.

### Mengatur Mode Pengembangan
Secara default, CodeIgniter dijalankan dalam mode produksi. Ini adalah fitur keamanan untuk menjaga situs Anda sedikit lebih aman jika pengaturannya kacau saat ditayangkan. Jadi pertama-tama mari kita perbaiki itu. Salin atau ganti nama file env menjadi .env . Bukalah.

File ini berisi pengaturan khusus server. Ini berarti Anda tidak perlu memasukkan informasi sensitif apa pun ke sistem kontrol versi Anda. Ini mencakup beberapa yang paling umum yang sudah ingin Anda masukkan, meskipun semuanya sudah diberi komentar. Jadi batalkan komentar pada baris dengan CI_ENVIRONMENTdi atasnya, dan ubah production menjadi development:
``` bash
CI_ENVIRONMENT = development
```
### Konfigurasi Awal
Buka file app/Config/App.php dengan editor teks.

** $baseURL
Tetapkan URL dasar Anda menjadi $baseURL. Jika Anda memerlukan lebih banyak fleksibilitas, baseURL dapat diatur dalam file .env sebagai . Selalu gunakan garis miring pada URL dasar Anda!

``` shell
app.baseURL = 'http://localhost:8080/';
```

alamat tersebut dapat di dapatkan dengan server pengembangan lokal, memanfaatkan server web bawaan PHP dengan routing CodeIgniter. Anda dapat meluncurkannya, dengan baris perintah berikut pada terminal yang telah arahkan ke direktori utama file ci4 (projek yang sebelumnya di atas):
![Terminal akses](https://github.com/Destenad/Tugas1_pbf/assets/134569575/15480ba2-a35b-4bcd-a60d-84daa4742dab)

``` bash
php spark serve
```

Ini akan meluncurkan server dan sekarang Anda dapat melihat aplikasi Anda di browser Anda di http://localhost:8080 .

# Menetapkan Aturan Perutean
Perutean mengaitkan URI dengan metode pengontrol. Pengontrol hanyalah sebuah kelas yang membantu mendelegasikan pekerjaan. Kami akan membuat pengontrol nanti.

Mari kita siapkan aturan perutean. Buka file rute yang terletak di app/Config/Routes.php .

Satu-satunya petunjuk rute untuk memulai adalah:
``` bash
<?php

use CodeIgniter\Router\RouteCollection;
/**
 * @var RouteCollection $routes
 */
$routes->get('/', 'Home::index');
```

Arahan ini mengatakan bahwa setiap permintaan masuk tanpa konten apa pun yang ditentukan harus ditangani oleh index()metode di dalam Homepengontrol.

Tambahkan baris berikut, setelah arahan rute untuk '/'.

```bash
use App\Controllers\Pages;

$routes->get('pages', [Pages::class, 'index']);
$routes->get('(:segment)', [Pages::class, 'view']);
```

![Routing](https://github.com/Destenad/Tugas1_pbf/assets/134569575/1bb2ac7b-63ad-4ea9-a885-d7325987e861)

CodeIgniter membaca aturan routingnya dari atas ke bawah dan merutekan permintaan ke aturan pertama yang cocok. Setiap aturan adalah ekspresi reguler (sisi kiri) yang dipetakan ke pengontrol dan nama metode (sisi kanan). Ketika sebuah permintaan masuk, CodeIgniter mencari kecocokan pertama, dan memanggil pengontrol dan metode yang sesuai, mungkin dengan argumen.

Informasi selengkapnya tentang perutean dapat ditemukan di Perutean URI .

Di sini, aturan kedua dalam $routesobjek mencocokkan permintaan GET dengan jalur URI /pages , dan dipetakan ke index()metode kelas Pages.

Aturan ketiga dalam $routesobjek mencocokkan permintaan GET ke segmen URI menggunakan placeholder (:segment), dan meneruskan parameter ke view()metode kelas Pages.

### Buat Pengontrol Halaman
Buat file di app/Controllers/Pages.php dengan kode berikut.
```bash
<?php

namespace App\Controllers;

class Pages extends BaseController
{
    public function index()
    {
        echo "Helo world";
    }

    public function view($page = 'home')
    {
        // ...
    }
}
```
maka setelah jadi maka saat kita mengetikan pada alamat http://localhost:8080/pages
akan muncul seperti gambar berikut
![Helloworld](https://github.com/Destenad/Tugas1_pbf/assets/134569575/f4d64c8e-155e-44d0-8efb-2952d5e4f990)
### Buat Tampilan
Sekarang setelah Anda membuat metode pertama, sekarang saatnya membuat beberapa templat halaman dasar. Kami akan membuat dua "tampilan" (templat halaman) yang bertindak sebagai footer dan header halaman kami.

Buat header di app/Views/templates/header.php dan tambahkan kode berikut:
```bash
<!doctype html>
<html>
<head>
    <title>CodeIgniter Tutorial</title>
</head>
<body>

    <h1><?= esc($title) ?></h1>
    ```
Header berisi kode HTML dasar yang ingin Anda tampilkan sebelum memuat tampilan utama, bersama dengan judul. Ini juga akan menampilkan $titlevariabel, yang akan kita definisikan nanti di pengontrol. Sekarang, buat footer di app/Views/templates/footer.php yang menyertakan kode berikut:
```bash
    <em>&copy; 2022</em>
</body>
</html>
```

### Menambahkan Logika ke Controller
Buat home.php dan about.php
Sebelumnya Anda menyiapkan pengontrol dengan suatu view()metode. Metode ini menerima satu parameter, yaitu nama halaman yang akan dimuat.

Badan halaman statis akan ditempatkan di direktori app/Views/pages .

Di direktori itu, buat dua file bernama home.php dan about.php . Di dalam file tersebut, ketikkan beberapa teks - apa pun yang Anda suka - dan simpan. Jika Anda ingin tampil tidak orisinal, cobalah “Hello World!”.

### Halaman Lengkap::view() Metode
Untuk memuat halaman tersebut, Anda harus memeriksa apakah halaman yang diminta benar-benar ada. Ini akan menjadi isi metode view()pada Pagespengontrol yang dibuat di atas:
```bash
<?php

namespace App\Controllers;

use CodeIgniter\Exceptions\PageNotFoundException; // Add this line

class Pages extends BaseController
{
    // ...

    public function view($page = 'home')
    {
        if (! is_file(APPPATH . 'Views/pages/' . $page . '.php')) {
            // Whoops, we don't have a page for that!
            throw new PageNotFoundException($page);
        }

        $data['title'] = ucfirst($page); // Capitalize the first letter

        return view('templates/header', $data)
            . view('pages/' . $page)
            . view('templates/footer');
    }
}
```
Dan tambahkan setelah baris untuk mengimpor kelas.use CodeIgniter\Exceptions\PageNotFoundException;namespacePageNotFoundException

Sekarang, ketika halaman yang diminta memang ada, halaman tersebut dimuat, termasuk header dan footer, dan dikembalikan ke pengguna. Jika pengontrol mengembalikan string, string tersebut akan ditampilkan kepada pengguna.

# Membuat Database
Pada tahap ini akan menyiapkan database yang akan di gunakan. Dalam tutorial ini kita akan mengeluarkan perintah database (mysql, MySQL Workbench, atau phpMyAdmin).

Anda perlu membuat database ci4 dapat digunakan untuk tutorial ini, dan kemudian mengkonfigurasi CodeIgniter untuk menggunakannya.

Menggunakan klien database Anda, sambungkan ke database Anda dan jalankan perintah SQL di bawah ini (MySQL):
```bash
use ci4

CREATE TABLE mahasiswa (
    id INT UNSIGNED NOT NULL AUTO_INCREMENT,
    nama VARCHAR(128) NOT NULL,
    jurusan VARCHAR(128) NOT NULL,
    alamat TEXT NOT NULL,
    PRIMARY KEY (id)
);
```
Untuk mengecek apakah tabel tersebut berhasil di buat
```bash
show tables;
```
![cmdtable](https://github.com/Destenad/Tugas1_pbf/assets/134569575/1b9ede8c-971c-42fd-9937-dc12a5954bd5)

Juga, tambahkan beberapa data. 

Data bisa diisi seperti:
```bash
INSERT INTO news VALUES
(1,'Desten','TI','Purwokerto'),
(2,'Aditya','TD','Cilacap'),
(3,'Da','TIK','Purbalingga');
```
Untuk memastikan bahwa data ada pada table tersebut gunakan syntax:
```bash
select*from mahasiswa;
```
![Datatable](https://github.com/Destenad/Tugas1_pbf/assets/134569575/a8363beb-ae3c-48b6-b62c-885e3d761e91)

### Hubungkan ke Basis Data Anda
File konfigurasi lokal, .env , yang Anda buat saat menginstal CodeIgniter, harus memiliki pengaturan properti database yang tidak diberi komentar dan disetel dengan tepat untuk database yang ingin Anda gunakan. Pastikan Anda telah mengkonfigurasi database Anda dengan benar seperti yang dijelaskan dalam Konfigurasi Database :
```bash
database.default.hostname = localhost
 database.default.database = ci4
 database.default.username = root
 database.default.password = 
 database.default.DBDriver = MySQLi
```
![Databaseconfig](https://github.com/Destenad/Tugas1_pbf/assets/134569575/00bb241e-1a50-4f2a-bbf0-f9685d533be6)

### Menyiapkan Model Anda
Daripada menulis operasi database langsung di pengontrol, kueri harus ditempatkan dalam model, sehingga dapat digunakan kembali dengan mudah nanti. Model adalah tempat Anda mengambil, menyisipkan, dan memperbarui informasi dalam database atau penyimpanan data lainnya. Mereka menyediakan akses ke data Anda. Anda dapat membaca lebih lanjut tentang hal ini di Menggunakan Model CodeIgniter .

### Buat Model Berita
Buka direktori app/Models dan buat file baru bernama MahasiswaModel.php dan tambahkan kode berikut.
```bash
<?php

namespace App\Models;

use CodeIgniter\Model;

class NewsModel extends Model
{
    protected $table = 'mahasiswa';
}
```
Kode ini terlihat mirip dengan kode pengontrol yang digunakan sebelumnya. Ini menciptakan model baru dengan memperluas CodeIgniter\Modeldan memuat perpustakaan database. Ini akan membuat kelas database tersedia melalui $this->dbobjek.

### Tambahkan Metode NewsModel::getNews()
Sekarang database dan model telah disiapkan, Anda memerlukan metode untuk mendapatkan semua postingan dari database kami. Untuk melakukan hal ini, lapisan abstraksi database yang disertakan dengan CodeIgniter - Query Builder - digunakan dalam CodeIgniter\Model. Hal ini memungkinkan untuk menulis 'kueri' Anda satu kali dan membuatnya berfungsi pada semua sistem basis data yang didukung . Kelas Model juga memungkinkan Anda bekerja dengan mudah dengan Pembuat Kueri dan menyediakan beberapa alat tambahan untuk mempermudah pengerjaan data. Tambahkan kode berikut ke model Anda.
```bash
  public function getMahasiswa($id = false)
    {
        if ($id === false) {
            return $this->findAll();
        }

        return $this->where(['id' => $id])->first();
    }
```
Dengan kode ini, Anda dapat melakukan dua kueri berbeda. Anda bisa mendapatkan semua catatan berita, atau mendapatkan item berita melalui siputnya. Anda mungkin memperhatikan bahwa $slugvariabel tidak di-escape sebelum menjalankan kueri; Pembuat Kueri melakukan ini untuk Anda.

Dua metode yang digunakan di sini, findAll()dan first(), disediakan oleh CodeIgniter\Modelkelas. Mereka sudah mengetahui tabel yang akan digunakan berdasarkan $table properti yang kita atur di NewsModelkelas tadi. Mereka adalah metode pembantu yang menggunakan Pembuat Kueri untuk menjalankan perintahnya pada tabel saat ini, dan mengembalikan serangkaian hasil dalam format pilihan Anda. Dalam contoh ini, findAll()mengembalikan array dari array.

### Tampilkan Berita
Sekarang setelah kueri ditulis, model harus dikaitkan dengan tampilan yang akan menampilkan item berita kepada pengguna. Ini bisa dilakukan di Pagespengontrol yang kami buat sebelumnya, tetapi demi kejelasan, Mahasiswa Controller baru telah ditentukan.
### Menambahkan Aturan Perutean
Ubah file app/Config/Routes.php Anda , sehingga terlihat seperti berikut:
```bash
<?php

// ...

use App\Controllers\Mahasiswa; // Add this line
use App\Controllers\Pages;

$routes->get('mahasiswa', [News::class, 'index']);           // Add this line
$routes->get('mahasiswa/(:segment)', [News::class, 'show']); // Add this line

$routes->get('pages', [Pages::class, 'index']);
$routes->get('(:segment)', [Pages::class, 'view']);
```
Hal ini memastikan permintaan mencapai Newspengontrol alih-alih langsung ke Pagespengontrol. Baris kedua $routes->get()merutekan URl dengan id ke show()metode di MahasiswaController.
### Buat Mahasiswa Controller
Buat pengontrol baru di app/Controllers/Mahasiswa.php .
```bash
<?php

namespace App\Controllers;

use App\Models\MahasiswaModel;

class News extends BaseController
{
    public function index()
    {
        $model = model(NewsModel::class);

        $data['mahasiswa'] = $model->getMahasiswa();
    }

    public function show($id = null)
    {
        $model = model(NewsModel::class);

        $data['mahasiswa'] = $model->getMahasiswa($id);
    }
}
```
Melihat kodenya, Anda mungkin melihat beberapa kesamaan dengan file yang kita buat sebelumnya. Pertama, ini BaseControllermemperluas kelas inti CodeIgniter, Controlleryang menyediakan beberapa metode pembantu, dan memastikan bahwa Anda memiliki akses ke objek saat ini Requestdan Response, serta Loggerkelas tersebut, untuk menyimpan informasi ke disk.

Berikutnya, ada dua metode, satu untuk melihat semua item berita, dan satu lagi untuk item berita tertentu.

Selanjutnya, model()fungsi tersebut digunakan untuk membuat NewsModelinstance. Ini adalah fungsi pembantu. Anda dapat membaca lebih lanjut tentangnya di Fungsi dan Konstanta Global . Anda juga bisa menulis , jika Anda tidak menggunakannya.$model = new MahasiswaModel();

Anda dapat melihat bahwa $id diteruskan ke metode model di metode kedua. Model menggunakan id ini untuk mengidentifikasi data yang akan dikembalikan.
### Berita Lengkap::index() Metode
Sekarang data diambil oleh pengontrol melalui model kami, tetapi belum ada yang ditampilkan. Hal berikutnya yang harus dilakukan adalah meneruskan data ini ke tampilan. Ubah index()metodenya menjadi seperti ini:
```bash
<?php

namespace App\Controllers;

use App\Models\NewsModel;

class News extends BaseController
{
    public function index()
    {
        $model = model(NewsModel::class);

        $data = [
            'news'  => $model->getNews(),
            'title' => 'News archive',
        ];

        return view('templates/header', $data)
            . view('news/index')
            . view('templates/footer');
    }

    // ...
}
```
![mahasiswacontroller](https://github.com/Destenad/Tugas1_pbf/assets/134569575/baf2508c-cbbd-4d2b-9a9d-ec427b176b4f)

Kode di atas mengambil semua catatan berita dari model dan menugaskannya ke variabel. Nilai judul juga ditetapkan ke $data['title'] elemen dan semua data diteruskan ke tampilan. Anda sekarang perlu membuat tampilan untuk merender item berita.

### Buat File Tampilan Mahasiswa/indeks
Buat app/Views/mahasiswa/index.php dan tambahkan potongan kode berikutnya.
```bash
<h2><?= esc($title) ?></h2>

<?php if (! empty($mahasiswa) && is_array($mahasiswa)): ?>

    <?php foreach ($mahasiswa as $mahasiswa_item): ?>

        <h3><?= esc($mahasiswa_item['id']) ?></h3>

        <div class="main">
            <?= esc($mahasiswa_item['nama']) ?>
        </div>
        <p><a href="/news/<?= esc($mahasiswa_item['alamat'], 'url') ?>">Lihat Data</a></p>

    <?php endforeach ?>

<?php else: ?>

    <p>Unable to find any news for you.</p>

<?php endif ?>
```
### Lihat Lihat File
Satu-satunya hal yang perlu dilakukan adalah membuat tampilan terkait di app/Views/mahasiswa/view.php . Letakkan kode berikut di file ini.
```bash
<h2><?= esc($mahasiswa['nama']) ?></h2>
<p><?= esc($mahasiswa['alamat']) ?></p>
```
Arahkan browser Anda ke halaman “berita”, yaitu localhost:8080/news , Anda akan melihat daftar item berita, yang masing-masing memiliki link untuk menampilkan satu artikel saja.






## Important Change with index.php

**Please** read the user guide for a better explanation of how CI4 works!

## Repository Management


## Contributing


## Server Requirements


## Running CodeIgniter Tests


