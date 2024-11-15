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

## Referensi

[1] Kementerian Pariwisata dan Ekonomi Kreatif. (2024). "Statistik Kunjungan Wisatawan Mancanegara Bulan Januari 2024." (https://kemenparekraf.go.id/direktori-statistik/statistik-kunjungan-wisatawan-mancanegara-bulan-januari-2024)

[2] Liputan6. (2024). "Indeks Pariwisata Indonesia Ranking ke-22 Dunia pada 2024, Kembali Lampaui Malaysia dan Thailand." (https://www.liputan6.com/lifestyle/read/5602060/indeks-pariwisata-indonesia-ranking-ke-22-dunia-pada-2024-kembali-lampaui-malaysia-dan-thailand?page=4)

[3]
