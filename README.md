# Laporan Proyek Machine Learning - Febri Isthifa Adha

## Project Overview

### Latar Belakang

Indonesia merupakan negara kepulauan terbesar di dunia dengan kekayaan destinasi wisata yang luar biasa, mulai dari keindahan alam, warisan budaya, hingga kuliner yang beragam. Sektor pariwisata menjadi salah satu penggerak utama ekonomi Indonesia, dengan kontribusi signifikan terhadap PDB nasional dan penciptaan lapangan kerja. Berdasarkan jumlah kunjungan wisatawan mancanegara ke Indonesia melalui seluruh pintu masuk bulan Januari 2024 sebesar 927.746 terdiri dari 760.036 kunjungan atau 81,93% melalui pencatatan imigrasi dan 167.710 kunjungan atau 18,07% melalui pencatatan Mobile Positioning Data pada pintu masuk perbatasan [1].

Dalam daftar yang dirilis World Economic Forum (WEF) pada 21 Mei 2024, posisi Indonesia kembali naik 10 peringkat, dari rangking 32 menjadi 22 dunia. Berdasarkan data TTDI 2024, Indonesia mendapat skor 4,46 dengan posisi sembilan peringkat di bawah Singapura yang meraih skor 4,76 dan berada di ranking 13 [2]. 

Beragamnya destinasi wisata dan preferensi yang ada tak jarang membuat turis kebingungan dalam menentukan pilihan destinasi wisata yang akan mereka kunjungi. Akibatnya, banyak wisatawan, baik domestik maupun internasional, sering mengalami kesulitan dalam menemukan destinasi wisata yang sesuai dengan preferensi mereka sehingga menyebabkan ketidakpuasan mereka dalam berlibur. Untuk itu, sistem rekomendasi destinasi wisata ini dibuat dengan harapan turis dapat terbantu dalam memilih destinasi wisata dengan tepat.

Dengan adanya sistem rekomendasi destinasi wisata, diharapkan wisatawan dapat merencanakan perjalanan mereka dengan lebih baik, menemukan destinasi wisata yang sesuai dengan keinginan mereka, dan mengoptimalkan pengalaman wisata mereka di Indonesia.

## Business Understanding

### Problem Statements

Berdasarkan latar belakang yang telah diuraikan, berikut adalah rumusan masalah yang akan diselesaikan dalam proyek ini:
- Bagaimana rekomendasi destinasi wisata dapat membantu meningkatkan kunjungan wisatawan di Indonesia?
- Bagaimana cara untuk membuat model yang dapat memberikan hasil rekomendasi sesuai dengan ketertarikan pengguna?

### Goals

Tujuan dari proyek ini adalah:
- Mengetahui bagaimana rekomendasi destinasi wisata dapat membantu meningkatkan kunjungan wisatawan di Indonesia.
- Mendapatkan model yang dapat memberikan rekomendasi yang sesuai dengan ketertarikan pengguna.

### Solution statements

Untuk mencapai goals yang telah ditetapkan, berikut adalah solusi yang akan diterapkan:
1. Pengelolaan data
   - Mengumpulkan data destinasi wisata pada daerah yang sering dikunjungi oleh masyarakat.
   - Mempersiapkan data dengan preprocessing dan preparation agar dapat dimodelkan dengan sistem rekomendasi yang sesuai.
2. Pemodelan
   - Melakukan pembuatan model sistem rekomendasi berbasis _Content-Based Filtering_ untuk merekomendasikan destinasi wisata berdasarkan kategori yang sesuai.
   - Melakukan pembuatan model sistem rekomendasi berbasis _Collaborative Filtering_ untuk merekomendasikan destinasi wisata berdasarkan perilaku pengguna dalam memberikan ulasan pada destinasi wisata.

## Data Understanding

Dataset yang digunakan dalam proyek ini adalah dataset [Indonesia Tourism Destination](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination) yang diambil dari platfrom Kaggle. File yang digunakan berupa file csv, yaitu `tourism_ with _id.csv` dengan 437 baris dan 9 kolom, `tourism_rating.csv` dengan 10000 baris dengan 3 kolom, dan `user.csv` dengan 300 baris dan 3 kolom.

### Exploratory Data Analysis - EDA

Kemudian dilakukan proses Exploratory Data Analysis (EDA) yang merupakan proses investigasi awal pada data untuk menganalisis karakteristik, menemukan pola, anomali, dan memeriksa asumsi pada data.

### Variabel-variabel pada Destinasi Wisata Indonesia

- **tourism_ with _id** : berisi informasi tempat wisata di 5 kota besar di Indonesia yang berjumlah ~400
- **tourism_rating** : berisi 3 kolom yaitu user, tempat, dan rating yang diberikan, berfungsi untuk membuat sistem rekomendasi berdasarkan rating yang diberikan
- **user** : yang berisi data pengguna dummy untuk membuat fitur rekomendasi berdasarkan pengguna

### Deskripsi Variabel

