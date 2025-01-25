# Aplikasi Pendaftaran Siswa

## Gambaran Umum
Aplikasi Pendaftaran Siswa adalah aplikasi desktop berbasis Java yang dirancang untuk mengelola data siswa dan informasi pendaftaran mereka. Aplikasi ini menyediakan fitur untuk menambahkan, memperbarui, menghapus, dan melihat data siswa serta pendaftaran. Selain itu, aplikasi ini mendukung pencetakan tabel data untuk keperluan pelaporan.

## Fitur

### Manajemen Siswa
- Menambahkan siswa baru dengan detail seperti nama, alamat, tanggal lahir, dan jenis kelamin.
- Memperbarui data siswa.
- Menghapus data siswa.
- Melihat tabel semua siswa.
- Mencetak tabel siswa.

### Manajemen Pendaftaran
- Mendaftarkan siswa ke program atau jurusan tertentu.
- Memperbarui detail pendaftaran, termasuk tanggal daftar, jurusan, dan status.
- Menghapus data pendaftaran.
- Melihat tabel semua pendaftaran.
- Mencetak tabel pendaftaran.

## Petunjuk Instalasi

### Prasyarat
- JDK 8 atau lebih baru.
- NetBeans IDE (atau IDE Java pilihan Anda).
- Server database MySQL.
- Driver JDBC untuk MySQL.

### Konfigurasi Database
1. Buat database MySQL dengan nama `pendaftaran_siswa`.
2. Jalankan perintah SQL berikut untuk membuat tabel yang diperlukan:

   ```sql
   CREATE TABLE siswa (
       id_siswa INT AUTO_INCREMENT PRIMARY KEY,
       nama VARCHAR(100) NOT NULL,
       alamat TEXT NOT NULL,
       ttl DATE NOT NULL,
       jenis_kelamin ENUM('Laki-laki', 'Perempuan') NOT NULL
   );

   CREATE TABLE pendaftaran (
       id_pendaftaran INT AUTO_INCREMENT PRIMARY KEY,
       id_siswa INT NOT NULL,
       tanggal_daftar DATE NOT NULL,
       jurusan VARCHAR(100) NOT NULL,
       status ENUM('Aktif', 'Tidak Aktif') NOT NULL,
       FOREIGN KEY (id_siswa) REFERENCES siswa(id_siswa) ON DELETE CASCADE
   );
   ```

3. Perbarui koneksi database di metode `getConnection()`:
   ```java
   private Connection getConnection() throws SQLException {
       String url = "jdbc:mysql://localhost:3306/pendaftaran_siswa";
       String username = "root"; // Perbarui dengan username MySQL Anda
       String password = ""; // Perbarui dengan password MySQL Anda
       return DriverManager.getConnection(url, username, password);
   }
   ```

### Menjalankan Aplikasi
1. Buka proyek di NetBeans.
2. Build proyek untuk menyelesaikan dependensi.
3. Jalankan file utama aplikasi.

## Cara Penggunaan

### Menambahkan Siswa
1. Masukkan detail siswa (nama, alamat, tanggal lahir, dan jenis kelamin).
2. Klik tombol "Simpan" untuk menambahkan siswa ke database.

### Manajemen Siswa
- Untuk memperbarui data siswa, pilih data dari tabel, ubah field yang diperlukan, dan klik "Perbarui."
- Untuk menghapus data siswa, pilih data dari tabel dan klik "Hapus."

### Manajemen Pendaftaran
- Pilih siswa dari tabel siswa.
- Masukkan detail pendaftaran (tanggal daftar, jurusan, dan status) lalu klik "Daftar."
- Perbarui atau hapus data pendaftaran dari tabel pendaftaran.

### Mencetak Data
- Klik tombol "Cetak" pada bagian siswa atau pendaftaran untuk mencetak tabel yang sesuai.

## Penanganan Kesalahan
- Aplikasi akan menampilkan pesan kesalahan dalam dialog jika operasi database gagal (misalnya, kesalahan koneksi atau input data tidak valid).
- Pastikan server database berjalan dan detail koneksi sudah benar.

## Pengembangan di Masa Depan
- Implementasi fitur pencarian dan filter untuk manajemen data yang lebih baik.
- Menambahkan autentikasi pengguna untuk akses yang lebih aman.
- Menyediakan opsi ekspor data (misalnya ke CSV atau PDF).

## Lisensi
Proyek ini dilisensikan di bawah Lisensi MIT. Anda bebas menggunakan dan memodifikasinya sesuai kebutuhan.

