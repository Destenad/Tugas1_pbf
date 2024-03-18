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

## Dokumentasi
Panduan Pengguna adalah dokumentasi utama untuk CodeIgniter 4.

Panduan Pengguna yang sedang dalam proses dapat ditemukan di sini . Seperti halnya kerangka kerja lainnya, kerangka ini masih dalam proses, dan akan mengalami perubahan seiring berjalannya waktu pada struktur, penjelasan, dan lain-lain.

## Pemula Aplikasi
Repositori starter aplikasi CodeIgniter 4 menyimpan aplikasi kerangka, dengan ketergantungan komposer pada versi kerangka terbaru yang dirilis.

Teknik instalasi ini cocok untuk pengembang yang ingin memulai proyek baru berbasis CodeIgniter4.

## Instalasi
Di folder di atas root proyek Anda:

```bash
composer create-project codeigniter4/appstarter ci4
```
Perintah di atas akan membuat folder ci4.

Jika Anda menghilangkan argumen “ci4”, perintah akan membuat folder “appstarter”, yang dapat diganti namanya sesuai kebutuhan.

## Konfigurasi Awal
Buka file app/Config/App.php dengan editor teks.

** $baseURL
Tetapkan URL dasar Anda menjadi $baseURL. Jika Anda memerlukan lebih banyak fleksibilitas, baseURL dapat diatur dalam file .env sebagai . Selalu gunakan garis miring pada URL dasar Anda!
``` shell
app.baseURL = 'http://localhost:8080/';
```
alamat tersebut dapat di dapatkan dengan server pengembangan lokal, memanfaatkan server web bawaan PHP dengan routing CodeIgniter. Anda dapat meluncurkannya, dengan baris perintah berikut pada terminal yang telah arahkan ke direktori utama file ci4 (projek yang sebelumnya di atas):
``` bash
php spark serve
```
Ini akan meluncurkan server dan sekarang Anda dapat melihat aplikasi Anda di browser Anda di http://localhost:8080 .

## Important Change with index.php

**Please** read the user guide for a better explanation of how CI4 works!

## Repository Management


## Contributing


## Server Requirements


## Running CodeIgniter Tests