1. Deskripsi Variabel `tourism_ with _id`

   Tabel 1. Deskripsi Variabel `tourism_ with _id`
   |   | Column       | Non-Null Count | Dtype   |  
   |---|--------------|----------------|---------|  
   | 0 | Place_Id     | 437 non-null   | int64   |  
   | 1 | Place_Name   | 437 non-null   | object  |
   | 2 | Description  | 437 non-null   | object  |
   | 3 | Category     | 437 non-null   | object  |
   | 4 | City         | 437 non-null   | object  |
   | 5 | Price        | 437 non-null   | int64   |
   | 6 | Rating       | 437 non-null   | float64 |
   | 7 | Time_Minutes | 205 non-null   | float64 |
   | 8 | Coordinate   | 437 non-null   | object  |
   | 9 | Lat          | 437 non-null   | float64 |
   | 10 | Long        | 437 non-null   | float64 |
   | 11 | Unnamed: 11 | 0 non-null     | float64 |
   | 12 | Unnamed: 12 | 437 non-null   | int64   |

   Dari hasil di atas terlihat bahwa:
   
   - Terdapat tiga tipe data utama dalam dataset:
     - Integer (int64) : `Place_Id`, `Price`, dan `Unnamed: 12`.
     - Float (float64) : `Rating`, `Time_Minutes`, `Lat`, `Long`, dan `Unnamed: 11`.
     - String (object) : `Place_Name`, `Description`, `Category`, `City`, dan `Coordinate`.

   - Nilai null:
     - Kolom `Time_Minutes` memiliki 205 nilai non-null dari total 437 entri, yang berarti terdapat 232 nilai yang hilang.
     - Kolom `Unnamed: 11` tidak memiliki nilai yang terisi (0 non-null), sehingga kolom ini sepenuhnya kosong.
     - Kolom lainnya memiliki 437 nilai non-null, artinya tidak ada nilai yang hilang kecuali pada `Time_Minutes` dan `Unnamed: 11`.

   - Variabel dataset:
     - `Place_Id` : Identitas destinasi wisata.
     - `Place_Name` : Nama destinasi wisata.
     - `Description` : Deskripsi singkat tentang destinasi.
     - `Category` : Kategori destinasi (misalnya: Budaya, Alam).
     - `City` : Kota tempat destinasi berada.
     - `Price` : Harga tiket masuk.
     - `Rating` : Rating rata-rata dari pengguna (0-5).
     - `Time_Minutes` : Waktu yang dibutuhkan untuk mengunjungi (dalam menit).
     - `Coordinate` : Koordinat geografis.
     - `Lat` : Latitude lokasi.
     - `Long` : Longitude lokasi.
     - `Unnamed: 11` : Kolom kosong.
     - `Unnamed: 12` : Nilai duplikat dari Place_id

1. Deskripsi Variabel `user`

   Tabel 2. Deskripsi Variabel `user`
   |   | Column   | Non-Null Count | Dtype  |
   |---|----------|----------------|--------| 
   | 0 | User_Id  | 300 non-null   | int64  |
   | 1 | Location | 300 non-null   | object |
   | 2 | Age      | 300 non-null   | int64  |

   Dari hasil di atas terlihat bahwa:

   - Terdapat dua tipe data utama dalam dataset:
     - Integer (int64) : `User_Id` dan `Age`.
     - String (object) : `Location`
     
   - Tidak ada nilai yang hilang dalam dataset ini, semua kolom memiliki 300 nilai non-null.
     
   - Variabel dataset:
     - `User_Id` : Identitas pengguna.
     - `Location` : Asal pengguna
     - `Age` : Usia pengguna
    
3. Deskripsi Variabel `tourism_rating`

   Tabel 3. Deskripsi Variabel `tourism_rating`
   |   | Column        | Non-Null Count | Dtype |
   |---|---------------|----------------|-------|
   | 0 | User_Id       | 10000 non-null | int64 |
   | 1 | Place_Id      | 10000 non-null | int64 |
   | 2 | Place_Ratings | 10000 non-null | int64 |

   Dari hasil di atas terlihat bahwa:

   - Semua kolom memiliki tipe data Integer (`int64`)
     
   - Tidak ada nilai yang hilang dalam dataset ini, semua kolom memiliki 10.000 nilai non-null.
     
   - Variabel dataset:
     - `User_Id` : Identitas pengguna.
     - `Place_Id` : Identitas destinasi wisata.
     - `Place_Ratings` : Rating yang diberikan oleh pengguna kepada destinasi wisata

## Data Preparation
   

## Referensi

[1] Kementerian Pariwisata dan Ekonomi Kreatif. (2024). "Statistik Kunjungan Wisatawan Mancanegara Bulan Januari 2024." (https://kemenparekraf.go.id/direktori-statistik/statistik-kunjungan-wisatawan-mancanegara-bulan-januari-2024)

[2] Liputan6. (2024). "Indeks Pariwisata Indonesia Ranking ke-22 Dunia pada 2024, Kembali Lampaui Malaysia dan Thailand." (https://www.liputan6.com/lifestyle/read/5602060/indeks-pariwisata-indonesia-ranking-ke-22-dunia-pada-2024-kembali-lampaui-malaysia-dan-thailand?page=4)

[3]
