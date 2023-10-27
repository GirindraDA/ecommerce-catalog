# Product Viewer App

Ini adalah aplikasi sederhana yang memungkinkan Anda untuk menampilkan produk secara acak dari [FakeStoreAPI](https://fakestoreapi.com/). Aplikasi ini memanfaatkan teknologi Vue.js untuk mengambil data produk dan menampilkannya dalam antarmuka yang interaktif.

## Fitur

- Menampilkan produk secara acak dari FakeStoreAPI.
- Menampilkan detail produk, termasuk gambar, judul, kategori, rating, deskripsi, dan harga.
- Mengganti tema antarmuka berdasarkan kategori produk.
- Kemampuan untuk beralih ke produk berikutnya.

## Penggunaan

1. Clone repositori ini ke komputer Anda.
2. Buka terminal dan arahkan ke direktori repositori.
3. Jalankan perintah `npm install` untuk menginstal dependensi.
4. Jalankan perintah `npm run serve` untuk menjalankan aplikasi pada mode pengembangan.
5. Buka browser dan akses [http://localhost:8080] untuk melihat aplikasi.

## Komponen

Aplikasi ini terdiri dari beberapa komponen Vue.js, termasuk:

- `ProductViewer`: Komponen utama yang menampilkan detail produk dan mengganti tema.
- `ProductNotAvailable`: Komponen yang ditampilkan jika produk tidak tersedia.
- `LoadingPlaceholder`: Komponen yang digunakan saat data produk sedang dimuat.
