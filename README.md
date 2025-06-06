# 📊 Laporan Proyek Rekomendasi Cellphone

## Project Overview

### Latar Belakang

Sistem rekomendasi telah berkembang menjadi alat penting di berbagai industri, termasuk e-commerce, di mana mereka membantu pengguna menemukan produk yang sesuai dengan preferensi pribadi mereka. Dalam konteks ponsel, banyaknya pilihan model dengan spesifikasi yang beragam sering kali membuat pengguna kesulitan dalam membuat keputusan. Oleh karena itu, sistem rekomendasi yang efektif dapat mempermudah proses pemilihan ponsel yang tepat dengan mempertimbangkan kebutuhan dan preferensi individu. Sistem rekomendasi ini umumnya menggunakan teknik seperti collaborative filtering, yang memanfaatkan data interaksi pengguna lain, dan content-based filtering, yang berbasis pada deskripsi produk itu sendiri.

Namun, tantangan utama dalam pengembangan sistem rekomendasi adalah mengatasi masalah kekosongan data, di mana tidak semua pengguna memberikan rating untuk setiap item, serta menangani keanekaragaman kebutuhan pengguna yang berbeda. Kombinasi kedua metode tersebut dalam pendekatan hybrid dapat meningkatkan akurasi dan relevansi rekomendasi.[1] Proyek ini bertujuan untuk membangun sistem rekomendasi ponsel yang dapat memberikan saran yang lebih personal dan relevan, mengatasi masalah data yang tidak lengkap dan menghasilkan rekomendasi yang lebih sesuai dengan preferensi pengguna.

**Pentingnya Proyek** 🤔

Proyek ini memiliki peranan penting karena:
1. Peningkatan Pengalaman Pengguna: Mempermudah pengguna dalam menemukan ponsel yang sesuai dengan preferensi mereka, sehingga meningkatkan kepuasan dan kualitas pengalaman pengguna.
2. Efisiensi: Menghemat waktu dan usaha pengguna dalam proses pencarian serta perbandingan berbagai model ponsel.
3. Personalisasi: Menyediakan rekomendasi yang disesuaikan dengan preferensi individu berdasarkan data penilaian pengguna.

## Business Understanding

### Problem Statements
- Bagaimana kita dapat membantu pengguna menemukan ponsel yang paling cocok dengan kebutuhan dan preferensi mereka?
- Bagaimana kita dapat membantu pengguna menemukan ponsel yang serupa dengan ponsel lama mereka, meskipun mereka tidak memahami spesifikasi teknis ponsel tersebut?

### Tujuan 
- Membangun sistem rekomendasi yang dapat menyajikan daftar ponsel terbaik sesuai dengan preferensi pengguna
- Mengembangkan sistem rekomendasi yang dapat memberikan daftar ponsel terbaik berdasarkan model ponsel lama pengguna (misalnya: iPhone 13).

### Solution statements 💡
- **Content-Based Filtering**: Mengandalkan fitur deskriptif ponsel (seperti merek, model, dan sistem operasi) untuk memberikan rekomendasi yang relevan.
- **Collaborative Filtering**: Memanfaatkan data rating dari pengguna untuk memberikan rekomendasi berdasarkan kesamaan preferensi dengan pengguna lain.

