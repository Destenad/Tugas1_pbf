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

Sekarang kunjungi localhost:8080/home . Apakah itu dirutekan dengan benar ke view() metode di Pagespengontrol? Luar biasa!

Anda akan melihat sesuatu seperti berikut:
![/home](https://github.com/Destenad/Tugas1_pbf/assets/134569575/b529cade-e3a4-4560-89e5-6b598c67e7c0)


# Membuat Database
Pada tahap ini akan menyiapkan database yang akan di gunakan. Dalam tutorial ini kita akan mengeluarkan perintah database (mysql, MySQL Workbench, atau phpMyAdmin).

Anda perlu membuat database ci4 dapat digunakan untuk tutorial ini, dan kemudian mengkonfigurasi CodeIgniter untuk menggunakannya.

Menggunakan klien database Anda, sambungkan ke database Anda dan jalankan perintah SQL di bawah ini (MySQL):
```bash
use ci4

CREATE TABLE news (
    id INT UNSIGNED NOT NULL AUTO_INCREMENT,
    title VARCHAR(128) NOT NULL,
    slug VARCHAR(128) NOT NULL,
    body TEXT NOT NULL,
    PRIMARY KEY (id),
    UNIQUE slug (slug)
);
```
Untuk mengecek apakah tabel tersebut berhasil di buat
```bash
show tables;
```
![tabeldb](https://github.com/Destenad/Tugas1_pbf/assets/134569575/ca916f7a-25ee-45cd-9cd9-993ce9700306)

Juga, tambahkan beberapa data. 

Data bisa diisi seperti:
```bash
INSERT INTO news VALUES
(1,'Elvis sighted','elvis-sighted','Elvis was sighted at the Podunk internet cafe. It looked like he was writing a CodeIgniter app.'),
(2,'Say it isn\'t so!','say-it-isnt-so','Scientists conclude that some programmers have a sense of humor.'),
(3,'Caffeination, Yes!','caffeination-yes','World\'s largest coffee shop open onsite nested coffee shop for staff only.');
```
Untuk memastikan bahwa data ada pada table tersebut gunakan syntax:
```bash
select*from news;
```
![datatable](https://github.com/Destenad/Tugas1_pbf/assets/134569575/08cf72fd-1fc3-4fd5-81b5-91210a1f13ea)


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
Buka direktori app/Models dan buat file baru bernama NewsModel.php dan tambahkan kode berikut.
```bash
<?php

namespace App\Models;

use CodeIgniter\Model;

class NewsModel extends Model
{
    protected $table = 'news';
}
```
Kode ini terlihat mirip dengan kode pengontrol yang digunakan sebelumnya. Ini menciptakan model baru dengan memperluas CodeIgniter\Modeldan memuat perpustakaan database. Ini akan membuat kelas database tersedia melalui $this->dbobjek.

### Tambahkan Metode NewsModel::getNews()
Sekarang database dan model telah disiapkan, Anda memerlukan metode untuk mendapatkan semua postingan dari database kami. Untuk melakukan hal ini, lapisan abstraksi database yang disertakan dengan CodeIgniter - Query Builder - digunakan dalam CodeIgniter\Model. Hal ini memungkinkan untuk menulis 'kueri' Anda satu kali dan membuatnya berfungsi pada semua sistem basis data yang didukung . Kelas Model juga memungkinkan Anda bekerja dengan mudah dengan Pembuat Kueri dan menyediakan beberapa alat tambahan untuk mempermudah pengerjaan data. Tambahkan kode berikut ke model Anda.
```bash
 public function getNews($slug = false)
    {
        if ($slug === false) {
            return $this->findAll();
        }

        return $this->where(['slug' => $slug])->first();
    }
```
Dengan kode ini, Anda dapat melakukan dua kueri berbeda. Anda bisa mendapatkan semua catatan berita, atau mendapatkan item berita melalui siputnya. Anda mungkin memperhatikan bahwa $slugvariabel tidak di-escape sebelum menjalankan kueri; Pembuat Kueri melakukan ini untuk Anda.

Dua metode yang digunakan di sini, findAll()dan first(), disediakan oleh CodeIgniter\Modelkelas. Mereka sudah mengetahui tabel yang akan digunakan berdasarkan $table properti yang kita atur di NewsModelkelas tadi. Mereka adalah metode pembantu yang menggunakan Pembuat Kueri untuk menjalankan perintahnya pada tabel saat ini, dan mengembalikan serangkaian hasil dalam format pilihan Anda. Dalam contoh ini, findAll()mengembalikan array dari array.

### Tampilkan Berita
Sekarang setelah kueri ditulis, model harus dikaitkan dengan tampilan yang akan menampilkan item berita kepada pengguna. Ini bisa dilakukan di Pagespengontrol yang kami buat sebelumnya, tetapi demi kejelasan, Newspengontrol baru telah ditentukan.

### Menambahkan Aturan Perutean
Ubah file app/Config/Routes.php Anda , sehingga terlihat seperti berikut:
```bash
<?php

// ...

use App\Controllers\News; // Add this line
use App\Controllers\Pages;

$routes->get('news', [News::class, 'index']);           // Add this line##
$routes->get('news/(:segment)', [News::class, 'show']); // Add this line

$routes->get('pages', [Pages::class, 'index']);
$routes->get('(:segment)', [Pages::class, 'view']);
```

Hal ini memastikan permintaan mencapai NewsController alih-alih langsung ke PagesController. Baris kedua $routes->get()merutekan URL dengan slug ke show()metode di NewsController.
### Buat NewsController
Buat pengontrol baru di app/Controllers/News.php .
```bash
<?php

namespace App\Controllers;

use App\Models\NewsModel;

class News extends BaseController
{
    public function index()
    {
        $model = model(NewsModel::class);

        $data['news'] = $model->getNews();
    }

    public function show($slug = null)
    {
        $model = model(NewsModel::class);

        $data['news'] = $model->getNews($slug);
    }
}
```
Melihat kodenya, Anda mungkin melihat beberapa kesamaan dengan file yang kita buat sebelumnya. Pertama, ini BaseControllermemperluas kelas inti CodeIgniter, Controlleryang menyediakan beberapa metode pembantu, dan memastikan bahwa Anda memiliki akses ke objek saat ini Requestdan Response, serta Loggerkelas tersebut, untuk menyimpan informasi ke disk.

Berikutnya, ada dua metode, satu untuk melihat semua item berita, dan satu lagi untuk item berita tertentu.

Selanjutnya, model()fungsi tersebut digunakan untuk membuat NewsModelinstance. Ini adalah fungsi pembantu. Anda dapat membaca lebih lanjut tentangnya di Fungsi dan Konstanta Global . Anda juga bisa menulis , jika Anda tidak menggunakannya.$model = new NewsModel();

Anda dapat melihat bahwa $slugvariabel diteruskan ke metode model di metode kedua. Model menggunakan slug ini untuk mengidentifikasi item berita yang akan dikembalikan.

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
Kode di atas mengambil semua catatan berita dari model dan menugaskannya ke variabel. Nilai judul juga ditetapkan ke $data['title'] elemen dan semua data diteruskan ke tampilan. Anda sekarang perlu membuat tampilan untuk merender item berita.

### Buat File Tampilan berita/indeks
Buat app/Views/news/index.php dan tambahkan potongan kode berikutnya.
```bash
<h2><?= esc($title) ?></h2>

<?php if (! empty($news) && is_array($news)): ?>

    <?php foreach ($news as $news_item): ?>

        <h3><?= esc($news_item['title']) ?></h3>

        <div class="main">
            <?= esc($news_item['body']) ?>
        </div>
        <p><a href="/news/<?= esc($news_item['slug'], 'url') ?>">View article</a></p>

    <?php endforeach ?>

<?php else: ?>

    <h3>No News</h3>

    <p>Unable to find any news for you.</p>

<?php endif ?>
```
Di sini, setiap item berita diulang dan ditampilkan kepada pengguna. Anda dapat melihat kami menulis template kami dalam PHP dicampur dengan HTML.

### Berita Lengkap::show() Metode
Halaman ikhtisar berita kini sudah selesai, namun halaman untuk menampilkan item berita individual masih belum ada. Model yang dibuat sebelumnya dibuat sedemikian rupa sehingga dapat dengan mudah digunakan untuk fungsi ini. Anda hanya perlu menambahkan beberapa kode ke controller dan membuat tampilan baru. Kembali ke NewsController dan perbarui show()metode dengan yang berikut:
```bash
<?php

namespace App\Controllers;

use App\Models\NewsModel;
use CodeIgniter\Exceptions\PageNotFoundException;

class News extends BaseController
{
    // ...

    public function show($slug = null)
    {
        $model = model(NewsModel::class);

        $data['news'] = $model->getNews($slug);

        if (empty($data['news'])) {
            throw new PageNotFoundException('Cannot find the news item: ' . $slug);
        }

        $data['title'] = $data['news']['title'];

        return view('templates/header', $data)
            . view('news/view')
            . view('templates/footer');
    }
}
```
Jangan lupa menambahkan untuk mengimpor kelas.use CodeIgniter\Exceptions\PageNotFoundException;PageNotFoundException

Daripada memanggil getNews()metode tanpa parameter, $slugvariabel dilewatkan, sehingga akan mengembalikan item berita tertentu.
### Buat berita/lihat Lihat File
Satu-satunya hal yang perlu dilakukan adalah membuat tampilan terkait di app/Views/news/view.php . Letakkan kode berikut di file ini.
```bash
<h2><?= esc($news['title']) ?></h2>
<p><?= esc($news['body']) ?></p>
```
Arahkan browser Anda ke halaman “news”, yaitu localhost:8080/news , Anda akan melihat daftar item berita, yang masing-masing memiliki link untuk menampilkan satu artikel saja.
![news](https://github.com/Destenad/Tugas1_pbf/assets/134569575/cc3e2e5b-f185-4cf7-b813-233b63bc5283)

# Struktur Aplikasi
Untuk mendapatkan hasil maksimal dari CodeIgniter, Anda perlu memahami bagaimana struktur aplikasi, secara default, dan apa yang dapat Anda ubah untuk memenuhi kebutuhan aplikasi Anda.


### Direktori Default
Instalasi baru memiliki lima direktori: app/, public/, writable/, tests/dan vendor/atau system/. Masing-masing direktori ini memiliki peran yang sangat spesifik untuk dimainkan.
### Aplikasi
Direktori appadalah tempat semua kode aplikasi Anda berada. Ini hadir dengan struktur direktori default yang berfungsi dengan baik untuk banyak aplikasi. Folder berikut membentuk konten dasar:
```bash
app/
    Config/         Stores the configuration files
    Controllers/    Controllers determine the program flow
    Database/       Stores the database migrations and seeds files
    Filters/        Stores filter classes that can run before and after controller
    Helpers/        Helpers store collections of standalone functions
    Language/       Multiple language support reads the language strings from here
    Libraries/      Useful classes that don't fit in another category
    Models/         Models work with the database to represent the business entities
    ThirdParty/     ThirdParty libraries that can be used in application
    Views/          Views make up the HTML that is displayed to the client
```
Karena appdirektori sudah diberi namespace, Anda bebas memodifikasi struktur direktori ini agar sesuai dengan kebutuhan aplikasi Anda. Misalnya, Anda mungkin memutuskan untuk mulai menggunakan pola Repositori dan Model Entitas untuk bekerja dengan data Anda. Dalam hal ini, Anda dapat mengganti nama Modelsdirektori menjadi Repositories, dan menambahkan direktori baru Entities.
Semua file dalam direktori ini berada di bawah Appnamespace, meskipun Anda bebas mengubahnya di app/Config/Constants.php .

### Sistem
Direktori ini menyimpan file-file yang membentuk kerangka itu sendiri. Meskipun Anda memiliki banyak fleksibilitas dalam cara menggunakan direktori aplikasi, file dalam direktori sistem tidak boleh diubah. Sebaliknya, Anda harus memperluas kelas, atau membuat kelas baru, untuk menyediakan fungsionalitas yang diinginkan.

Semua file dalam direktori ini berada di bawah CodeIgniternamespace. 
### publik
Folder publik menampung bagian aplikasi web Anda yang dapat diakses browser, mencegah akses langsung ke kode sumber Anda. Ini berisi file .htaccess utama , index.php , dan aset aplikasi apa pun yang Anda tambahkan, seperti CSS, javascript, atau gambar.

Folder ini dimaksudkan sebagai “root web” situs Anda, dan server web Anda akan dikonfigurasi untuk mengarah ke folder tersebut.
### Dapat ditulis
Direktori ini menampung semua direktori yang mungkin perlu ditulisi selama masa pakai aplikasi. Ini termasuk direktori untuk menyimpan file cache, log, dan unggahan apa pun yang mungkin dikirim pengguna. Anda harus menambahkan direktori lain tempat aplikasi Anda perlu menulis di sini. Hal ini memungkinkan Anda untuk menjaga direktori utama lainnya tidak dapat ditulisi sebagai langkah keamanan tambahan.
### Tes
Direktori ini disiapkan untuk menyimpan file pengujian Anda. Direktori ini _supportmenampung berbagai kelas tiruan dan utilitas lain yang dapat Anda gunakan saat menulis pengujian Anda. Direktori ini tidak perlu ditransfer ke server produksi Anda.
### Memodifikasi Lokasi Direktori
Jika Anda telah memindahkan salah satu direktori utama, Anda dapat mengubah pengaturan konfigurasi di dalam app/Config/Paths.php .

# Model, Tampilan, dan Pengontrol
### Apa itu MVC?
Setiap kali Anda membuat aplikasi, Anda harus menemukan cara untuk mengatur kode agar mudah menemukan file yang tepat dan memudahkan pemeliharaan. Seperti kebanyakan kerangka web, CodeIgniter menggunakan pola Model, View, Controller (MVC) untuk mengatur file. Hal ini menjaga data, presentasi, dan aliran melalui aplikasi sebagai bagian yang terpisah.

Perlu dicatat bahwa ada banyak pandangan mengenai peran masing-masing elemen, namun dokumen ini menjelaskan pendapat kami mengenai hal tersebut. Jika Anda memikirkannya secara berbeda, Anda bebas mengubah cara Anda menggunakan setiap bagian sesuai kebutuhan.

Model mengelola data aplikasi dan membantu menegakkan aturan bisnis khusus yang mungkin diperlukan aplikasi.

Tampilan adalah file sederhana, dengan sedikit atau tanpa logika, yang menampilkan informasi kepada pengguna.

Pengontrol bertindak sebagai kode perekat, menyusun data bolak-balik antara tampilan (atau pengguna yang melihatnya) dan penyimpanan data.

Pada dasarnya, pengontrol dan model hanyalah kelas yang memiliki tugas tertentu. Tentu saja mereka bukan satu-satunya tipe kelas yang dapat Anda gunakan, tetapi mereka membentuk inti bagaimana kerangka kerja ini dirancang untuk digunakan. Mereka bahkan telah menetapkan direktori di direktori aplikasi untuk penyimpanannya, meskipun Anda bebas menyimpannya di mana pun Anda inginkan, asalkan diberi spasi nama yang benar. Kami akan membahasnya lebih detail di bawah ini.

Mari kita lihat lebih dekat masing-masing dari ketiga komponen utama ini.

### Komponen
Tampilan
Tampilan adalah file paling sederhana dan biasanya berbentuk HTML dengan jumlah PHP yang sangat kecil. PHP harusnya sangat sederhana, biasanya hanya menampilkan isi variabel, atau mengulang beberapa item dan menampilkan informasinya dalam sebuah tabel.

Tampilan mendapatkan data untuk ditampilkan dari pengontrol, yang meneruskannya ke tampilan sebagai variabel yang dapat ditampilkan dengan echopanggilan sederhana. Anda juga dapat menampilkan tampilan lain dalam suatu tampilan, membuatnya cukup mudah untuk menampilkan header atau footer umum di setiap halaman.

Tampilan umumnya disimpan di app/Views , tetapi dapat dengan cepat menjadi berat jika tidak diatur dengan cara tertentu. CodeIgniter tidak menerapkan jenis organisasi apa pun, namun aturan praktis yang baik adalah membuat direktori baru di direktori Views untuk setiap pengontrol. Kemudian, beri nama tampilan berdasarkan nama metode. Hal ini membuat mereka sangat mudah ditemukan nantinya. Misalnya, profil pengguna mungkin ditampilkan dalam pengontrol bernama User, dan metode bernama profile. Anda dapat menyimpan file tampilan untuk metode ini di app/Views/user/profile.php .

Jenis organisasi seperti itu berfungsi dengan baik sebagai kebiasaan dasar yang harus dilakukan. Terkadang Anda mungkin perlu mengaturnya secara berbeda. Itu bukan masalah. Selama CodeIgniter dapat menemukan file tersebut, ia dapat menampilkannya.

### Model
Tugas model adalah memelihara satu tipe data untuk aplikasi. Ini mungkin pengguna, postingan blog, transaksi, dll. Dalam hal ini, tugas model memiliki dua bagian: menerapkan aturan bisnis pada data saat diambil dari, atau dimasukkan ke dalam database; dan menangani penyimpanan dan pengambilan data sebenarnya dari database.

Bagi banyak pengembang, kebingungan muncul ketika menentukan aturan bisnis apa yang diterapkan. Artinya, segala batasan atau persyaratan pada data ditangani oleh model. Ini mungkin termasuk normalisasi data mentah sebelum disimpan untuk memenuhi standar perusahaan, atau memformat kolom dengan cara tertentu sebelum menyerahkannya ke pengontrol. Dengan mempertahankan persyaratan bisnis ini dalam model, Anda tidak akan mengulangi kode di beberapa pengontrol dan secara tidak sengaja melewatkan pembaruan suatu area.

Model biasanya disimpan di app/Models , meskipun model tersebut dapat menggunakan namespace untuk dikelompokkan sesuai kebutuhan Anda.

### Controller
Pengendali memiliki beberapa peran berbeda untuk dimainkan. Yang paling jelas adalah mereka menerima masukan dari pengguna dan kemudian menentukan apa yang harus dilakukan dengannya. Hal ini sering kali melibatkan meneruskan data ke model untuk menyimpannya, atau meminta data dari model yang kemudian diteruskan ke tampilan untuk ditampilkan. Hal ini juga mencakup memuat kelas utilitas lainnya, jika diperlukan, untuk menangani tugas khusus yang berada di luar lingkup model.

Tanggung jawab lain dari pengontrol adalah menangani segala sesuatu yang berkaitan dengan permintaan HTTP - pengalihan, otentikasi, keamanan web, pengkodean, dll. Singkatnya, pengontrol adalah tempat Anda memastikan bahwa orang diizinkan berada di sana, dan mereka mendapatkan data mereka butuhkan dalam format yang dapat mereka gunakan.

Pengontrol biasanya disimpan di app/Controllers , meskipun mereka dapat menggunakan namespace untuk dikelompokkan sesuai kebutuhan Anda.












## Important Change with index.php

**Please** read the user guide for a better explanation of how CI4 works!

## Repository Management


## Contributing


## Server Requirements


## Running CodeIgniter Tests


