### 1. **Membuat Database dan API PHP**
   - **Database**: Membuat tabel `user` dengan kolom `username` dan `password`. Untuk keamanan, password di-*hash* menggunakan fungsi `MD5`.
   - **API PHP**:
     - **koneksi.php**: Menghubungkan aplikasi dengan database `coba-ionic`.
     - **login.php**: Menerima data *input* (username dan password), memverifikasi dari database, dan memberikan respons JSON dengan status login (berhasil atau gagal) beserta *token* sederhana untuk autentikasi.

### 2. **Membuat Proyek Ionic**
   - **Persiapan Project**:
     - Membuat project dengan `ionic start` menggunakan Angular dan menambahkan modul `NgModules`.
     - Instalasi modul `@capacitor/preferences` untuk menyimpan data di *storage* perangkat.
     - Menggunakan perintah `ionic generate` untuk membuat layanan autentikasi (`services/authentication`) dan halaman login (`login.page`).
     - Membuat *guards* (pengaman) untuk melindungi halaman tertentu (`guards/auth` dan `guards/autoLogin`).

### 3. **Implementasi Autentikasi di Ionic**
   - **app.module.ts**: Menggunakan `provideHttpClient` agar aplikasi dapat melakukan request HTTP ke API PHP.
   - **AuthenticationService**:
     - *Service* ini menangani login dan logout, menyimpan token ke *storage*, dan menampilkan notifikasi kesalahan.
     - Metode `saveData()` dan `clearData()` mengatur penyimpanan token dan data pengguna.
     - Metode `postMethod()` melakukan *POST request* ke API PHP.

### 4. **Guard untuk Proteksi Halaman**
   - **auth.guard.ts**: Mencegah pengguna yang belum login untuk mengakses halaman tertentu (seperti halaman *home*).
   - **auto-login.guard.ts**: Mencegah pengguna yang sudah login untuk mengakses halaman *login* lagi, langsung mengarahkan mereka ke halaman *home*.

### 5. **Konfigurasi Routing dan Akses Guard**
   - **app-routing.module.ts**: Menentukan rute aplikasi serta menambahkan *guard* `authGuard` untuk halaman *home* dan `autoLoginGuard` untuk halaman *login*.

### 6. **Halaman Login**
   - **login.page.html**: Tampilan *form* login dengan *input* username dan password serta tombol login.
   - **login.page.ts**:
     - Fungsi `login()` memeriksa apakah username dan password diisi, mengirim data ke API PHP melalui `AuthenticationService`, dan menyimpan token serta data pengguna jika berhasil login.

### 7. **Halaman Home**
   - **home.page.html**: Halaman sederhana dengan tombol *logout* dan pesan selamat datang.
   - **home.page.ts**: Menampilkan nama pengguna yang tersimpan dan memiliki fungsi `logout()` yang menghapus data pengguna dan kembali ke halaman login.

### **Kesimpulan**
Dengan menggunakan Ionic dan Angular, proyek ini membuat aplikasi login sederhana yang terintegrasi dengan API PHP untuk autentikasi. Data login disimpan di *storage* perangkat dengan *guard* untuk melindungi akses ke halaman tertentu.
