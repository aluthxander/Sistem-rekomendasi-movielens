# Laporan Proyek Machine Learning - Nama Anda

## Project Overview

Keragaman informasi yang tersedia di web sekarang ini mengalami pertumbuhan yang sangat pesat sehingga menimbulkan masalah baru bagi user untuk menemukan konten yang relvan dengan kebutuhannya. untuk itu, dibutuhkan suatu sistem yang dapat memfilter dan merekomendasikan konten yang sekiranya relevan bagi user. Pada saat ini, salah satu cara untuk melakukannya adalah dengan memanfaatkan machine learning. salah satu algoritma yang sangat populer adalah _Content-based Filtering_ dan *Collaborative Filtering*.  Pada proyek ini akan dibangun sistem rekomendasi *Content-based Filtering* dan *Collaborative Filtering* dengan menggunakan dataset **Movielens 100k** sebagai pembelajaran dasar dalam membangun sistem rekomendasi.  Dataset ini berasal dari situs rekomendasi film movielens.org milik tim riset GroupLens [1]. 
  
**Rubrik/Kriteria Tambahan (Opsional)**:

- Proyek ini penting untuk pembelajaran dasar dalam membangun sistem rekomendasi. karena setiap perusahaan mempunyai cara sendiri dalam membangun sistem rekomendasinya, proyek ini bisa menjadi pijakan dasar dalam membangun sistem rekomendasi.

  

## Business Understanding

### Problem Statements

Latar belakang masalah dari proyek ini adalah sebagai berikut :

- Apa itu sistem rekomendasi *Content-based Filtering* dan *Collaborative Filtering*?
- Bagaimana cara membangun sistem rekomendasi?
- Bagaimana cara mengevaluasi sisten rekomendasi tersebut?

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Mengetahui apa itu sistem rekomendasi *Content-based Filtering* dan *Collaborative Filtering*
- Mengetahui cara membangun sistem rekomendasi
- Mengetahui cara mengevaluasi sistem rekomendasi yang telah dibuat

  

**Rubrik/Kriteria Tambahan (Opsional)**:

- Untuk mencapai goals tersebut, saya melakukan riset diberbagai media seperti kaggle, medium, youtube dll. saya juga melakukan riset pada journal-journal ilmiah yang membahas tentang sistem rekomendasi.

  

### Solution statements

- Untuk membangun sistem rekomendasi *Content-based filtering* saya menggunakan pendekatan melalui genre film, dan untuk melakukannya saya menggunakan TF-IDF Vectorizer untuk menemukan representasi fitur penting dari setiap genre film. sedangkan untuk *similiarity* saya menggunakan 2 metode, yaitu *euclidean distances* dan *cosine similiarity*. kemudian saya akan membandingkan mana yang lebih bagus dari 2 metode similarity tersebut.
- Untuk membangun sistem rekomendasi Collaborative Filtering, saya menggunakan metode embedding. dimana metode ini melakukan proses embedding terhadap data user dan movie. Selanjutnya, dilakukan operasi perkalian dot product antara embedding user dan movie. Selain itu, saya juga dapat menambahkan bias untuk setiap user dan resto. Skor kecocokan ditetapkan dalam skala [0,1] dengan menggunakan fungsi aktivasi sigmoid.

  

## Data Understanding

