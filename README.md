## **Project Overview**

Permasalahan utama dalam e-commerce adalah membantu pengguna menemukan produk yang sesuai dengan preferensi mereka di antara ribuan pilihan. Untuk itu, sistem rekomendasi menjadi solusi penting dalam meningkatkan pengalaman pengguna dan mendorong penjualan.

Proyek ini bertujuan membangun sistem rekomendasi makanan menggunakan dataset **Amazon Fine Food Reviews**. Dataset ini memuat lebih dari 500 ribu ulasan pelanggan, termasuk skor, komentar, dan informasi pengguna serta produk. Sistem rekomendasi ini akan membantu pengguna mendapatkan rekomendasi produk berdasarkan preferensi pribadi dan ulasan pengguna lain.

Dalam proyek ini, dua metode rekomendasi utama, yaitu **Content-Based Filtering** dan **Collaborative Filtering**, digunakan untuk memberikan rekomendasi yang relevan dan personal. Dengan pendekatan ini, diharapkan sistem mampu meningkatkan kepuasan pengguna serta membantu mereka dalam pengambilan keputusan pembelian.

Pentingnya proyek ini didasari oleh tingginya volume informasi dalam platform e-commerce, yang menyebabkan user fatigue dan kesulitan dalam mengambil keputusan pembelian (Kotler et al., 2021). Dengan sistem rekomendasi yang efektif, pengalaman pengguna bisa ditingkatkan secara signifikan.

Referensi:

* [Amazon Fine Food Reviews - Kaggle](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews)
* Kotler, P., Keller, K. L., et al. (2021). *Marketing Management*.

## **Business Understanding**

### Problem Statement

Pengguna e-commerce sering mengalami kesulitan dalam menemukan produk makanan yang sesuai dengan preferensi mereka karena banyaknya pilihan dan variasi produk. Hal ini dapat menyebabkan ketidakpuasan pelanggan dan menurunnya penjualan.

### Goals

* Membangun sistem rekomendasi yang mampu memberikan rekomendasi produk makanan sesuai preferensi pengguna.
* Mengurangi beban pengguna dalam memilih produk dengan menampilkan rekomendasi yang relevan dan personal.
* Meningkatkan kepuasan pelanggan dan potensi peningkatan penjualan di platform e-commerce.

### Solution Approach

Untuk mencapai tujuan tersebut, dua pendekatan sistem rekomendasi akan digunakan:

1. **Content-Based Filtering (CBF):** Menggunakan fitur teks ulasan untuk merekomendasikan produk berdasarkan kemiripan konten dengan produk yang sudah disukai pengguna.
2. **Collaborative Filtering (CF):** Memanfaatkan interaksi pengguna (rating) untuk memberikan rekomendasi berdasarkan preferensi pengguna lain yang serupa.

Pendekatan ini dipilih agar sistem rekomendasi dapat menangani berbagai kondisi, misalnya produk baru (CBF) dan pola preferensi pengguna yang kompleks (CF).

Paham banget! Saya susun ulang **Data Understanding** ini dengan format narasi laporan yang rapi dan terstruktur sesuai ketentuan rubrik kamu, sekaligus tetap sesuai dengan pengerjaan di Colab kamu. Jadi kamu tinggal copy-paste dan tinggal sesuaikan minor jika perlu.

## Data Understanding

Dataset yang digunakan dalam proyek ini adalah **Amazon Fine Food Reviews** yang diperoleh dari Kaggle ([link dataset](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews)). Dataset ini berisi **568.454** baris dan **10** kolom yang mencakup informasi lengkap mengenai ulasan produk makanan di Amazon.

### Deskripsi Data

Setiap baris pada dataset merepresentasikan sebuah ulasan yang mencakup fitur-fitur seperti:

* **UserId** dan **ProductId** sebagai identitas unik pengguna dan produk, dengan total 256.059 pengguna dan 74.258 produk yang berbeda.
* **ProfileName** dan **Summary** yang berisi nama pengguna dan ringkasan ulasan dalam bentuk teks, meskipun terdapat sedikit nilai yang hilang (masing-masing 26 dan 27 missing values).
* **HelpfulnessNumerator** dan **HelpfulnessDenominator** yang menunjukkan jumlah vote pengguna lain terkait seberapa membantu ulasan tersebut.
* **Score** adalah rating ulasan dengan skala 1 hingga 5, yang menunjukkan tingkat kepuasan pengguna.
* **Text** berisi isi lengkap dari ulasan dalam bentuk teks.
* **Time** merepresentasikan waktu ulasan dalam format UNIX timestamp, yang diubah menjadi tanggal agar dapat dianalisis tren waktunya.

### Insight dari Data

