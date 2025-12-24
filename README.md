# 📘 Panduan Penggunaan Sistem Resident Help

Dokumen ini menjelaskan alur kerja aplikasi **Resident Help** mulai dari persiapan data oleh Admin hingga proses pelaporan kerusakan oleh Warga.

---

## 🔐 Akun Demo (Default)

Gunakan akun berikut untuk simulasi:

| Role | Email | Password | Keterangan |
| :--- | :--- | :--- | :--- |
| **Admin** | `admin@admin.com` | `password` | Akses Full (Manajemen Data & Laporan) |
| **Nasabah** | `nasabah@gmail.com` | `password` | Pemilik Rumah (Bisa Lapor & Cek Aset) |
| **Warga** | `warga@gmail.com` | `password` | Penghuni (Bisa Lapor Kerusakan) |

---

## SKENARIO 1: ALUR KERJA ADMIN (Manajemen)

Admin adalah kunci utama sistem. Sebelum warga bisa lapor, Admin harus menyiapkan datanya dulu.

### 1. Login & Dashboard
1. Buka halaman login, masuk sebagai **Admin**.
2. Anda akan melihat **Dashboard Statistik** (Grafik Penjualan Unit & Tren Keluhan).

### 2. Setup Data Master (Wajib Dilakukan di Awal)
Sebelum menjual rumah, data ini harus ada:
* **Menu Data User:** Cek daftar user yang sudah register. Jika ada Nasabah baru daftar mandiri, datanya akan muncul di sini.
* **Menu Data Mitra Teknisi:**
    1. Klik "Tambah Tukang".
    2. Input Nama, Spesialisasi (Listrik/Air/Bangunan), dan No WA.
    3. Status awal default adalah `Available` (Ready).
* **Menu Data Unit Rumah:**
    1. Klik "Tambah Unit".
    2. Input Blok, Nomor, dan Harga (Input harga otomatis ada titik pemisah ribuan).
    3. Isi spesifikasi lengkap (Listrik, Air, Luas).
    4. Status awal `Tersedia`.

### 3. Proses Penjualan / Serah Terima (Ownership)
Ini langkah paling krusial agar User Nasabah bisa melihat rumahnya.
1.  **Lengkapi Biodata Nasabah:**
    * Masuk menu **Data Nasabah**.
    * Klik "Lengkapi Data".
    * Pilih Akun User (yang daftar mandiri tadi), lalu isi NIK, Alamat KTP, dan Domisili.
2.  **Transaksi Penjualan (Linking):**
    * Masuk menu **Data Penjualan**.
    * Klik "Input Penjualan".
    * Pilih **Unit Rumah** (yang statusnya Tersedia).
    * Pilih **Nasabah** (yang sudah lengkap biodatanya).
    * Tentukan metode bayar (Cash/Kredit) dan Tanggal Serah Terima.
    * **PENTING:** Set status ke `Active` (agar bisa dipakai lapor) atau `Moved Out` (jika rumah kosong).
    * *Otomatis:* Status Unit berubah jadi `Terjual` dan Masa Garansi aktif selama 3 tahun.

### 4. Manajemen Komplain (Disposisi)
Saat ada laporan masuk dari warga:
1.  Admin mendapat notifikasi di Dashboard (Kartu "Keluhan Baru").
2.  Masuk menu **Transaksi > Maintenance**.
3.  Lihat laporan dengan status `Pending`. Klik tombol **Proses**.
4.  Cek detail keluhan dan foto bukti.
5.  Ubah status menjadi `In Progress`.
6.  **Pilih Teknisi** yang statusnya `Available`.
7.  Simpan. (Status teknisi otomatis berubah jadi `Busy`).

### 5. Penyelesaian Tiket
Setelah teknisi selesai bekerja:
1.  Buka kembali laporan tersebut.
2.  Ubah status menjadi `Done` (Selesai).
3.  Simpan. (Status teknisi kembali `Available` dan siap terima job baru).

### 6. Cetak Laporan (Output Managerial)
Masuk menu **Laporan & Output**, Admin bisa mencetak:
* **Rekapitulasi Keluhan:** PDF daftar semua kerusakan.
* **Analisis Kategori:** PDF grafik jenis kerusakan (Listrik vs Air, dll).
* **Kinerja SLA:** PDF kecepatan respon (Cepat/Lambat).
* **Data Teknisi:** PDF jumlah job yang diselesaikan tiap tukang.
* **Indeks Kepuasan:** PDF rating bintang dari warga.
* **Database Nasabah:** Excel data lengkap pemilik rumah.

---

## SKENARIO 2: ALUR KERJA NASABAH / WARGA

### 1. Registrasi Mandiri
1.  Di halaman depan (Landing Page), klik **Mulai Sekarang** atau **Daftar Akun**.
2.  Isi Nama, Email, **No HP (WA)**, dan pilih Role (Warga/Nasabah).
3.  Klik Daftar. Anda akan langsung login.
    * *Note:* Saat awal daftar, menu "Rumah Saya" masih kosong sampai Admin menghubungkan akun Anda dengan Unit Rumah (Langkah A.3 di atas).

### 2. Cek Aset (Rumah Saya)
1.  Klik menu **Rumah Saya**.
2.  Jika sudah di-link oleh Admin, akan muncul Kartu Rumah.
3.  Anda bisa melihat Spesifikasi Bangunan dan **Status Garansi** (Aktif/Expired).

### 3. Melaporkan Kerusakan
1.  Klik tombol **Lapor Kerusakan** di Dashboard atau di Kartu Rumah.
2.  Pilih Unit Rumah yang bermasalah.
3.  Isi Judul (misal: "Kran Air Patah") dan Deskripsi.
4.  Upload Foto Bukti.
5.  Klik Kirim.

### 4. Tracking & Cetak Tiket
1.  Masuk menu **Riwayat Keluhan**.
2.  Status awal adalah `Pending`.
3.  Klik **Detail** untuk melihat info teknisi (jika sudah diproses).
4.  Klik **Icon Print** 🖨️ untuk mencetak **Tiket Bukti Lapor** sebagai pegangan saat teknisi datang.

### 5. Memberi Rating (Feedback)
1.  Setelah Admin mengubah status menjadi `Done` (Selesai).
2.  Buka detail keluhan tersebut.
3.  Akan muncul Form Penilaian.
4.  Beri Bintang (1-5) dan ulasan (Testimoni).
5.  Submit.

---

## 💡 Troubleshooting (Tips)

1.  **Gambar tidak muncul?**
    * Pastikan sudah menjalankan perintah: `php artisan storage:link`.
2.  **PDF Error / Tanda Tanya pada Bintang?**
    * Pastikan koneksi internet stabil (untuk load font).
    * Sistem menggunakan font `DejaVu Sans` untuk support simbol rating.
3.  **Rumah tidak muncul saat mau Lapor?**
    * Hubungi Admin. Pastikan status kepemilikan Anda di set ke `Active`. Jika statusnya `Moved Out` atau `Sold`, unit tidak bisa dilaporkan.

---
