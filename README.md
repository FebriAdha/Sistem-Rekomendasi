# Laporan Proyek Machine Learning - Febri Isthifa Adha

![dataset cover](https://raw.githubusercontent.com/FebriAdha/Sistem-Rekomendasi-Destinasi-Wisata/refs/heads/main/images/dataset-cover.jpg)

## Project Overview

### Latar Belakang

Indonesia, sebagai negara kepulauan terbesar di dunia, memiliki potensi pariwisata yang sangat kaya dan beragam. Dengan lebih dari 17.000 pulau yang luar biasa dan punya 50.000 kilometer garis pantai. Indonesia sendiri memiliki sejumlah destinasi wisata populer yang menawarkan keindahan alam, antara lain Bali, hutan tropis di Sumatera dan Kalimantan, serta kawasan cagar alam orang utan di Kalimantan. Tak ketinggalan, ada juga Taman Nasional Komodo yang menjadi salah satu situs warisan dunia UNESCO. [[1]](https://dispar.kaltimprov.go.id/2023/02/15/indonesia-negara-terindah-no-1-dunia/). Sektor pariwisata di Indonesia tidak hanya berfungsi sebagai sumber pendapatan devisa negara, tetapi juga berperan penting dalam meningkatkan kesejahteraan masyarakat lokal dan pelestarian lingkungan [[2]](https://repository.unsimar.ac.id/1299/4/BAB%20I.pdf).

Berdasarkan jumlah kunjungan wisatawan mancanegara ke Indonesia melalui seluruh pintu masuk bulan Januari 2024 sebesar 927.746 terdiri dari 760.036 kunjungan atau 81,93% melalui pencatatan imigrasi dan 167.710 kunjungan atau 18,07% melalui pencatatan Mobile Positioning Data pada pintu masuk perbatasan [[3]](https://kemenparekraf.go.id/direktori-statistik/statistik-kunjungan-wisatawan-mancanegara-bulan-januari-2024). Dalam daftar yang dirilis World Economic Forum (WEF) pada 21 Mei 2024, posisi Indonesia kembali naik 10 peringkat, dari rangking 32 menjadi 22 dunia. Berdasarkan data TTDI 2024, Indonesia mendapat skor 4,46 dengan posisi sembilan peringkat di bawah Singapura yang meraih skor 4,76 dan berada di ranking 13 [[4]](https://www.liputan6.com/lifestyle/read/5602060/indeks-pariwisata-indonesia-ranking-ke-22-dunia-pada-2024-kembali-lampaui-malaysia-dan-thailand?page=4). 

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
1. **Pengelolaan data**
   - Mengumpulkan data destinasi wisata pada daerah yang sering dikunjungi oleh masyarakat.
   - Mempersiapkan data dengan preprocessing dan preparation agar dapat dimodelkan dengan sistem rekomendasi yang sesuai.

2. **Modeling**

   Pada proses pengembangan model akan menggunakan dua metode sebagai berikut:
   - **Model Development dengan Content Based Filtering**. Pada tahap ini, dikembangkan sistem rekomendasi dengan teknik Content Based Filtering. Teknik ini akan merekomendasikan destinasi wisata yang sesuai dengan nama tempat wisata dan kategori yang disukai pengguna di masa lalu. Pada tahap ini, akan dicari representasi fitur penting dari setiap kategori buku dengan TF-IDF (Term Frequency - Inverse Document Frequency) Vertorizer dan menghitung tingkat kesamaan (similarity measure) dengan cosine similarity. Setelah itu akan menghasilkan sejumlah rekomendasi destinasi wisata untuk pengguna berdasarkan kesamaan yang telah dihitung sebelumnya.
   - **Model Development dengan Collaborative Filtering**. Pada tahap ini, dikembangan sistem rekomendasi dengan teknik Collaborative Filtering. Sistem nantinya akan merekomendasikan sejumlah destinasi wisata kepada pengguna berdasarkan rating yang telah diberikan sebelumnya. Dari data rating pengguna akan diidentifikasi nama - nama tempat wisata yang mirip dan belum pernah dikunjungi oleh pengguna lainnya.

## Data Understanding

![dataset](https://raw.githubusercontent.com/FebriAdha/Sistem-Rekomendasi-Destinasi-Wisata/refs/heads/main/images/dataset.png)

Dataset yang digunakan dalam proyek ini adalah dataset [Indonesia Tourism Destination](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination) yang diambil dari platfrom Kaggle. File yang digunakan berupa file csv, yaitu `tourism_ with _id.csv` dengan 437 baris dan 9 kolom, `tourism_rating.csv` dengan 10000 baris dengan 3 kolom, dan `user.csv` dengan 300 baris dan 3 kolom.

### Exploratory Data Analysis - EDA

Kemudian dilakukan proses Exploratory Data Analysis (EDA) yang merupakan proses investigasi awal pada data untuk menganalisis karakteristik, menemukan pola, anomali, dan memeriksa asumsi pada data.

**Variabel-variabel pada Destinasi Wisata Indonesia**

- **tourism_ with _id** : berisi informasi tempat wisata di 5 kota besar di Indonesia yang berjumlah ~400
- **tourism_rating** : berisi 3 kolom yaitu user, tempat, dan rating yang diberikan, berfungsi untuk membuat sistem rekomendasi berdasarkan rating yang diberikan
- **user** : yang berisi data pengguna dummy untuk membuat fitur rekomendasi berdasarkan pengguna

**Deskripsi Variabel**

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

4. Visualisasi Data

   - Distribusi Rating Destinasi Wisata

     ![Distribusi rating](https://raw.githubusercontent.com/FebriAdha/Sistem-Rekomendasi-Destinasi-Wisata/refs/heads/main/images/destribusi%20rating.png)

     Gambar 1. Distribusi Rating Destinasi Wisata.

     Distribusi rating destinasi wisata pada grafik menunjukkan jumlah destinasi dengan rating 2 hingga 4 mendominasi, masing-masing mencapai sekitar 2000 destinasi. Destinasi dengan rating 1 lebih sedikit (~1750), sedangkan rating 5 sedikit di bawah distribusi tengah. Hal ini mencerminkan kualitas destinasi yang cukup merata, dengan peluang peningkatan agar lebih banyak destinasi mencapai rating terbaik.

   - Jumlah destinasi wisata menurut kategori

     ![Jumlah destinasi](https://raw.githubusercontent.com/FebriAdha/Sistem-Rekomendasi-Destinasi-Wisata/refs/heads/main/images/jumlah%20destinasi%20wisata.png)

     Gambar 2.  Jumlah destinasi wisata per kategori

     Grafik ini menunjukkan jumlah destinasi wisata per kategori. Taman Hiburan memiliki jumlah terbanyak, diikuti oleh Budaya dan Cagar Alam. Kategori Bahari cukup signifikan, namun Tempat Ibadah dan Pusat Perbelanjaan memiliki jumlah yang paling sedikit. Hal ini membuat opsi wisata cenderung lebih kepada taman hiburan, budaya, dan alam, dibandingkan kategori lainnya.

   -  Distribusi Top 10 Destinasi Wisata

      ![Distribusi Top 10](https://raw.githubusercontent.com/FebriAdha/Sistem-Rekomendasi-Destinasi-Wisata/refs/heads/main/images/top%2010%20destinasi%20wisata.png)

      Gambar 3. Distribusi Top 10 Destinasi Wisata

      Berdasarkan informasi diatas, diketahui bahwa destinasi wisata dengan nama lokasi Gereja Perawan Maria Tak Berdosa Surabaya dengan rating tertinggi yaitu dengan jumlah diatas 400

## Data Preparation

Pada tahap data preparation, dilakukan serangkaian langkah untuk memastikan bahwa data yang digunakan dalam proses pemodelan bersih, terstruktur, dan siap untuk dianalisis.

### 1. Data Preprocessing

Seperti yang sudah diketahui berdasarkan tahapan data understanding bahwa Indonesia Tourism Destination Dataset terdiri dari 3 file terpisah yaitu tourism_ with _id, user, dan tourism_rating. Pada tahap ini, akan dilakukan proses penggabungan file menjadi satu kesatuan file agar sesuai dengan pengembangan model yang ingin dibuat. Variabel setelah dilakukan penggabungan menjadi 6 variabel dengan 10.000 baris data. Tampilan Dataset bisa dilihat pada Tabel 4, dataset inilah yang akan digunakan untuk membuat sistem rekomendasi.

Tabel 4. Tampilan dari dataset yang sudah dilakukan proses penggabungan antara variabel tourism_rating dan tourism_with_id
|	 | User_Id | Place_Id | Place_Ratings | Place_Name                    | Category      | Price |
|---|---------|----------|---------------|-------------------------------|---------------|-------|
| 0 |	1	     | 179	    | 3	           | Candi Ratu Boko               | Budaya        | 75000 |
| 1 |	1	     | 344	    | 2	           | Pantai Marina	                | Bahari	     | 3000  |
| 2 |	1	     | 5	       | 5	           | Atlantis Water Adventure      | Taman_Hiburan | 94000 |
| 3 |	1	     | 373	    | 3	           | Museum Kereta Ambarawa	       | Budaya        | 10000 |
| 4 |	1	     | 101	    | 4	           | Kampung Wisata Sosro Menduran |	Budaya        | 0     |

### 2. Mengatasi missing value.
     
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

### 3. Menyamakan nama tempat wisata

Sebelum masuk tahap pemodelan, diperlukan proses menyamakan nama tempat wisata berdasarkan Place_Id-nya. Jika terdapat Place_Id yang sama pada lebih dari satu nama tempat dapat menyebabkan bias pada data. Oleh karena itu harus dipastikan bahwa hanya terdapat satu Place_Id pada satu nama tempat saja. Pada proses ini dilakukan pengecekan ulang data setelah proses cleaning pada tahap sebelumnya. Berdasarkan informasi pada dataset, diketahui bahwa jumlah Place_Id dengan jumlah nama tempat wisata tidak sama, artinya terdapat Place_Id yang sama pada lebih dari satu nama tempat wisata. Oleh karena itu, diatasi dengan mengubah datasetnya menjadi data unik sehingga nantinya siap dimasukkan ke dalam proses pemodelan dengan cara membuang data duplikat pada kolom 'Place_Id'. Setelah melewati proses menyamakan jumlah dari jenis buku berdasarkan Place_Id, dataset hanya tersisa 437 baris data. Tahap berikutnya yaitu dibuatkan dictionary untuk menentukan pasangan key-value pada data place_id, place_name, place_category, dan price yang sudah disiapkan sebelumnya untuk proses pengembangan model sistem rekomendasi berbasis konten (content-based filtering). Hasil pembuatan dictionary disimpan dalam variabel bernama tourism_new dan terlihat seperti pada Tabel 5.

Tabel 5. Tampilan tourism_new setelah mengatasi missing value dan menyamakan nama tempat wisata
|	 | id	 | place_name	                  | category      | price |
|---|-----|-------------------------------|---------------|-------|
| 0 |	179 |	Candi Ratu Boko               | Budaya	       | 75000 |
| 1 |	344 |	Pantai Marina	               | Bahari        | 3000  |
| 2 |	5	 | Atlantis Water Adventure      | Taman_Hiburan | 94000 |
| 3 |	373 |	Museum Kereta Ambarawa        | Budaya	       | 10000 |
| 4 |	101 |	Kampung Wisata Sosro Menduran	| Budaya        |	0     |

### 4. Model Development dengan Content Based Filtering

Pada tahap ini, dilakukan beberapa langkah untuk menyiapkan data yang akan digunakan dalam model content-based filtering. Berikut langkah-langkah data preparation yang dilakukan:

1. **Menggunakan TF-IDF Vectorizer**

   TF-IDF Vectorizer digunakan untuk menemukan representasi fitur penting dari setiap kategori destinasi wisata. Dalam menggunakan TF-IDF Vectorizer, beberapa tahapnya adalah sebagai berikut.
   - Menginisialisasi TF-IDF Vectorizer dari library sklearn.
   - Melakukan perhitungan IDF pada data destinasi wisata.
   - Melakukan mapping fitur index ke fitur nama desrtinasi kategori.
   - Membentuk matriks TF-IDF.

   Setelah dibawa ke dalam bentuk matriks, akan didapatkan nilai-nilai untuk setiap tempat wisata berdasarkan kategorinya. Salah satu contohnya adalah seperti berikut.

   Tabel 6. TF-IDF Vectorizer
   | place_name                         | bahari | budaya | cagar_alam | pusat_perbelanjaan | taman_hiburan | tempat_ibadah |
   |------------------------------------|--------|--------|------------|--------------------|---------------|---------------|
   | Pantai Samas	                      | 1.0    |	0.0    |	0.0        | 0.0	              | 0.0	         | 0.0           |
   | Sunrise Point Cukul	             | 0.0    |	0.0    |	1.0	     | 0.0	              | 0.0	         | 0.0           |
   | Pantai Ancol	                      | 1.0    |	0.0    |	0.0	     | 0.0	              | 0.0	         | 0.0           |
   | Taman Budaya Yogyakarta            |	0.0    |	1.0    |	0.0	     | 0.0	              | 0.0	         | 0.0           |

   Output matriks tf-idf di atas menunjukkan Pantai Samas memiliki kategori bahari. Hal ini terlihat dari nilai matriks 1.0 pada kategori bahari. Selanjutnya, Sunrise Point Cukul termasuk dalam kategori cagar alam. Sedangkan, Taman Budaya Yogyakarta termasuk dalam kategori budaya.

3. **Menggunakan Cosine Similarity**

   Pada tahap sebelumnya, sudah berhasil mengidentifikasi korelasi antara nama tempat wisata dengan kategori wiasata. Sekarang, kita akan menghitung derajat kesamaan (similarity degree) antar nama tempat wisata dengan teknik cosine similarity. Di sini, kita menggunakan fungsi cosine_similarity dari library sklearn.

   Tabel 7. Cosine Similarity
   | place_name                            | Taman Suropati | Monumen Bandung Lautan Api | Grand Indonesia Mall | Kampoeng Rawa |	Bukit Wisata Pulepayung |
   |---------------------------------------|----------------|----------------------------|----------------------|---------------|-------------------------|
   | Museum Sepuluh Nopember Kota Surabaya | 0.0	           | 1.0	                      | 0.0	               | 0.0	          | 0.0                     |
   | Monumen Palagan Ambarawa	            | 0.0	           | 1.0	                      | 0.0	               | 0.0	          | 0.0                     |
   | Taman Ayodya	                        | 1.0	           | 0.0	                      | 0.0	               | 0.0	          | 0.0                     |
   | Hutan Mangrove Kulon Progo            | 0.0	           | 0.0	                      | 0.0	               | 0.0	          | 0.0                     |
   
   Perhatikanlah output matriks di atas. Angka 1.0 mengindikasikan bahwa nama tempat wista pada kolom X (horizontal) memiliki kesamaan dengan nama tempat wisata pada baris Y (vertikal). Sebagai contoh, Museum Sepuluh Nopember Kota Surabaya dan Monumen Palagan Ambarawa teridentifikasi sama (similar) dengan Monumen Bandung Lautan Api. Contoh lain, Taman Ayodya mirip dengan Taman Suropati.

5. **Mendapatkan rekomendasi**

   Pada tahap ini, akan dibuatkan sebuah fungsi bernama wisata_recommendations dengan beberapa parameter sebagai berikut:
   - place_name : nama tempat wisata (index kemiripan dataframe).
   - similarity_data : Dataframe mengenai similarity yang telah didefinisikan sebelumnya.
   - items : Nama dan fitur yang digunakan untuk mendefinisikan kemiripan, dalam hal ini adalah 'place_name', 'category', dan 'price'.
   - k : Jumlah top-N recommendation yang diberikan oleh sistem rekomendasi. Secara default, k bernilai 5.
   
   Fungsi wisata_recommendation adalah fungsi yang dibuat untuk menampilkan hasil rekomendasi berbasis konten berupa nama tempat wisata dengan kategori yang sama dengan nama tempat wisata yang pernah ditelusuri oleh pengguna. Sebelum fungsi dibuat, perlu diingat bahwa definisi dari sistem rekomendasi yang menyatakan bahwa keluaran sistem adalah berupa top-N recommendation. Oleh karena itu, nantinya untuk mendapatkan rekomendasi perlu diberikan sejumlah rekomendasi nama tempat wisata pada pengguna yang diatur pada parameter k.

   Pada fungsi wisata_recommendations digunakan juga fungsi argpartition() untuk proses pengambilan sejumlah nilai k tertinggi dari similarity data. Selanjutnya, mengambil data dari bobot (tingkat kesamaan) tertinggi ke terendah. Data ini dimasukkan ke dalam variabel bernama 'closest'. Berikutnya, perlu dihapus place_name yang dicari agar tidak muncul dalam daftar rekomendasi. Dalam kasus ini, akan dicari nama tempat wisata yang mirip dengan nama tempat wisata sebelumnya yang nanti di input dalam place_name, sehingga perlu drop place_name agar tidak muncul dalam daftar rekomendasi yang diberikan nanti. 

### 5. Model Development dengan Collaborative Filtering

Pada tahap data preparation untuk model collaborative filtering, dilakukan beberapa langkah penting agar data siap digunakan dalam proses pelatihan model. Berikut adalah penjelasan langkah-langkah tersebut:

1. **Persiapan data**

   Pertama-tama sebelum melakukan pemodelan, fitur 'User_Id' dan 'Place_Id' harus disandikan (encoding) terlebih dahulu menjadi indeks integer. Selanjutnya, dipetakan 'User_Id' dan 'Place_Id' ke tabel yang berkaitan, lalu mengubah data-data numerik menjadi tipe data float.

2. **Membagi Data Untuk Training dan Validasi**

   Sebelum dilakukan proses pembagian data. Dataset akan diacak terlebih dahulu agar distribusinya menjadi random. Setelah itu, dilakukan proses pembagian data menjadi data train dan validasi dengan komposisi 80:20. Namun sebelumnya, perlu dipetakan (mapping) data user dan nama tempat wisata menjadi satu value terlebih dahulu. Kemudian, dibuat rating dalam skala 0 sampai 1 agar mudah dalam melakukan proses training.

3. **Proses Training**

   Pada proses training model, model akan menghitung skor kecocokan antara pengguna dan nama tempat wisata dengan teknik embedding. Pertama, dilakukan proses embedding terhadap data user dan Place_Id. Selanjutnya, lakukan operasi perkalian dot product antara embedding user dan Place_Id. Selain itu, juga dapat ditambahkan bias untuk setiap user dan Place_Id. Skor kecocokan ditetapkan dalam skala [0, 1] dengan fungsi aktivasi sigmoid.

   Di sini, Model dibuatkan class RecommenderNet dengan keras Model class. Kode class RecommenderNet ini terinspirasi dari tutorial dalam situs keras dengan beberapa adaptasi layer yang menyesuaikan dengan kasus yang sedang dikerjakan. Class RecommenderNet ini akan berisi layer yang akan melatih model. Setelah layer model sudah dibuat, dilakukan proses compile terhadap model menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan root mean squared error (RMSE) sebagai metrics evaluation.

   Berdasarkan hasil proses training model, didapat hasil yang cukup memuaskan dan model konvergen pada epochs sekitar 50. Dari proses ini, diperoleh nilai Root Mean Squared Error (RMSE) sebesar sekitar 0.2939 dan RMSE pada data validasi sebesar 0.3353. Nilai ini cukup bagus untuk sistem rekomendasi. Untuk mengetahui hasil dari pengembangan model, langkah selanjutnya adalah mendapatkan rekomendasi destinasi wisata berdasarkan model yang dikembangan.

4. **Mendapatkan Rekomendasi Destinasi Wisata**

   Untuk mendapatkan rekomendasi destinasi wisata, pertama diambil sampel user secara acak dan definisikan variabel `place_not_readed` yang merupakan daftar destinasi wiasata yang belum pernah dikunjungi oleh pengguna. variabel `place_not_readed` inilah yang akan menjadi destinasi wisata yang direkomendasikan oleh sistem. Variabel place_bot_visited diperoleh dengan menggunakan operator bitwise (~) pada variabel `place_readed_by_user`. Selanjutnya, untuk memperoleh rekomendasi destinasi wiasata, digunakan fungsi model.predict() dari library Keras dan hasil output akan menampilkan top-N recommendation berdasarkan preferensi pengguna.

## Modeling and Result

Dalam menyusun sistem rekomendasi destinasi wisata, dilakukan 2 pendekatan yaitu content based filtering dan collaborative filtering. Dengan content based filtering, dapat direkomendasikan destinasi wisata yang serupa berdasarkan lokasi yang pernah diulas oleh pengguna di masa lalu. Sementara itu, untuk collaborative filtering akan digunakan algoritma neural network RecommendationNet untuk menghasilkan serangkaian rekomendasi berdasarkan nilai-nilai ulasan yang ditinggalkan oleh pengguna pada berbagai destinasi wisata di masa lalu.

### 1. Content Based Filtering

Model yang digunakan pada Content-Based Filtering ini adalah model klasik yang memanfaatkan cosine similarity untuk menentukan kemiripan karakteristika antardestinasi. Pembangunan model dilakukan dengan menghitung cosine similarity dari matriks fitur. Setelah itu dibuat sebuah fungsi untuk memberikan rekomendasi dengan memanfaatkan data cosine similarity dan data masukan berupa nama tempat serta jumlah rekomendasi. Fungsi rekomendasi ini mengurutkan tempat-tempat selain masukan berdasarkan nilai cosine similarity yang terbesar. Fungsi rekomendasi ini kemudian akan mengembalikan dataframe dari top-n recommendation.

Kelebihan teknik Content Based Filtering:
- Memberikan rekomendasi yang personal untuk setiap pengguna berdasarkan preferensi unik pengguna.
- Cocok untuk mengatasi masalah cold-start (ketika sedikit data pengguna tersedia) dan dapat memberikan rekomendasi yang baik sejak awal.
- Tidak tergantung pada data pengguna lain.
- Cocok untuk item dengan fitur atau atribut yang mudah diukur atau diidentifikasi.

Kekurangan teknik Content Based Filtering:
- Tidak efektif dalam menangani kejutan, karena hanya merekomendasikan item yang serupa dengan yang sudah diketahui pengguna.
- Kesulitan dalam menangkap preferensi yang kompleks atau dinamis dari pengguna, terutama jika item yang serupa tidak mencerminkan preferensi yang mendalam.
- Ada risiko "filter bubble" di mana pengguna hanya menerima rekomendasi yang sesuai dengan preferensi pengguna yang sudah diketahui, tanpa diverifikasi.

**Output Model**

Tabel 8. Contoh nama tempat destinasi yang digunakan untuk menampilkan rekomendasi
|	   | id  | place_name        | category | price |
|-----|-----|-------------------|----------|-------|
| 357 | 172 | Pantai Indrayanti | Bahari   | 10000 |

Tabel 9. Hasil rekomendasi 5 nama tempat destinasi teratas dengan kateogri
|	 | place_name          | category | price |
|---|---------------------|----------|-------|
| 0 |	Pantai Ngrenehan    | Bahari   | 3000  |
| 1 |	Pantai Drini        | Bahari   | 10000 |
| 2 |	Pantai Pulang Sawal | Bahari   | 10000 |
| 3 |	Pantai Ancol        | Bahari   | 25000 |
| 4 |	Pantai Krakal       | Bahari   | 10000 |

Berdasarkan output diatas, sistem berhasil merekomendasikan 5 nama tempat wisata teratas dengan kategori wisata 'category' yaitu 'Bahari' beserta harga tiket masuk.

### 2. Collaborative Filtering

Model yang digunakan dalam Collaborative Filtering ini adalah model Deep Learning dengan menggunakan Embedding Layer. Pembangunan model diawali dengan inisialisasi struktur layer pada kelas yang merupakan turunan dari kelas ff.keras.model. Inisialisasi dilakukan dengan membuat layer bias dan layer embedding dari fitur yang digunakan dalam collaborative filtering. Fitur yang digunakan adalah Place Id dan User Id. Setelah itu, definisikan method Call pada kelas untuk menerima input dan mengembalikan prediksi nilai rating dari user terhadap suatu tempat. Tahap ini melibatkan proses perkalian dot dari vector kedua atribut yang ditambah dengan kedua biasnya. Setelah siap, model akan dicompile agar dapat digunakan. Setelah itu, dilakukan training pada model menggunakan data train.

Kelebihan Collaborative Filtering:
- Dapat memberikan rekomendasi yang sangat personal kepada pengguna karena memanfaatkan preferensi dan perilaku pengguna secara langsung.
- Dapat mengidentifikasi pola tersembunyi dalam data interaksi pengguna.
- Dapat menangkap data yang lebih kompleks dan dinamis.

Kekurangan Collaborative Filtering:
- Memerlukan data interaksi pengguna yang cukup untuk model belajar.
- Rentan terhadap masalah sparsity jika data interaksi pengguna rendah.
- Tidak cocok untuk pengguna baru yang belum memiliki interaksi (cold start).

**Output Model**

```
Daftar rekomendasi untuk: User 86
============================================= 

------------------------------------------------------------
Destinasi wisata dengan rating paling tinggi dari user
------------------------------------------------------------
Pulau Bidadari : Bahari
Taman Spathodea : Taman_Hiburan
Pasar Kebon Empring Bintaran : Pusat_Perbelanjaan
Taman Bunga Cihideung : Cagar_Alam
Kampung Pelangi : Taman_Hiburan

------------------------------------------------------------
Top 10 Destinasi Wisata recommendation
------------------------------------------------------------
1 . Kampoeng Tulip 
     Taman_Hiburan , Harga Tiket Masuk  15000 , Rating Wisata  3.8 

2 . Selasar Sunaryo Art Space 
     Taman_Hiburan , Harga Tiket Masuk  25000 , Rating Wisata  4.6 

3 . Teras Cikapundung BBWS 
     Taman_Hiburan , Harga Tiket Masuk  0 , Rating Wisata  4.3 

4 . Museum Barli 
     Budaya , Harga Tiket Masuk  15000 , Rating Wisata  4.4 

5 . Wisata Batu Kuda 
     Cagar_Alam , Harga Tiket Masuk  10000 , Rating Wisata  4.4 

6 . Ciwangun Indah Camp Official 
     Cagar_Alam , Harga Tiket Masuk  10000 , Rating Wisata  4.3 

7 . Curug Batu Templek 
     Cagar_Alam , Harga Tiket Masuk  5000 , Rating Wisata  4.1 

8 . Taman Jomblo 
     Taman_Hiburan , Harga Tiket Masuk  10000 , Rating Wisata  4.1 

9 . Masjid Agung Trans Studio Bandung 
     Tempat_Ibadah , Harga Tiket Masuk  0 , Rating Wisata  4.8 

10 . Curug Cilengkrang 
     Cagar_Alam , Harga Tiket Masuk  7500 , Rating Wisata  4.0 

=============================================
```

Berdasarkan output diatas, model telah berhasil membuat rekomendasi kepada user. Hasil tersebut adalah rekomendasi untuk user dengan id 86. Dari output tersebut, dapat dibandingkan antara 'Destinasi wisata dengan rating paling tinggi dari user' dan 'Top 10 Destinasi Wisata recommendation' untuk user. Perhatikan, beberapa destinasi wisata rekomendasi menyediakan nama tempat wisata juga yang sesuai dengan kategori, harga dan rating user. Diperoleh 10 top rekomendasi destinasi wisata yang disertai juga dengan kategori untuk user tersebut serta terdapat 1 destinasi wisata yang merupakan nama tempat wisata dengan kategori, harga, dan rating tertinggi dari user.

## Evaluation

### Evaluasi Model dengan Content Based Filtering

Metrik yang digunakan untuk mengevaluasi model dengan pendekatan content-based filtering pada proyek ini meliputi Precision, Recall, dan F1-Score. Ketiga metrik ini merupakan ukuran yang sering digunakan untuk menilai performa model rekomendasi. Precision mengukur rasio jumlah item relevan yang dihasilkan oleh model dibandingkan dengan total item yang direkomendasikan. Recall mengukur rasio jumlah item relevan yang dihasilkan oleh model dibandingkan dengan total item relevan yang seharusnya direkomendasikan. Sementara itu, F1-Score adalah metrik yang menggabungkan Precision dan Recall, memberikan nilai tunggal yang menunjukkan keseimbangan antara keduanya. Berikut adalah rumus untuk menghitung Precision, Recall, dan F1-Score pada model sistem rekomendasi berbasis konten:

$$Precision = \frac{Jumlah\ item\ revelan\ yang\ dihasilkan}{Total\ item\ yang\ dihasilkan}$$

$$Recall = \frac{Jumlah\ item\ relevan\ yang\ dihasilkan}{Total\ item\ yang\ seharusnya\ direkomendasikan}$$

$$F1\ Score = 2 * \frac{Precision * Recall}{Precision + Recall}$$

Sebelum menghitung nilai evaluasi menggunakan metrik Precision, Recall, dan F1-Score, diperlukan data referensi yang berfungsi sebagai acuan untuk menilai hasil prediksi model. Data ini dikenal sebagai data ground truth. Dalam proyek ini, data ground truth dibuat berdasarkan derajat kesamaan yang dihitung menggunakan teknik cosine similarity. Setiap baris dan kolom pada dataframe mewakili judul buku, sementara nilai pada setiap sel menunjukkan label. Nilai 1 digunakan untuk menandai item yang similar (mirip), dan nilai 0 untuk item yang tidak similar. Nilai ambang batas atau threshold ditetapkan sebesar 0.5 pada proyek ini. Nilai threshold ini disesuaikan dengan kebutuhan dan karakteristik setelah melihat hasil rekomendasi sebelumnya. Lalu dibuatkan matriks ground truth menggunakan fungsi np.where() dari NumPy. Matriks ini akan memiliki nilai 1 di posisi di mana nilai cosine similarity antara dua item lebih besar atau sama dengan nilai threshold yang ditetapkan, dan nilai 0 di posisi di mana nilai similarity di bawah threshold. Kemudian, setelah matriks dibuat, hasilnya disajikan dalam bentuk dataframe. Baris dan kolom Dataframe ground truth ini diindeks menggunakan nama tempat wisata dari data.

Terakhir, digunakan fungsi `precision_recall_fscore_support` untuk menghitung precision, recall, dan f1 score. Parameter average='binary' digunakan karena sedang mengukur kinerja dalam konteks klasifikasi biner (1 atau 0). Parameter 'zero_division=1' digunakan untuk menghindari pembagian dengan nol jika ada kelas yang tidak terdapat di prediksi. Hasil evaluasi metriks didapat adalah sebagai berikut:

- Precision: 1.0
- Recall: 1.0
- F1-score: 1.0

Berdasarkan hasil evaluasi, didapat nilai dari masing - masing metrik evaluasi yaitu precision, recall dan F1 Score. Nilai Precision didapat sebesar 1.0, artinya semua prediksi positif model adalah benar dan tidak terdapat false positive. Nilai recall didapat nilai 1.0 menunjukkan bahwa model berhasil mengidentifikasi sekitar 100% dari semua item yang sebenarnya relevan. Nilai F1 Score didapat sekitar 1.0 juga, ini menunjukkan keseimbangan yang baik antara precision dan recall dan model cenderung memberikan hasil yang sangat baik untuk kedua kelas (positif dan negatif). Kesimpulannya, berdasarkan hasil metrik evaluasi tersebut model bekerja dengan sangat baik dalam memberikan rekomendasi item dengan content based filtering.

### Evaluasi Model dengan Collaborative Filtering

Seperti yang sudah dilihat pada proses pelatihan model di bagian modeling. Metrik yang digunakan untuk melakukan evaluasi model pada model dengan Collaborative Filtering di proyek ini adalah Root Mean Squared Error (RMSE). RMSE adalah metrik evaluasi yang umum digunakan untuk mengukur seberapa baik model memprediksi nilai kontinu dengan membandingkan nilai prediksi dengan nilai sebenarnya. Dalam konteks collaborative filtering, RMSE biasanya digunakan untuk mengukur seberapa baik model kolaboratif dalam memprediksi preferensi pengguna terhadap item. RMSE didefinisikan dalam persamaan berikut:

$$RMSE = \sqrt{\frac{1}{N} \Sigma_{i=1}^N({y_i}- y\_pred_i)^2}$$

Keterangan:
- N adalah jumlah prediksi.
- yi adalah nilai sebenarnya dari preferensi pengguna terhadap item.
- y_pred adalah prediksi model terhadap preferensi pengguna terhadap item.

Berdasarkan hasil proses training model pada tahap modeling, diperoleh hasil pelatihan berupa informasi RMSE di data train dan validasi. Untuk melihat visualisai proses training model, dilakukan proses plot metrik evaluasi dengan matplotlib dan terlihat seperti Gambar 2.

![model matrics](https://raw.githubusercontent.com/FebriAdha/Sistem-Rekomendasi-Destinasi-Wisata/refs/heads/main/images/model%20matrics.png)

Gambar 4. Model Matrics

Berdasarkan hasil visualisasi metrik evaluasi RMSE terhadap model yang dikembangkan, terlihat hasil model konvergen pada epochs sekitar 50 dan berdasarkan plot metriks model terlihat memberikan nilai MSE yang cukup kecil. Dari proses ini, diperoleh nilai error akhir sebesar 0.3288 dan error pada data validasi sebesar 0.3461. Nilai tersebut menunjukkan hasil yang cukup baik untuk sistem rekomendasi yang dihasilkan. Semakin kecil nilai RMSE, semakin baik model dalam memprediksi preferensi pengguna terhadap item. Hal inilah yang menyebabkan hasil rekomendasi dari model cukup akurat.

### Kesimpulan

Sistem rekomendasi yang dibangun berhasil memberikan rekomendasi destinasi wisata yang relevan dengan akurasi yang baik. Content-based filtering efektif untuk merekomendasikan destinasi serupa, sementara collaborative filtering baik dalam memberikan rekomendasi personal berdasarkan preferensi pengguna.

## Referensi

[1] M. Zaenal Arifin, "Indonesia Negara Terindah…. Nomor Satu di Dunia," Dinas Pariwisata Provinsi Kaltim, (2023). (https://dispar.kaltimprov.go.id/2023/02/15/indonesia-negara-terindah-no-1-dunia/)

[2] Tuwungkuya, Yudha Sagitama, "STRATEGI PENGEMBANGAN PANTAI 1000 BINTANG SEBAGAI DESTINASI WISATA DI DESA MASANI KECAMATAN POSO PESISIR KABUPATEN POSO," Undergraduate thesis, UNIVERSITAS SINTUWU MAROSO, (2021).(https://repository.unsimar.ac.id/1299/4/BAB%20I.pdf)

[3] Kementerian Pariwisata dan Ekonomi Kreatif, "Statistik Kunjungan Wisatawan Mancanegara Bulan Januari 2024," (2024).(https://kemenparekraf.go.id/direktori-statistik/statistik-kunjungan-wisatawan-mancanegara-bulan-januari-2024)

[4] Dinny Mutiah, "Indeks Pariwisata Indonesia Ranking ke-22 Dunia pada 2024, Kembali Lampaui Malaysia dan Thailand,"  Liputan6, (2024).(https://www.liputan6.com/lifestyle/read/5602060/indeks-pariwisata-indonesia-ranking-ke-22-dunia-pada-2024-kembali-lampaui-malaysia-dan-thailand?page=4)