* **Distribusi Skor**: Rata-rata skor ulasan adalah 4.18 dengan mayoritas ulasan memberikan nilai tinggi (4 dan 5), menunjukkan ulasan positif mendominasi. Namun, distribusi ini bersifat tidak seimbang (skewed), sehingga perlu diwaspadai agar model tidak bias terhadap kelas mayoritas.
* **Panjang Teks Ulasan** sangat bervariasi, dengan rata-rata sekitar 436 karakter dan adanya beberapa ulasan sangat panjang (hingga lebih dari 21 ribu karakter), yang perlu diperhatikan dalam tahap pemrosesan teks.
* **Helpfulness**: Terdapat korelasi sangat tinggi (0.97) antara kolom numerator dan denominator helpfulness, yang menunjukkan kedua fitur ini sangat berkaitan dan dapat mempengaruhi pemodelan jika digunakan bersamaan.
* **Waktu Ulasan** tersebar dari tahun 1999 sampai 2012, memungkinkan analisis tren perubahan ulasan selama waktu yang cukup panjang.
* **Missing Values** pada kolom `ProfileName` dan `Summary` sangat sedikit (26-27 baris) sehingga tidak signifikan dan mudah ditangani dalam proses pembersihan data.
* **Data Duplikat**: Tidak ditemukan data duplikat dalam dataset, menandakan data sudah bersih dan siap untuk tahap analisis dan modeling.

### Kesimpulan

Dataset ini cukup besar dan lengkap, dengan berbagai tipe data numerik dan teks yang memungkinkan penerapan berbagai teknik analisis, seperti content-based filtering menggunakan fitur teks, serta collaborative filtering berdasarkan interaksi pengguna-produk. Kondisi data yang bersih dan beragam juga mendukung pengembangan sistem rekomendasi yang akurat dan relevan.

## Data Understanding

### 1. Informasi Dataset

Dataset **Amazon Fine Food Reviews** berisi **568.454 baris** dan **10 kolom** yang merepresentasikan ulasan produk makanan di Amazon. Data ini sangat kaya dengan informasi seperti ID produk, ID pengguna, nama profil, skor ulasan, waktu ulasan, dan isi ulasan.

Dataset dapat diunduh di:
[https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews)

### 2. Variabel/Fitur Dataset

| Kolom                  | Tipe Data | Deskripsi                                       |
| ---------------------- | --------- | ----------------------------------------------- |
| Id                     | int64     | ID unik untuk setiap ulasan                     |
| ProductId              | object    | ID produk                                       |
| UserId                 | object    | ID pengguna                                     |
| ProfileName            | object    | Nama profil pengguna (terdapat sedikit missing) |
| HelpfulnessNumerator   | int64     | Jumlah vote helpful untuk ulasan                |
| HelpfulnessDenominator | int64     | Jumlah total vote untuk ulasan                  |
| Score                  | int64     | Skor ulasan (1 sampai 5)                        |
| Time                   | int64     | Waktu ulasan dalam UNIX timestamp               |
| Summary                | object    | Ringkasan ulasan (sedikit missing)              |
| Text                   | object    | Isi teks ulasan                                 |

### 3. Statistik Deskriptif dan Kondisi Data

* Dataset bersih, tanpa duplikat.
* Sedikit missing values pada kolom `ProfileName` (26 baris) dan `Summary` (27 baris) yang dapat diatasi dengan pengisian nilai default atau dihapus.
* Skor ulasan didominasi nilai 5 (median = 5.0), menunjukkan mayoritas ulasan positif.
* Variasi panjang teks ulasan besar, dari sangat pendek hingga lebih dari 21.000 karakter.
* Waktu ulasan mencakup rentang dari tahun 2000 hingga 2012, memungkinkan analisis tren.


### 4. Visualisasi dan Insight

#### Distribusi Skor Ulasan
![image](https://github.com/user-attachments/assets/7c24eebc-5b32-4ab1-81aa-9b793ddd11aa)

**Insight:**
Distribusi skor ulasan sangat tidak seimbang, dengan dominasi skor 5 yang sangat besar. Hal ini menunjukkan ulasan mayoritas positif, sehingga perlu diperhatikan imbalance ini dalam modeling.


#### Boxplot Panjang Teks Ulasan

![image](https://github.com/user-attachments/assets/20e585da-3758-4d27-8137-68a50fc20696)

**Insight:**
Sebagian besar ulasan memiliki panjang teks sedang, namun ada beberapa ulasan dengan teks sangat panjang yang dapat mempengaruhi proses pemrosesan teks dan harus dipertimbangkan dalam tahap cleaning atau preprocessing.

#### Heatmap Korelasi Variabel Numerik

![image](https://github.com/user-attachments/assets/5baf1e1d-c148-46cf-88c0-6da7da9dfce7)

**Insight:**
Terdapat korelasi sangat tinggi antara `HelpfulnessNumerator` dan `HelpfulnessDenominator` (0.97), menandakan keduanya berkaitan erat dan berpotensi menyebabkan multikolinearitas dalam model. Skor ulasan tidak menunjukkan korelasi kuat dengan panjang teks ulasan.


### 5. Exploratory Data Analysis (EDA) Ringkas

* Terdapat **256.059 UserId unik** dan **74.258 ProductId unik**, menunjukkan data sangat beragam.
* Rentang waktu ulasan cukup panjang, dari Oktober 1999 hingga Oktober 2012, memungkinkan analisis tren waktu.
* Mayoritas produk mendapat skor review 5, dengan skewness positif pada distribusi skor.




