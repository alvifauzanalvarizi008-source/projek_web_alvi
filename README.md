# Inventaris Sarana dan Prasarana

Aplikasi PHP untuk katalog inventaris dan peminjaman barang sekolah.

## Menjalankan di hosting

GitHub menyimpan source code, tetapi GitHub Pages tidak menjalankan PHP atau MySQL. Deploy aplikasi ini ke hosting yang mendukung PHP dan MySQL/MariaDB (PHP 8.2 atau lebih baru, ekstensi `mysqli` aktif).

1. Buat database MySQL/MariaDB pada hosting, lalu impor `SARANA_PRASARAN.sql` melalui phpMyAdmin. Jika hosting tidak mengizinkan `CREATE DATABASE`, pilih/buat database dari panel hosting dan hapus perintah `CREATE DATABASE` serta `USE` dari salinan SQL sebelum import.
2. Atur environment variables di panel hosting:
   - `SARPRAS_DB_HOST`: host MySQL dari provider.
   - `SARPRAS_DB_NAME`: nama database.
   - `SARPRAS_DB_USER`: user database.
   - `SARPRAS_DB_PASSWORD`: kata sandi database.
3. Upload source code ke document root hosting, atau sambungkan repository GitHub ke fitur deploy provider PHP.
4. Siapkan file `daftar-peminjam.json` secara terpisah. File ini berisi data pribadi siswa dan sengaja tidak disertakan di GitHub. Upload ke lokasi privat di server, lalu atur `SARPRAS_BORROWERS_FILE` ke path absolut file tersebut. Formatnya berupa array JSON, misalnya:

   ```json
   [
     {
       "kelas": "X PPLG 1",
       "nama": "Nama Siswa"
     }
   ]
   ```

5. Uji halaman utama (`index.php`), login, dashboard, dan laporan setelah deploy. Ganti kredensial demo sebelum aplikasi digunakan secara publik.

## Pengembangan lokal XAMPP

Taruh folder proyek di `htdocs`, jalankan Apache dan MySQL, impor `SARANA_PRASARAN.sql`, lalu buka proyek melalui `http://localhost/PROJECT_UJIKOM_ALVI_12PPLG2/`. Koneksi lokal default di `koneksi.php` menggunakan `localhost`, user `root`, tanpa kata sandi. Nilai ini dapat diganti melalui environment variables yang disebutkan di atas.

## Catatan penyimpanan aplikasi

`koneksi.php` menyediakan koneksi database, tetapi fitur dashboard saat ini belum menggunakan koneksi tersebut. Data inventaris dan peminjaman disimpan di `localStorage` browser, sehingga tidak tersinkron antar pengguna/perangkat dan dapat hilang jika data browser dihapus. Database SQL yang disertakan belum otomatis menjadi penyimpanan aplikasi.