Paragraf awal bagian ini menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).
Dataset **Movielens 100k** merupakan dataset yang berisi film beserat rating yang diberikan oleh masing-masing *users*.  Dataset ini berasal dari situs rekomendasi film movielens.org milik tim riset GroupLens [1]. Dataset ini berisi 3 file, file-file ini berisi 1.000.209 rating anonim dari sekitar 3.900 film  oleh 6.040 users MovieLens  2000. Untuk lebih lengkapnya tentang dataset ini bisa dilihat pada tautan berikut :\
[Movielens 100k](https://www.kaggle.com/datasets/sherinclaudia/movielens)
3 fil pada dataset ini adalah sebagai berikut :
- movies.dat
- ratings.dat
- users.dat
   
### movies
 Pada dataset movies mempunyai jumlah data 3883 yang terdiri dari 3 fitur, yaitu : 
1. `MovieID` merupakan ID pada masing-masing film.
2.  `Title` merupakan judul dari film
3.  `Genres` merupakan genre pada setiap film. Pada fitur ini terdapat 18 kategori, yaitu :
	* Action
	* Adventure
	* Animation
	* Children's
	* Comedy
	* Crime
	* Documentary
	* Drama
	* Fantasy
	* Film-Noir
	* Horror
	* Musical
	* Mystery
	* Romance
	* Sci-Fi
	* Thriller
	* War
	* Western

### ratings
Pada dataset ratings mempunyai jumlah data sebanyak 1000209 yang terdiri dari 4 fitur, yaitu :
1. `UserID` merupakan Id pada masing-masing user. Fitur ini memiliki jumlah unik user sebanyak 6040.
2. `MovieID` merupakan id pada masing-masing movie. Fitur ini memiliki jumlah unik movies sebanyak 3706.
3. `Rating` merupakan rating yang diberikan oleh user pada setiap film. Fitur ini mempunyai 5 unik rating yaitu 1,  2,3 ,4  dan 5.
4. `Timestamp`merupakan waktu penayangan film dalam bentuk detik.

### users
Pada dataset users, jumlah data sebanyak 6040 yang terdiri dari 5 fitur, yaitu :
1. `UserID` merupakan Id pada setiap user.
2. `Gender` merupakan jenis kelamin pada setiap user. fitur ini memiliki 2 kategori yaitu :
	* F : wanita
	* M: Pria
3. `Age` merupakan usia pada masing-masing user. fitur ini merepresentasikan usia pada range sebagai berikut:
	*  1:  "Under 18"
	* 18:  "18-24"
	* 25:  "25-34"
	* 35:  "35-44"
	* 45:  "45-49"
	* 50:  "50-55"
	* 56:  "56+"
4.  `Occupation` merupakan pekerjaan user. fitur ini memiliki 21 kode unik pekerjaan yaitu:
	*  0:  "other" or not specified
	*  1:  "academic/educator"
	*  2:  "artist"
	*  3:  "clerical/admin"
	*  4:  "college/grad student"
	*  5:  "customer service"
	*  6:  "doctor/health care"
	*  7:  "executive/managerial"
	*  8:  "farmer"
	*  9:  "homemaker"
	* 10:  "K-12 student"
	* 11:  "lawyer"
	* 12:  "programmer"
	* 13:  "retired"
	* 14:  "sales/marketing"
	* 15:  "scientist"
	* 16:  "self-employed"
	* 17:  "technician/engineer"
	* 18:  "tradesman/craftsman"
	* 19:  "unemployed"
	* 20:  "writer"

5. `Zip-code` merupakan kodepos yang dimiliki oleh masing-masing user.

**Rubrik/Kriteria Tambahan (Opsional)**:

- Dalam proses exploratory data analysis, saya menggunakan beberapa library standar yaitu pandas, matplotlip dan seaborn. karena dataset ini terdiri dari 3 file, hal pertama yang saya lakukan adalah melihat jumlah, bentuk, tipe dan fitur pada masing-masing file tersebut. 
- Selanjutnya saya melakukan proses Univariate EDA, pada proses ini saya mencari jumlah kategori dan kode unik pada masing-masing fitur dataset. untuk melakukannya saya menggunakan library pandas. disini saya mendapatkan insight berupa jenis genre yang mendominasi semua film pada dataset adalah *Drama* dan *Comedy*.
- Kemudian saya melakukan Bivariate EDA. Pada proses ini saya ingin mencari korelasi antar fitur. disini saya menggunakan representasi visual dengan menggunakan matplotlib dan seaborn. Hasilnya adalah sebagai berikut :\
![image](https://user-images.githubusercontent.com/87218279/183256759-c26088c6-8c7a-4e8b-882c-61afe6a2b87a.png)\
Dari grafik diatas dapat dianalisa bahwa kebanyakan penonton film didominasi oleh penonton dengan usia 25-34 tahun.\
![image](https://user-images.githubusercontent.com/87218279/183256789-c991df8d-277e-4f29-b4cd-b9ccc3867af3.png)\
Dari grafik diatas, mayoritas penonton film merupakan laki-laki.

## Data Preparation

Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.\
Pada bagian Data Preparation saya akan membagi menjadi 2 bagian :
1. **Data Preparation Content-based Filtering**
	- Mencari missing value 
	hal pertama yang saya lakukan adalah mencari *missing value* pada dataset movies dan hasilnya tidak ditemukan *missing value* pada dataset movies.  
	- Data Preprocessing
	tahap selanjutnya *Data Preprocessing*, karena pada proyek ini sistem rekomendasi yang saya buat berdasarkan genre film, jadi saya mengubah fitur `Genres` ke dalam bentuk **string array** hal ini dilakukan karena pada saat modeling nantinya menggunakan TF-IDF Vectorizer sehingga perlu mengubah fitur tersebut dalam bentuk string sehingga data siap untuk digunakan.
2. **Data Preparation Collaborative Filtering**
	- Mencari missing value
		Hal pertama yang saya lakukan adalah mencari missing value pada dataset ratings dan hasilnya tidak terdapat missing value. 
	- Data Preprocessing
		Selanjutnya melakukan  *Data Preprocessing*, pada tahap ini saya menggunakan library numpy untuk membantu saya dalam mengubah tipe data. Pada tahap ini saya melakukan persiapan data dengan encode fitur `User` dan `MovieID`. selanjutnya saya menggabungkan hasil encode tersebut ke dalam dataset. Pada tahap ini saya juga mengubah type data fitur `Rating` ke dalam bentuk float agar proses pelatihan menjadi lebih ringan.  Setelah itu saya mengecek beberapa data seperti jumlah user dan jumlah film yang akan saya gunakan untuk menentukan jumlah input pada layer embedding serta nilai minimum dan maksimum pada fitur `Rating` yang nantinya akan berguna saat melakukan normalisasi data.
	- Pembagian Dataset Training dan Validasi
		Pada tahap ini saya akan membagi dataset menjadi data training dan data validasi. Sebelum melakukannya, saya melakukan normalisasi pada  fitur `Ratings` yang tujuannya untuk meringankan proses training. setelah itu saya membagi dataset menggunakan fungsi `train_test_split()`pada library sklearn. Disini saya membagi data menjadi 80% data training dan 20% data testing, saya juga melakukan pengacakan data dengan mengisi parameter `random_state`.


## Modeling

Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.
### Content-based filtering
  Sistem rekomendasi Content-based filtering adalah sistem rekomendasi berdasarkan konten yang dilihat oleh user[2]. sistem rekomendasi ini akan merekomendasikan sesuatu berdasarkan kemiripan konten *item*.
  Untuk membangun sistem rekomendasi ini perlu dilakukan representasikan fitur-fitur penting dari setiap genre film dan mengukur *Similarity*(kesamaan) pada setiap fitur tersebut.\
  
  **TF-IDF Vectorizer**\
  Untuk melakuan representasikan fitur-fitur penting dari setiap genre film. saya menggunakan algorimat *TF-IDF*. TF-IDF merupakan suatu metode algoritma yang berguna untuk menghitung bobot setiap kata yang umum digunakan. Metode ini juga terkenal efisien, mudah dan memiliki hasil yang akurat. Metode ini akan menghitung nilai Term Frequency (TF) dan Inverse Document Frequency (IDF) pada setiap token (kata) di setiap dokumen dalam korpus. Secara sederhana, metode TF-IDF digunakan untuk mengetahui berapa sering suatu kata muncul di dalam dokumen[3]. Untuk melakukannya, library sklearn telah menyediakan fungsi tersebut yaitu `TfidfVectorizer`.  Cara menggunakannya pun mudah, yaitu dengan melakukan inisialisasi fungsi tersebut ke suatu variabel, kemudian lakukan `fit_transform` dengan memasukkan fitur yang  menjadi konten item dan hasilnya berupa array matrik.\

 **Similarity**\
 Setelah proses TF-IDF dilakukan, selanjutnya menghitung Similarity (kesamaan) antar film, disini saya menggunakan 2 metode Similarity yaitu euclidean distances dan cosinus similarity.\
Metode Euclidean distance dapat dipakai untuk mengetahui kemiripan dokumen. Metode ini menghitung jarak paling pendek antara dua titik apabila digunakan didalam dua dimensi[4]. Hasil yang didapat dengan menggunakan metode ini adalah sebagai berikut :
Film yang telah ditonton user:

| Title | Genres |
| :-----: | :---------: |
| Head (1995) | ['Action', 'Crime', 'Thriller'] |
	
Hasil rekomendasi sistem:
| Title | Genres |
| :-----: | :---------: |
| Father of the Bride Part II (1995) | ['Comedy'] |
| Tom and Huck (1995) | ['Adventure', "Children's"] |
| American President, The (1995) | ['Comedy', 'Drama', 'Romance'] |
| Dracula: Dead and Loving It (1995) | ['Comedy', 'Horror'] |
| Balto (1995) | ['Animation', "Children's"] |
| Nixon (1995) | ['Drama'] |
| Sense and Sensibility (1995) | ['Drama', 'Romance'] |
| Ace Ventura: When Nature Calls (1995) | ['Comedy'] |
| Powder (1995) | ['Drama', 'Sci-Fi'] |
| Leaving Las Vegas (1995) | ['Drama', 'Romance'] |
Dari tabel diatas, dapat diketahui bahwa film-film yang direkomendasikan oleh sistem masih kurang sesuai dengan yang diharapkan. Film yang telah ditonton oleh user bergenre ['Action', 'Crime', 'Thriller'] sedangkan film yang direkomendasikan kebanyakan diluar genre tersebut. Oleh karena itu saya mencoba menggunakan metode lain yiatu Cosinus similarity.\

Cosinus similarity Metode cosine similarity merupakan metode untuk menghitung kesamaan antara dua buah objek yang dinyatakan dalam dua buah vector dengan menggunakan keywords (kata kunci) dari sebuah dokumen sebagai ukuran[5]. Hasil yang didapat dengan menggunakan metode ini adalah sebagai berikut :
Film yang telah ditonton user:

| Title | Genres |
| :-----: | :---------: |
| Head (1995) | ['Action', 'Crime', 'Thriller'] |

Hasil rekomendasi sistem:
| Title | Genres |
| :-----: | :---------: |
| Hackers (1995) | ['Action', 'Crime', 'Thriller'] |
| Ronin (1998) | ['Action', 'Crime', 'Thriller'] |
| Someone to Watch Over Me (1987) | ['Action', 'Crime', 'Thriller'] |
| F/X (1986) | ['Action', 'Crime', 'Thriller'] |
| F/X 2 (1992) | ['Action', 'Crime', 'Thriller'] |
| Seven (Se7en) (1995) | ['Crime', 'Thriller'] |
| Usual Suspects, The (1995) | ['Crime', 'Thriller'] |
| Romeo Is Bleeding (1993) | ['Crime', 'Thriller'] |
| Purple Noon (1960) | ['Crime', 'Thriller'] |
| Reservoir Dogs (1992) | ['Crime', 'Thriller'] |
Dari tabel di atas dapat dilihat bahwa film-film yang direkomendasikan oleh sistem jauh lebih masuk akal dari pada tadi, Dari sini saya menyimpulkan bahwa penggunaan cosinus similarity lebih baik dari pada Euclidean distance untuk dataset ini.

### Collaborative filtering
Sistem collaborative filtering adalah metode yang digunakan untuk memprediksi kegunaan item berdasarkan penilaian pengguna , misalnya cara pemberian rating terhadap suatu item. Metode ini merekomendasikan item-item yang dipilih oleh pengguna lain dengan kemiripan model item dari pengguna saat ini.\
Untuk model sistem rekomendasi collaborative filtering pada proyek ini, model menghitung skor kecocokan antara pengguna dan movie dengan teknik embedding. Pertama, melakukan proses embedding terhadap data user dan movie. Selanjutnya, lakukan operasi perkalian dot product antara embedding user dan movie. Selain itu, saya juga dapat menambahkan bias untuk setiap user dan resto. Skor kecocokan ditetapkan dalam skala [0,1] dengan fungsi aktivasi sigmoid. Untuk ukuran embeddingnya adalah 32, Model ini menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan root mean squared error (RMSE) sebagai metrics evaluation.\
Dalam proses pelatihan, saya menggunakan 5 epoch dengan batch size 64 dan hasil dari pelatihan dapat dilihat dari grafik berikut :\
![image](https://user-images.githubusercontent.com/87218279/183256930-9e36edcd-a0d7-4e22-b0db-dd392605a9f4.png)
Dari proses ini, saya memperoleh nilai root_mean_squared_error sekitar 0.2573 dan val_root_mean_squared_error sebesar 0.2591. Nilai tersebut cukup bagus untuk sistem rekomendasi.

## Evaluation

Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.
### Content-based filtering
Untuk melakukan evaluasi model ini, saya hanya membandingkan hasil output model dengan hasil output model lain yang menggunakan metode lain.  model yang hasil outputnya berupa item-item yang kontennya hampir serupa dengan konten item yang telah ditonton oleh user maka model tersebut menjadi model terbaik.

### Collaborative filtering
Untuk melakukan evaluasi model ini saya menggunakan matrik evaluasi root mean squared error (RMSE). RMSE ini merupakan metode pengukuran dengan mengukur perbedaan nilai dari prediksi sebuah model sebagai estimasi atas nilai yang diobservasi. Root Mean Square Error adalah hasil dari akar kuadrat Keakuratan metode estimasi kesalahan pengukuran ditandai dengan adanya nilai RMSE yang kecil. Secara matematik adalah sebagai berikut:\
RMSE = ${\sqrt{\frac{1}{n}\Sigma_{i=1}^{n}{\Big(\frac{d_i -f_i}{\sigma_i}\Big)^2}}}$

 Metode estimasi yang mempunyai Root Mean Square Error (RMSE) lebih kecil dikatakan lebih akurat daripada metode estimasi yang mempunyai Root Mean Square Error (RMSE) lebih besar.  Untuk hasil pelatihannya dapat dilihat dari grafik berikut:\
 ![image](https://user-images.githubusercontent.com/87218279/183256939-616f30f4-9e95-4246-b631-53230b179bdf.png)


## Kesimpulan

Dari pembahasan diatas dapat diambil kesimpulan sebagai berikut:
- Sistem rekomendasi Content-based filtering adalah sistem rekomendasi berdasarkan konten yang dilihat oleh user[2]. sistem rekomendasi ini akan merekomendasikan sesuatu berdasarkan kemiripan konten _item_. sedangkan Sistem collaborative filtering adalah metode yang digunakan untuk memprediksi kegunaan item berdasarkan penilaian pengguna.
-  Tahap-tahap membangun sistem rekomendasi hampir sama dengan membangun model machine learning yaitu Data understanding, Data preparation & data preprocessing, Model Development terakhir Evaluation.
- Untuk mengevaluasi sistem rekomendasi content-based filtering hanya bisa dilakukan dengan membandingkan hasil output konten item dengan konten yang ada pada item yang telah dilihat oleh user. Sedangkan untuk mengevaluasi sistem Rekomendasi collaborative filtering bisa menggunakan matrik evaluasi Root Mean Square Error (RMSE).

## Referensi

[1]  R. Oktoria, W. Maharani, and Y. Firdaus, “Content Based Recommender System Menggunakan Algoritma Apriori,” _Konf. Nas. Sist. dan Inform._, pp. 124–129, 2010.

[2]  R. T. Wahyuni, D. Prastiyanto, and E. Supraptono, “Penerapan Algoritma Cosine Similarity dan Pembobotan TF-IDF pada Sistem Klasifikasi Dokumen Skripsi,” _J. Tek. Elektro_, vol. 9, no. 1, pp. 18–23, 2017.

[3]  Y. Yunitasari, “Penerapan Metode Eucliean Distance Untuk Ekstraksi Ciri Dokumen dan Kemiripan Dokumen,” _DoubleClick J. Comput. Inf. Technol._, vol. 3, no. 1, pp. 1–5, 2019.

[4]  P. Wicaksono, “Analisis Sistem Rekomendasi Collaborative Filtering Pada Data Ternormalisasi.” Universitas Gadjah Mada, 2015.
