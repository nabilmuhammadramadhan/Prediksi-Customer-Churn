# **Proyek UAS Kecerdasan Buatan: Prediksi Customer Churn**

Repositori ini berisi pengerjaan Ujian Akhir Semester (UAS) mata kuliah Kecerdasan Buatan. Proyek ini berfokus pada penyelesaian masalah klasifikasi menggunakan algoritma *Machine Learning* untuk mendeteksi pelanggan telekomunikasi yang berpotensi untuk berhenti berlangganan (*churn*).

## **Struktur Direktori**

* Laporan\_uas.md: Berisi laporan proyek komprehensif dari *Business Understanding* hingga Evaluasi.  
* uas\_model.ipynb: Kode Jupyter Notebook (*Machine Learning Pipeline*).  
* data/dataset/: Direktori penyimpanan data (program menggunakan simulasi *mock data* jika dataset asli tidak terdeteksi).  
* data/Jurnal/: Kumpulan referensi jurnal ilmiah terkait *Customer Churn*.

## **Penjelasan Langkah Pengerjaan**

1. **Business & Data Understanding:** Merumuskan permasalahan tingginya kerugian akibat *customer churn* dan menganalisis karakteristik dataset telco.  
2. **Exploratory Data Analysis (EDA):** Mengeksekusi visualisasi data untuk melihat rasio distribusi antara retained vs churn, korelasi fitur melalui *heatmap*, dan mengonfirmasi keberadaan *imbalanced classes*.  
3. **Data Preparation:** Menangani 5 *missing value* dengan imputasi median, melakukan LabelEncoding pada fitur kategorik, dan penskalaan StandardScaler pada numerik, diakhiri dengan pemisahan *train/test* (80/20).  
4. **Modeling:** Mengimplementasikan dua buah algoritma: *Decision Tree* yang divisualisasikan dalam bentuk pohon, dan algoritma *K-Nearest Neighbors (KNN)*.  
5. **Evaluation:** Melakukan komparasi performa model yang membuahkan *Decision Tree* sebagai pemenang pada metrik Akurasi (71%). Ditemukan kelemahan pada metrik *Recall* karena karakteristik acak pada *mock data* dan ketidakseimbangan target.