## 📂 Data Understanding 
Dataset yang digunakan mencakup informasi tentang berbagai model ponsel, seperti merek, model, sistem operasi, serta beberapa fitur lainnya. Dataset ini berasal dari [kaggle](https://www.kaggle.com/datasets/meirnizri/cellphones-recommendations/data).
    - Dataset terbagi menjadi 3 yaitu `cellphones data`, `cellphones rating`, dan `cellphones users`.
    
    
Data `cellphones data` terdiri dari 33 baris dan 14 kolom tanpa adanya nilai yang hilang. Dataset ini memuat spesifikasi rinci dari setiap cellphones berikut adalah informasi:

|   Column           |  Dtype   |
|--------------------|----------|
| cellphone_id       | int64    |
| brand              | object   |
| model              | object   |
| operating system   | object   |
| internal memory    | int64    |
| RAM                | int64    |
| performance        | float64  |
| main camera        | int64    |
| selfie camera      | int64    |
| battery size       | int64    |
| screen size        | float64  |
| weight             | int64    |
| price              | int64    |
| release date       | object   |

Berikut adalah contoh data dari dataset cellphone:

| cellphone_id | brand   | model             | operating system | internal memory | RAM | performance | main camera | selfie camera | battery size | screen size | weight | price | release date |
|--------------|---------|-------------------|------------------|-----------------|-----|-------------|-------------|---------------|--------------|-------------|--------|-------|--------------|
| 0            | Apple   | iPhone SE (2022)   | iOS              | 128             | 4   | 7.23        | 12          | 7             | 2018         | 4.7         | 144    | 429   | 18/03/2022   |
| 1            | Apple   | iPhone 13 Mini     | iOS              | 128             | 4   | 7.72        | 12          | 12            | 2438         | 5.4         | 141    | 699   | 24/09/2021   |


*****************************************************************
Cellphones rating terdiri dari 990 baris dan 3 kolom tanpa adanya missing value. Dataset ini berisi nilai rating yang diberikan oleh pengguna X untuk ponsel Y, berikut adalah informasi dari cellphones rating:

|   Column           |  Dtype   |
|--------------------|----------|
| user_id            | int64    |
| cellphone_id       | int64    |
| rating             | int64    |

Berikut adalah contoh data dari cellphones rating:

|index|user_id|cellphone_id|rating|
|---|---|---|---|
|0|0|30|1|
|1|0|5|3|

*****************************************************************

Cellphones users terdiri dari 99 baris dan 4 kolom dengan 1 missing value pada kolom occupation. Dataset ini berisi informasi tentang pengguna, berikut adalah informasi data dari cellphones users:

|   Column           |  Dtype   |
|--------------------|----------|
| user_id            | int64    |
| age                | int64    |
| gender             | object   |
| occupation         | object   |

Berikut adalah contoh data dari cellphones users:

|index|user\_id|age|gender|occupation|
|---|---|---|---|---|
|0|0|38|Female|Data analyst|
|1|1|40|Female|team worker in it|

#### Variabel dalam dataset
Berikut adalah variabel-variabel yang terdapat dalam dataset:
- data:
  - `cellphone_id`: Unik ID untuk setiap ponsel.
  - `brand`: Merek ponsel.
  - `model`: Model ponsel.
  - `operating system`: Sistem operasi yang digunakan oleh ponsel.
  - `internal memory`: Kapasitas memori internal ponsel dalam GB.
  - `RAM`: Kapasitas RAM ponsel dalam GB.
  - `performance`: Skor kinerja ponsel.
  - `main camera`: Resolusi kamera utama dalam MP.
  - `selfie camera`: Resolusi kamera depan dalam MP.
  - `battery size`: Kapasitas baterai ponsel dalam mAh.
  - `screen size`: Ukuran layar ponsel dalam inci.
  - `weight`: Berat ponsel dalam gram.
  - `price`: Harga ponsel dalam USD.
  - `release date`: Tanggal rilis ponsel.

- rating:
  - `user_id`: Unik ID untuk setiap pengguna.
  - `cellphone_id`: Unik ID untuk setiap ponsel (merujuk pada cellphones_data).
  - `rating`: Nilai rating yang diberikan pengguna untuk ponsel tertentu (skala 1-10).

- users:
  - `user_id`: Unik ID untuk setiap pengguna.
  - `age`: Usia pengguna.
  - `gender`: Jenis kelamin pengguna.
  - `occupation`: Pekerjaan pengguna.

### Exploratory Data Analysis (EDA) 🔍
- Distribusi Brand Ponsel
  ![Distribusi Brand](./images/outputcode.png)
  - Gambar tersebut menunjukkan distribusi jumlah ponsel berdasarkan brand dalam dataset, di mana brand `Samsung` mencatatkan jumlah terbanyak dengan 8 unit, diikuti oleh `Apple` dengan 6 unit. Sementara itu, brand `Asus`, `Oppo`, `Vivo`, dan `Sony` memiliki jumlah ponsel yang lebih sedikit.

- Distribusi Sistem Operasi Ponsel
  ![Distribusi Sistem Operasi](./images/outputcode2.png)
  - Gambar tersebut menunjukkan distribusi sistem operasi pada ponsel dalam dataset, di mana `Android` merupakan sistem operasi yang paling dominan dengan lebih dari 25 unit, sementara `iOS` tercatat memiliki sekitar 6 unit.

- Distribusi Tahun Rilis Ponsel
  ![Distribusi Tahun Rilis](./images/outputcode3.png)
  - Gambar tersebut menunjukkan distribusi ponsel berdasarkan tahun rilis, di mana tahun `2021` dan `2022` mencatatkan jumlah ponsel yang hampir sama, masing-masing lebih dari 15 unit. Sementara itu, tahun `2018` hanya memiliki jumlah ponsel yang sangat sedikit, menunjukkan bahwa dataset lebih dominan pada model-model terbaru.

- Distribusi Rating Ponsel
  ![Distribusi Tahun Rilis ](./images/outputcode4.png)
  - Gambar tersebut menunjukkan distribusi rating yang diberikan pengguna untuk ponsel dalam dataset, di mana rating `8 ` merupakan yang paling umum, diikuti oleh rating `7` dan `10`. Rating yang lebih rendah, seperti `2`, `3`, dan `4`, tercatat memiliki jumlah yang lebih sedikit. Secara keseluruhan, sebagian besar ponsel dalam dataset mendapatkan rating yang cukup tinggi, yaitu antara `7` hingga`10`.



### Teknik Data Prepocessing
- Menggabungkan seluruh dataset menjadi satu.
- Menangani Missing Values: Menghapus atau mengisi data yang hilang dalam dataset.

## Data Preparation ⚙️

### Teknik Data Preparation

#### 1. Tahap Persiapan Data Umum
- **Menggabungkan Dataset**: Menggabungkan dataset `cellphones data`, `cellphones ratings`, dan `cellphones user` menjadi satu dataframe untuk memudahkan analisis dan menghindari fragmentasi data.
- **Menangani Missing Values**: Menghapus nilai Null pada kolom `occupation` agar tidak ada data yang hilang yang dapat memengaruhi hasil analisis dan model.
- **Menghapus Outliers**: Penghapusan ini secara tidak langsung juga menghapus satu entri dengan gender = '-Select Gender-' (user ID 53), namun dua entri lain dengan nilai serupa tetap ada karena memiliki data occupation yang lengkap. Catatan: Dua pengguna lain dengan gender = -Select Gender- (user ID 105 dan 230) yang memiliki data occupation tidak terhapus dan masih ada dalam data yang diproses lebih lanjut.
- **Standardisasi Data**: Mengubah semua nilai pada kolom `occupation` menjadi huruf kecil untuk memastikan konsistensi format penulisan dan mencegah kesalahan interpretasi.
- **Perbaikan Inkonsistensi**: Memperbaiki penulisan yang salah pada kolom `occupation`, seperti mengganti nilai 'Healthare' menjadi 'healthcare' dan 'it' menjadi 'information technology'.

#### 2. Persiapan Data untuk Content-Based Filtering
- **Penghapusan Duplikasi**: Menghapus duplikasi berdasarkan `cellphone_id` untuk memastikan dataset tidak mengandung entri berulang yang dapat memengaruhi model.
- **Feature Selection**: Karena TF-IDF hanya cocok digunakan untuk data teks, maka hanya kolom dengan tipe data objek yang dipilih (`cellphone_id`, `brand`, `model`, `operating_system`).
- **TF-IDF Vectorization**: Menggunakan TF-IDF (Term Frequency-Inverse Document Frequency) untuk mengekstrak fitur dari kolom `brand` guna menghitung kemiripan antara model ponsel.
  ```python
  #dictionary untuk menentukan pasangan key-value
  data_dict = pd.DataFrame({
      'cellphone_id': cellphone_id,
      'brand': brand,
      'model': model,
      'operating_system': operating_system,
  })
  ```
- **Transformasi ke Matrix**: Melakukan fit lalu ditransformasikan ke bentuk matrix
  ```python
  #fit dan transform ke matriks
  tfidf_matrix = tf.fit_transform(data['brand']) 
  ```
  Hasilnya berupa matriks berukuran (33,10), di mana 33 merujuk pada jumlah data dan 10 adalah jumlah brand.

#### 3. Persiapan Data untuk Collaborative Filtering
- **Encoding Fitur**: Melakukan encoding pada fitur `user_id` dan `cellphone_id` untuk menyusun input yang siap digunakan dalam model Collaborative Filtering.
- **Menghapus Outliers**: Mengeliminasi outlier pada kolom `rating` yang memiliki nilai 18  untuk meningkatkan akurasi model dengan menghilangkan data yang dapat mengganggu kinerja model.
- **Pengacakan Dataset**: Melakukan pengacakan dataset (`df.sample(frac=1, random_state=42)`) untuk memastikan distribusi data yang acak sebelum pembagian.
- **Normalisasi Rating**: Melakukan normalisasi rating menjadi skala 1-10 untuk meningkatkan akurasi dalam Collaborative Filtering.
- **Pembagian Dataset**: Membagi dataset menjadi train dan test dengan proporsi 80:20 untuk memastikan bahwa model dilatih dengan data yang cukup dan diuji dengan data yang tidak terpengaruh oleh proses pelatihan.

### Proses Data Preparation
Berikut adalah urutan proses data preparation yang dilakukan:

1. **Menggabungkan dataset** `cellphones data`, `cellphones ratings`, dan `cellphones user` menjadi satu dataframe
2. **Menghapus nilai Null** pada kolom `occupation`
3. **Memperbaiki inkonsistensi penulisan** pada kolom `occupation` 
4. **Persiapan untuk Content-Based Filtering**:
   - Menghapus duplikasi data berdasarkan `cellphone_id`
   - Seleksi fitur kategorikal
   - Implementasi TF-IDF Vectorization pada kolom `brand`
   - Transformasi ke bentuk matrix
5. **Persiapan untuk Collaborative Filtering**:
   - Encoding fitur `user_id` dan `cellphone_id`
   - Menghapus outlier pada kolom `rating`
   - Pengacakan dataset dengan random state
   - Normalisasi rating ke skala 1-10
   - Pembagian dataset menjadi train dan test (80:20)
   
## Modeling

Pada tahap modeling, akan dibahas dua pendekatan utama yang digunakan dalam pembangunan sistem rekomendasi, yaitu: Content-Based Filtering dan Collaborative Filtering.

### Model Sistem Rekomendasi Content Based Filtering

Content-Based Filtering memanfaatkan deskripsi dan fitur dari item itu sendiri untuk memberikan rekomendasi berdasarkan kesamaan karakteristik produk.

**Bagaimana Algoritma Bekerja:**
Content-Based Filtering menggunakan deskripsi item itu sendiri untuk memberikan rekomendasi. Algoritma ini bekerja dengan cara menganalisis fitur-fitur deskriptif dari item (seperti brand ponsel) yang telah diproses menjadi representasi numerik. Selanjutnya, dihitung cosine similarity untuk menentukan tingkat kemiripan antara item-item berdasarkan vektor fitur mereka. Berdasarkan hasil perhitungan kemiripan ini, sistem dapat memberikan rekomendasi item yang paling mirip dengan item yang telah disukai oleh pengguna.

**Parameter yang Digunakan:**
- **Cosine Similarity**: Metrik untuk mengukur kesamaan antar item
- **Top-N Recommendation**: Menampilkan 4 rekomendasi teratas
- **Fitur Utama**: Brand sebagai basis perhitungan kesamaan

**Tahapan Pemodelan:**
1. Menghitung similarity degree antar model menggunakan metode cosine similarity
2. Membuat fungsi `model_recommendations` untuk menghasilkan rekomendasi
3. Implementasi sistem rekomendasi berdasarkan input model ponsel

**Interaksi dengan Sampel Input:**
Misalkan pengguna memiliki ponsel "Galaxy S22 Ultra" dan ingin mendapatkan rekomendasi ponsel yang serupa. Algoritma akan:
1. Mengambil representasi vektor dari "Galaxy S22 Ultra"
2. Menghitung cosine similarity antara vektor "Galaxy S22 Ultra" dan semua vektor ponsel lain dalam dataset
3. Mengembalikan daftar ponsel dengan tingkat kemiripan tertinggi terhadap "Galaxy S22 Ultra"

### Top-N Recommendation Content Based Filtering
Menampilkan hasil rekomendasi
  - model_recommendations('Galaxy S22 Ultra')

  |index|model|brand|operating\_system|
  |---|---|---|---|
  |0|Galaxy Z Flip 3 |Samsung|Android|
  |1|Galaxy S22 Plus|Samsung|Android|
  |2|Galaxy Z Fold 3|Samsung|Android|
  |3|Galaxy A32|Samsung|Android|

  - model_recommendations('iPhone XR')

  |index|model|brand|operating\_system|
  |---|---|---|---|
  |0|iPhone 13|Apple|iOS|
  |1|iPhone 13 Mini|Apple|iOS|
  |2|iPhone SE (2022)|Apple|iOS|
  |3|iPhone 13 Pro|Apple|iOS|

### Model Sistem Rekomendasi Collaborative Filtering 
Collaborative Filtering menggunakan interaksi antara pengguna dan item (rating) untuk menghasilkan rekomendasi berdasarkan pola preferensi pengguna.

**Bagaimana Algoritma Bekerja:**
Collaborative Filtering menggunakan interaksi antara pengguna dan item (seperti rating) untuk menghasilkan rekomendasi. Algoritma ini berfungsi dengan memprediksi rating untuk item yang belum diulas oleh pengguna, berdasarkan rating yang diberikan oleh pengguna lain untuk item serupa. Model ini mempelajari pola preferensi pengguna dari data rating yang ada, dan menggunakan pola tersebut untuk memberikan rekomendasi item yang kemungkinan besar akan disukai oleh pengguna.

**Arsitektur Model:**
1. **RecommenderNet Class**: Menggunakan kelas `RecommenderNet` yang mewarisi kelas `Model` Keras
2. **Embedding Layer**: Inisialisasi model dengan nilai embedding sebesar 50 untuk user dan item
3. **Neural Network**: Implementasi neural network untuk prediksi rating

**Parameter Model:**
- **Embedding Dimension**: 50
- **Loss Function**: `BinaryCrossentropy`
- **Optimizer**: `Adam` dengan learning rate 0.001
- **Metrics**: `RootMeanSquaredError`
- **Training Parameters**: 
  - batch_size = 8
  - epochs = 100

**Interaksi dengan Sampel Input:**
Misalnya, pengguna dengan ID 10 memiliki beberapa ponsel dengan rating tinggi dan ingin menerima rekomendasi. Algoritma akan:
1. Mengambil data rating dari pengguna lain yang memiliki preferensi serupa
2. Menggunakan model yang sudah dilatih untuk memprediksi rating untuk ponsel yang belum diulas oleh pengguna 10
3. Menghasilkan daftar ponsel berdasarkan prediksi rating tertinggi

### Top-N Recommendation Collaborative Filtering 
```
Showing recommendations for users: 243
===========================
cellphone with high ratings from user
--------------------------------
Vivo : X80 Pro
Samsung : Galaxy A13
OnePlus : Nord N20
Google : Pixel 6  
OnePlus : 10 Pro
--------------------------------
Top 10 cellphone recommendation
--------------------------------
Apple : iPhone XR
Samsung : Galaxy S22
Oppo : Find X5 Pro
Apple : iPhone 13 Pro
Apple : iPhone 13 Pro Max
Apple : iPhone 13 Mini
Xiaomi : 11T Pro
Apple : iPhone SE (2022)
Google : Pixel 6 Pro 
Apple : iPhone 13
```
*****************************************************************
*Untuk tahapan proses yang lebih lengkap silahkan baca [Dicoding_ModelSistemRekomendasi.ipynb](https://github.com/alishaanggranidi/recommender-system/blob/main/Recommender_System.ipynb)*
*****************************************************************

## Evaluation

Pada bagian ini, model rekomendasi yang telah dibangun akan dievaluasi menggunakan metrik evaluasi yang sesuai. Untuk model prediksi rating, kami akan menggunakan Root Mean Squared Error (RMSE) sebagai metrik evaluasi. Selain itu, evaluasi juga akan dilakukan untuk menentukan apakah proyek ini berhasil menjawab pernyataan masalah dan memberikan solusi yang diharapkan.


### Metrik Evaluasi Content-Based Filtering: Precision@k 📊

Precision@k adalah metrik yang digunakan untuk mengukur kualitas rekomendasi dalam sistem rekomendasi. Precision mengukur seberapa banyak item yang relevan dari total item yang direkomendasikan.

#### Formula Precision@k:
$$
\text{Precision@k} = \frac{\text{Jumlah item relevan pada k rekomendasi}}{k}
$$

**Penjelasan:**
- **Rekomendasi pada k**: Daftar item yang direkomendasikan oleh sistem untuk pengguna pada posisi ke-k.
- **Item relevan**: Item yang relevan atau sesuai dengan preferensi pengguna dalam kumpulan rekomendasi.
- **k**: Posisi dalam daftar rekomendasi, misalnya, k = 3 berarti melihat 3 item teratas yang direkomendasikan.

**Contoh Precision pada Hasil Rekomendasi:**

- Untuk rekomendasi Galaxy (k=3):
  - Rekomendasi: `['Galaxy Z Flip 3', 'Galaxy S22 Plus', 'Galaxy Z Fold 3']`
  - Item relevan: `{'Galaxy S22 Plus', 'Galaxy S22 Ultra', 'Galaxy S22'}` 
  - Intersection: `{'Galaxy S22 Plus'}`
  - **Precision@3**: 0.33 (1 relevan dari 3 rekomendasi)

- Untuk rekomendasi iPhone (k=4):
  - Rekomendasi: `['iPhone 13', 'iPhone 13 Mini', 'iPhone SE (2022)', 'iPhone 13 Pro']`
  - Item relevan: `{'iPhone 13', 'iPhone XR', 'iPhone 13 Pro Max', 'iPhone 13'}` 
  - Intersection: `{'iPhone 13'}`
  - **Precision@4**: 0.25 (1 relevan dari 4 rekomendasi)

**Interpretasi:**
- Precision@k memberikan gambaran seberapa efektif rekomendasi sistem dalam memilih item yang relevan untuk pengguna. Nilai yang lebih tinggi menunjukkan sistem rekomendasi yang lebih baik dalam memberikan hasil yang relevan.
- Precision yang lebih rendah seperti pada contoh iPhone XR menunjukkan bahwa meskipun model memiliki beberapa item relevan, sistem masih dapat ditingkatkan dengan memilih lebih banyak item relevan dalam daftar rekomendasi.

### Metrik Evaluasi Collaborative Filterin: Root Mean Squared Error (RMSE) 📈
Root Mean Squared Error (RMSE) dalah akar kuadrat dari rata-rata kuadrat selisih antara prediksi dan nilai sebenarnya. Metrik ini menggambarkan sejauh mana prediksi model menyimpang dari nilai yang sebenarnya dalam satuan yang sama dengan variabel yang diprediksi. RMSE sangat berguna karena memberikan penalti yang lebih besar pada kesalahan yang lebih besar.

$$
\text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}
$$

Di mana:

  - $y_i$ adalah nilai sebenarnya
  - $\hat y_i$ adalah nilai prediksi
  - $n$ adalah jumlah observasi

- RMSE kecil menunjukkan performa model yang baik karena kesalahan prediksi rendah.
- RMSE besar menunjukkan performa model yang buruk karena kesalahan prediksi tinggi.

## Hasil 
![Grafik train vs test](./images/outputcode5.png)

Berdasarkan gambar tersebut RMSE yang dihitung menunjukkan bahwa model prediksi rating memiliki tingkat kesalahan yang dapat diterima, sehingga cukup memadai untuk tujuan rekomendasi.

### Evaluasi Terhadap Business Understanding
- **Menjawab Problem Statement**: Model yang dikembangkan berhasil menjawab problem statement dengan memberikan rekomendasi ponsel berdasarkan model yang ada dan memprediksi rating ponsel yang belum diulas oleh pengguna. Pendekatan content-based filtering memanfaatkan data deskriptif seperti model, brand, dan operating system untuk memberikan rekomendasi ponsel yang relevan, sementara collaborative filtering menggunakan interaksi pengguna-item (rating) untuk menemukan pola preferensi pengguna.

- **Mencapai tujuan** : Model content-based filtering menggunakan cosine similarity dan collaborative filtering dengan RecommenderNet berhasil mencapai tujuan untuk memberikan rekomendasi yang relevan. Content-based filtering membuat profil item berdasarkan kesamaan fitur, meningkatkan akurasi rekomendasi, sedangkan collaborative filtering memanfaatkan data rating pengguna untuk memahami preferensi dan memberikan rekomendasi yang sesuai.

- **Pengaruh**: Dengan menggunakan kedua algoritma ini, solusi yang direncanakan memberikan dampak positif dalam meningkatkan relevansi dan akurasi rekomendasi. Content-based filtering memastikan rekomendasi yang relevan dengan mempertimbangkan kesamaan fitur, sementara collaborative filtering memungkinkan sistem memahami preferensi pengguna dari interaksi sebelumnya, menghasilkan rekomendasi yang lebih personal. Hasilnya menunjukkan bahwa pendekatan ini berhasil mencapai tujuan proyek dan memberikan rekomendasi yang sesuai dengan kebutuhan pengguna.

## Kesimpulan 👀

Kombinasi kedua pendekatan ini membangun sistem rekomendasi yang lebih kuat dan fleksibel. Content-Based Filtering cocok untuk memberikan rekomendasi berdasarkan fitur item, sementara Collaborative Filtering efektif dalam menemukan pola preferensi pengguna dari data interaksi. Memahami kelebihan dan kekurangan masing-masing pendekatan membantu memilih metode yang tepat sesuai dengan kebutuhan dan konteks sistem rekomendasi yang sedang dibangun.

## Referensi

[1] [Li, M., Wu, Q., Fu, L., Tang, Z., & Banks, D., "Recommender Systems: A Review," Journal of the American Statistical Association, vol. 119, no. 545, pp. 773-785, Nov. 2023.](https://www.researchgate.net/publication/375442432_Recommender_Systems_A_Review/link/660ab75d390c214cfd2f2864/download?_tp=eyJjb250ZXh0Ijp7ImZpcnN0UGFnZSI6InB1YmxpY2F0aW9uIiwicGFnZSI6InB1YmxpY2F0aW9uIn19) 