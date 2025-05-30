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

