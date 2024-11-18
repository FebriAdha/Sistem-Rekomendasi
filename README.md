# Laporan Proyek Machine Learning - Febri Isthifa Adha

![dataset cover](https://raw.githubusercontent.com/FebriAdha/Sistem-Rekomendasi-Destinasi-Wisata/refs/heads/main/images/dataset-cover.jpg)

## Project Overview

### Latar Belakang

Indonesia, sebagai negara kepulauan terbesar di dunia, memiliki potensi pariwisata yang sangat kaya dan beragam. Dengan lebih dari 17.000 pulau yang luar biasa dan punya 50.000 kilometer garis pantai. Indonesia sendiri memiliki sejumlah destinasi wisata populer yang menawarkan keindahan alam, antara lain Bali, hutan tropis di Sumatera dan Kalimantan, serta kawasan cagar alam orang utan di Kalimantan. Tak ketinggalan, ada juga Taman Nasional Komodo yang menjadi salah satu situs warisan dunia UNESCO. [1]. Sektor pariwisata di Indonesia tidak hanya berfungsi sebagai sumber pendapatan devisa negara, tetapi juga berperan penting dalam meningkatkan kesejahteraan masyarakat lokal dan pelestarian lingkungan [2].

Berdasarkan jumlah kunjungan wisatawan mancanegara ke Indonesia melalui seluruh pintu masuk bulan Januari 2024 sebesar 927.746 terdiri dari 760.036 kunjungan atau 81,93% melalui pencatatan imigrasi dan 167.710 kunjungan atau 18,07% melalui pencatatan Mobile Positioning Data pada pintu masuk perbatasan [3]. Dalam daftar yang dirilis World Economic Forum (WEF) pada 21 Mei 2024, posisi Indonesia kembali naik 10 peringkat, dari rangking 32 menjadi 22 dunia. Berdasarkan data TTDI 2024, Indonesia mendapat skor 4,46 dengan posisi sembilan peringkat di bawah Singapura yang meraih skor 4,76 dan berada di ranking 13 [4]. 

Untuk memaksimalkan potensi ini, dengan menerapan pengembangan sistem rekomendasi destinasi wisata, menjadi langkah strategis yang dapat diambil. Sistem rekomendasi memungkinkan wisatawan untuk mendapatkan rekomendasi destinasi, akomodasi, dan aktivitas yang sesuai dengan preferensi dan kebutuhan mereka.

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
2. Modeling
   - Melakukan pembuatan model sistem rekomendasi berbasis _Content-Based Filtering_ untuk merekomendasikan destinasi wisata berdasarkan kategori yang sesuai.
   - Melakukan pembuatan model sistem rekomendasi berbasis _Collaborative Filtering_ untuk merekomendasikan destinasi wisata berdasarkan perilaku pengguna dalam memberikan ulasan pada destinasi wisata.

## Data Understanding

![dataset](https://raw.githubusercontent.com/FebriAdha/Sistem-Rekomendasi-Destinasi-Wisata/refs/heads/main/images/dataset.png)

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

Pada tahap data preparation, dilakukan serangkaian langkah untuk memastikan bahwa data yang digunakan dalam proses pemodelan bersih, terstruktur, dan siap untuk dianalisis.

Pada tahap ini di akan dilakukan beberapa teknik untuk mempersiapkan data seperti:
- Mengatasi missing value.
- Menyamakan nama tempat wisata.

### 1. Mengatasi missing value.
     
Pertama dilakukan pengecekan missing value menggunakan kode berikut: `all_tourism.isnull().sum()`. Dari kode tersebut diketahui tidak terdapat missing value pada semua fitur. Pengecekan terhadap missing value menunjukkan hasil sebagai berikut:

```python
all_tourism.isnull().sum()
```
Output:
|               | 0 |
|---------------|---|
| User_Id       | 0 |
| Place_Id      | 0 |
| Place_Ratings | 0 |
| Place_Name    |	0 |
| Category      | 0 |
| Price         | 0 |

### 2. Menyamakan nama tempat wisata

Sebelum masuk tahap pemodelan, diperlukan proses menyamakan nama tempat wisata berdasarkan Place_Id-nya. Jika terdapat Place_Id yang sama pada lebih dari satu nama tempat dapat menyebabkan bias pada data. Oleh karena itu harus dipastikan bahwa hanya terdapat satu Place_Id pada satu nama tempat saja. Pada proses ini dilakukan pengecekan ulang data setelah proses cleaning pada tahap sebelumnya. Berdasarkan informasi pada dataset, diketahui bahwa jumlah Place_Id dengan jumlah nama tempat wisata tidak sama, artinya terdapat Place_Id yang sama pada lebih dari satu nama tempat wisata. Oleh karena itu, diatasi dengan mengubah datasetnya menjadi data unik sehingga nantinya siap dimasukkan ke dalam proses pemodelan dengan cara membuang data duplikat pada kolom 'Place_Id'. Setelah melewati proses menyamakan jumlah dari jenis buku berdasarkan Place_Id, dataset hanya tersisa 437 baris data. Tahap berikutnya yaitu dibuatkan dictionary untuk menentukan pasangan key-value pada data place_id, place_name, place_category, dan price yang sudah disiapkan sebelumnya untuk proses pengembangan model sistem rekomendasi berbasis konten (content-based filtering). Hasil pembuatan dictionary disimpan dalam variabel bernama tourism_new dan terlihat seperti pada Tabel 6.

Tabel 6. Tampilan tourism_new setelah mengatasi missing value dan menyamakan nama tempat wisata
|	 | id	 | place_name	                  | category      | price |
|---|-----|-------------------------------|---------------|-------|
| 0 |	179 |	Candi Ratu Boko               | Budaya	       | 75000 |
| 1 |	344 |	Pantai Marina	               | Bahari        | 3000  |
| 2 |	5	 | Atlantis Water Adventure      | Taman_Hiburan | 94000 |
| 3 |	373 |	Museum Kereta Ambarawa        | Budaya	       | 10000 |
| 4 |	101 |	Kampung Wisata Sosro Menduran	| Budaya        |	0     |

## Modeling

Dalam menyusun sistem rekomendasi destinasi wisata, dilakukan 2 pendekatan yaitu content based filtering dan collaborative filtering. Dengan content based filtering, dapat direkomendasikan destinasi wisata yang serupa berdasarkan lokasi yang pernah diulas oleh pengguna di masa lalu. Sementara itu, untuk collaborative filtering akan digunakan algoritma neural network RecommendationNet untuk menghasilkan serangkaian rekomendasi berdasarkan nilai-nilai ulasan yang ditinggalkan oleh pengguna pada berbagai destinasi wisata di masa lalu.

### Model Development dengan Content Based Filtering

Pada tahap ini, dikembangkan model dengan teknik Content Based Filtering. Content Based Filtering adalah salah satu pendekatan dalam sistem rekomendasi yang menggunakan informasi atau "konten" dari item atau pengguna untuk membuat rekomendasi. Ide dasarnya adalah mencocokkan preferensi pengguna dengan karakteristik atau konten dari item yang telah dilihat atau disukai oleh pengguna sebelumnya. Misalkan, jika seorang pengguna menyukai atau pernah mengunjungi ketempat wisata dengan nama "Pantai Indrayanti" dan tempat wisata tersebut memiliki fitur berupa kategori wisata yaitu "Bahari", maka sistem akan mencari tempat wisata lain dengan fitur serupa dan merekomendasikannya dalam bentuk top-N recommendation kepada pengguna tersebut.

Kelebihan teknik Content Based Filtering:
- Memberikan rekomendasi yang personal untuk setiap pengguna berdasarkan preferensi unik pengguna.
- Cocok untuk mengatasi masalah cold-start (ketika sedikit data pengguna tersedia) dan dapat memberikan rekomendasi yang baik sejak awal.
- Tidak tergantung pada data pengguna lain.
- Cocok untuk item dengan fitur atau atribut yang mudah diukur atau diidentifikasi.

Kekurangan teknik Content Based Filtering:
- Tidak efektif dalam menangani kejutan, karena hanya merekomendasikan item yang serupa dengan yang sudah diketahui pengguna.
- Kesulitan dalam menangkap preferensi yang kompleks atau dinamis dari pengguna, terutama jika item yang serupa tidak mencerminkan preferensi yang mendalam.
- Ada risiko "filter bubble" di mana pengguna hanya menerima rekomendasi yang sesuai dengan preferensi pengguna yang sudah diketahui, tanpa diverifikasi.

1. **Menggunakan TF-IDF Vectorizer**

   TF-IDF Vectorizer digunakan untuk menemukan representasi fitur penting dari setiap kategori destinasi wisata. Dalam menggunakan TF-IDF Vectorizer, beberapa tahapnya adalah sebagai berikut.
   - Menginisialisasi TF-IDF Vectorizer dari library sklearn.
   - Melakukan perhitungan IDF pada data destinasi wisata.
   - Melakukan mapping fitur index ke fitur nama desrtinasi kategori.
   - Membentuk matriks TF-IDF.

   Setelah dibawa ke dalam bentuk matriks, akan didapatkan nilai-nilai untuk setiap tempat wisata berdasarkan kategorinya. Salah satu contohnya adalah seperti berikut.

   | place_name             | bahari | budaya | cagar_alam | pusat_perbelanjaan | taman_hiburan | tempat_ibadah |
   |------------------------|--------|--------|------------|--------------------|---------------|---------------|	
   | Kampung Pelangi        | 0.0    | 0.0    | 0.0        | 0.0                | 1.0           | 0.0           |
   | Galaxy Waterpark Jogja | 0.0    | 0.0    | 0.0        | 0.0                | 1.0           | 0.0           |
   | Pintoe Langit Dahromo  | 0.0    | 0.0    | 1.0        | 0.0                | 0.0           | 0.0           |

   Output matriks tf-idf di atas menunjukkan Taman Kasmaran memiliki kategori taman hiburan. Hal ini terlihat dari nilai matriks 1.0 pada kategori taman hiburan. Selanjutnya, Watu Lumbung termasuk dalam kategori cagar alam. Sedangkan, Masjid Kapal Semarang termasuk dalam kategori tempat ibadah.

2. **Menggunakan Cosine Similarity**

   Pada tahap sebelumnya, sudah berhasil mengidentifikasi korelasi antara nama tempat wisata dengan kategori wiasata. Sekarang, kita akan menghitung derajat kesamaan (similarity degree) antar nama tempat wisata dengan teknik cosine similarity. Di sini, kita menggunakan fungsi cosine_similarity dari library sklearn.

   ||

   Perhatikanlah output matriks di atas. Angka 1.0 mengindikasikan bahwa nama tempat wista pada kolom X (horizontal) memiliki kesamaan dengan nama tempat wisata pada baris Y (vertikal). Sebagai contoh, Taman Senjata dan Museum Layang-layang teridentifikasi sama (similar) dengan Museum Taman Prasasti. Contoh lain, Pulau Pelangi mirip dengan Pulau Pari.

3. **Mendapatkan rekomendasi**

   Pada tahap ini, akan dibuatkan sebuah fungsi bernama wisata_recommendations dengan beberapa parameter sebagai berikut:
   - place_name : nama tempat wisata (index kemiripan dataframe).
   - similarity_data : Dataframe mengenai similarity yang telah didefinisikan sebelumnya.
   - items : Nama dan fitur yang digunakan untuk mendefinisikan kemiripan, dalam hal ini adalah 'place_name', 'category', dan 'price'.
   - k : Jumlah top-N recommendation yang diberikan oleh sistem rekomendasi. Secara default, k bernilai 5.
   
   Fungsi wisata_recommendation adalah fungsi yang dibuat untuk menampilkan hasil rekomendasi berbasis konten berupa nama tempat wisata dengan kategori yang sama dengan nama tempat wisata yang pernah ditelusuri oleh pengguna. Sebelum fungsi dibuat, perlu diingat bahwa definisi dari sistem rekomendasi yang menyatakan bahwa keluaran sistem adalah berupa top-N recommendation. Oleh karena itu, nantinya untuk mendapatkan rekomendasi perlu diberikan sejumlah rekomendasi nama tempat wisata pada pengguna yang diatur pada parameter k.

   Pada fungsi wisata_recommendations digunakan juga fungsi argpartition() untuk proses pengambilan sejumlah nilai k tertinggi dari similarity data. Selanjutnya, mengambil data dari bobot (tingkat kesamaan) tertinggi ke terendah. Data ini dimasukkan ke dalam variabel bernama 'closest'. Berikutnya, perlu dihapus place_name yang dicari agar tidak muncul dalam daftar rekomendasi. Dalam kasus ini, akan dicari nama tempat wisata yang mirip dengan nama tempat wisata sebelumnya yang nanti di input dalam place_name, sehingga perlu drop place_name agar tidak muncul dalam daftar rekomendasi yang diberikan nanti. Contoh nama tempat wisata yang digunakan terlihat pada Tabel 9.

   Tabel 9.

   Pada Tabel 9, terlihat bahwa nama tempat wisata 'Entering the Silence : Becoming a Monk and a Writer (The Journals of Thomas Merton, V. 2)' yang ditulis oleh 'Thomas Merton'. Selanjutnya, digunakan fungsi wisata_recommendations untuk menampilkan rekomendasi 5 destinasi wisata teratas yang direkomendasikan sistem berdasarkan nama tempat wisata di Tabel 9. Hasilnya terlihat pada Tabel 10.

   Tabel 10.

### Model Development dengan Collaborative Filtering

Model sistem rekomendasi lainnya yang dapat digunakan adalah collaborative filtering. Dengan menggunakan model ini, dapat direkomendasikan item sesuai dengan preferensi pengguna di masa lalu. Hal ini sangat bermanfaat dalam sistem rekomendasi destinasi wisata, karena dengan melihat riwayat ulasan pengguna di masa lalu, kita dapat memberikan sistem rekomendasi yang lebih beragam dan tentunya sesuai dengan minat pengguna dilihat dari ulasan yang tinggi pada item tersebut. Pada proyek ini akan dibuat model collaborative filtering berdasarkan kesamaan antar pengguna (User-Based Collaborative Filtering).

Kelebihan Collaborative Filtering:
- Dapat memberikan rekomendasi yang sangat personal kepada pengguna karena memanfaatkan preferensi dan perilaku pengguna secara langsung.
- Dapat mengidentifikasi pola tersembunyi dalam data interaksi pengguna.
- Dapat menangkap data yang lebih kompleks dan dinamis.

Kekurangan Collaborative Filtering:
- Memerlukan data interaksi pengguna yang cukup untuk model belajar.
- Rentan terhadap masalah sparsity jika data interaksi pengguna rendah.
- Tidak cocok untuk pengguna baru yang belum memiliki interaksi (cold start).

1. **Persiapan data**

   Pertama-tama sebelum melakukan pemodelan, fitur 'User_Id' dan 'Place_Id' harus disandikan (encoding) terlebih dahulu menjadi indeks integer. Selanjutnya, dipetakan 'User_Id' dan 'Place_Id' ke tabel yang berkaitan, lalu mengubah data-data numerik menjadi tipe data float.

2. **Membagi Data Untuk Training dan Validasi**

   Sebelum dilakukan proses pembagian data. Dataset akan diacak terlebih dahulu agar distribusinya menjadi random. Setelah itu, dilakukan proses pembagian data menjadi data train dan validasi dengan komposisi 80:20. Namun sebelumnya, perlu dipetakan (mapping) data user dan nama tempat wisata menjadi satu value terlebih dahulu. Kemudian, dibuat rating dalam skala 0 sampai 1 agar mudah dalam melakukan proses training.

3. **Proses Training**

   Pada proses training model, model akan menghitung skor kecocokan antara pengguna dan nama tempat wisata dengan teknik embedding. Pertama, dilakukan proses embedding terhadap data user dan Place_Id. Selanjutnya, lakukan operasi perkalian dot product antara embedding user dan Place_Id. Selain itu, juga dapat ditambahkan bias untuk setiap user dan Place_Id. Skor kecocokan ditetapkan dalam skala [0, 1] dengan fungsi aktivasi sigmoid.

   Di sini, Model dibuatkan class RecommenderNet dengan keras Model class. Kode class RecommenderNet ini terinspirasi dari tutorial dalam situs keras dengan beberapa adaptasi layer yang menyesuaikan dengan kasus yang sedang dikerjakan. Class RecommenderNet ini akan berisi layer yang akan melatih model. Setelah layer model sudah dibuat, dilakukan proses compile terhadap model menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan root mean squared error (RMSE) sebagai metrics evaluation.

   Berdasarkan hasil proses training model, didapat hasil yang cukup memuaskan dan model konvergen pada epochs sekitar 50. Dari proses ini, diperoleh nilai Root Mean Squared Error (RMSE) sebesar sekitar 0.2939 dan RMSE pada data validasi sebesar 0.3353. Nilai ini cukup bagus untuk sistem rekomendasi. Untuk mengetahui hasil dari pengembangan model, langkah selanjutnya adalah mendapatkan rekomendasi destinasi wisata berdasarkan model yang dikembangan.

4. **Mendapatkan Rekomendasi Destinasi Wisata**

   Untuk mendapatkan rekomendasi destinasi wisata, pertama diambil sampel user secara acak dan definisikan variabel place_not_readed yang merupakan daftar destinasi wiasata yang belum pernah dikunjungi oleh pengguna. variabel place_not_readed inilah yang akan menjadi destinasi wisata yang direkomendasikan oleh sistem. Variabel place_bot_visited diperoleh dengan menggunakan operator bitwise (~) pada variabel place_readed_by_user. Selanjutnya, untuk memperoleh rekomendasi destinasi wiasata, digunakan fungsi model.predict() dari library Keras dan hasil output akan menampilkan top-N recommendation berdasarkan preferensi pengguna seperti terlihat pada Tabel 11 dan Tabel 12.

   Berdasarkan Tabel 11 dan Tabel 12, model telah berhasil membuat rekomendasi kepada user. Hasil tersebut adalah rekomendasi untuk user dengan id 276798. Dari output tersebut, dapat dibandingkan antara 'Book with high ratings from user' dan 'Top 10 books recomendation' untuk user. Perhatikan, beberapa judul buku rekomendasi menyediakan nama penulis bukunya juga yang sesuai dengan rating user. Diperoleh 10 rekomendasi teratas buku yang disertai juga dengan nama penulisnya untuk user tersebut serta terdapat 1 judul buku yang merupakan buku dengan rating tertinggi dari user.

## Evaluation



## Referensi

[1] M. Zaenal Arifin. (2023). "Indonesia Negara Terindah…. Nomor Satu di Dunia." Dinas Pariwisata Provinsi Kaltim (https://dispar.kaltimprov.go.id/2023/02/15/indonesia-negara-terindah-no-1-dunia/)

[2] Tuwungkuya, Yudha Sagitama (2021). "STRATEGI PENGEMBANGAN PANTAI 1000 BINTANG SEBAGAI DESTINASI WISATA DI DESA MASANI KECAMATAN POSO PESISIR KABUPATEN POSO." Undergraduate thesis, UNIVERSITAS SINTUWU MAROSO.(https://repository.unsimar.ac.id/1299/4/BAB%20I.pdf)

[3] Kementerian Pariwisata dan Ekonomi Kreatif. (2024). "Statistik Kunjungan Wisatawan Mancanegara Bulan Januari 2024." (https://kemenparekraf.go.id/direktori-statistik/statistik-kunjungan-wisatawan-mancanegara-bulan-januari-2024)

[4] Liputan6. (2024). "Indeks Pariwisata Indonesia Ranking ke-22 Dunia pada 2024, Kembali Lampaui Malaysia dan Thailand." (https://www.liputan6.com/lifestyle/read/5602060/indeks-pariwisata-indonesia-ranking-ke-22-dunia-pada-2024-kembali-lampaui-malaysia-dan-thailand?page=4)


