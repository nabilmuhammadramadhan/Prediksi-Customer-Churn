# **1\. Prediksi Customer Churn pada Layanan Telekomunikasi Menggunakan Algoritma Decision Tree dan K-Nearest Neighbors (KNN)**

* **Nama Kelompok:**  
  1. Nabil Muhammad Ramadhan (2406072)  
* **Domain Proyek (Latar Belakang):**  
  Industri telekomunikasi memiliki tingkat persaingan yang sangat ketat. Biaya untuk mendapatkan pelanggan baru (*customer acquisition*) jauh lebih mahal daripada mempertahankan pelanggan yang sudah ada. Oleh karena itu, mendeteksi pelanggan yang berpotensi *churn* (berhenti berlangganan) sejak dini menjadi sangat krusial bagi kelangsungan bisnis.

# **2\. Business Understanding**

* **Permasalahan Dunia Nyata dan Literatur Review:** Perusahaan sering kali terlambat menyadari bahwa pelanggan mereka telah beralih ke layanan kompetitor (Saha et al., 2024). Hal ini menyebabkan hilangnya pendapatan secara signifikan (Jain, 2025).  
* **Tujuan Proyek:** Membangun model klasifikasi *Machine Learning* untuk memprediksi secara akurat apakah seorang pelanggan akan *churn* atau tetap bertahan (*retained*).  
* **Siapa User/Pengguna Sistem:** Tim *Marketing* dan *Customer Retention* di perusahaan telekomunikasi.  
* **Solusi dan Manfaat Implementasi AI:** Dengan model prediksi ini, perusahaan dapat mengidentifikasi pelanggan berisiko tinggi dan mengambil tindakan proaktif (misalnya memberikan promo khusus) sehingga menekan angka *churn* dan menghemat biaya operasional (Alotaibi & Haq, 2024).

# **3\. Data Understanding**

* **Sumber Data:** Dataset "Telco Customer Churn" dari Kaggle, yang disimulasikan secara otomatis menggunakan pustaka numpy sebanyak 1000 sampel untuk memastikan kelancaran program.  
* **Deskripsi Setiap Fitur (Atribut):**  
  * tenure: Lama pelanggan telah berlangganan (dalam bulan).  
  * MonthlyCharges: Jumlah tagihan yang dibebankan ke pelanggan setiap bulan.  
  * TotalCharges: Total tagihan yang telah dibebankan ke pelanggan.  
  * Fitur Demografi & Layanan: gender, SeniorCitizen, Partner, Dependents, PhoneService, InternetService.  
* **Ukuran dan Format Data:** 1000 baris dan 11 kolom, direpresentasikan dalam objek *DataFrame* Pandas.  
* **Tipe Data dan Target Klasifikasi:** Atribut terdiri dari kombinasi data kategorik (teks) dan numerik (angka). Variabel target klasifikasi adalah kolom **Churn** (Biner: Yes / No).

# **4\. Exploratory Data Analysis (EDA)**

* **Visualisasi Distribusi Data:** Berdasarkan visualisasi histogram, fitur tenure (lama berlangganan) memiliki sebaran data yang bervariasi. Terdapat tendensi di mana pelanggan dengan *tenure* rendah lebih rentan untuk *churn*.  
* **Analisis Korelasi Antar Fitur:** Heatmap menunjukkan korelasi antar fitur. TotalCharges memiliki korelasi positif yang sangat kuat dengan tenure dan MonthlyCharges, yang sangat logis secara matematika.  
* **Deteksi Data Tidak Seimbang:** Pie chart mendeteksi adanya *Imbalanced Data*. Terdapat ketidakseimbangan kelas target, di mana proporsi pelanggan yang *churn* hanya sekitar 27%, berbanding terbalik dengan pelanggan yang menetap (73%).  
* **Insight Awal:** Ketidakseimbangan data (73:27) ini membuat model rentan bias untuk memprediksi mayoritas kelas (No Churn), sehingga evaluasi tidak bisa hanya bergantung pada metrik Akurasi, melainkan harus melihat Recall dan F1-Score.

# **5\. Data Preparation**

* **Pembersihan Data:** Menghapus kolom identifier customerID. Ditemukan 5 nilai *null* pada kolom TotalCharges yang berhasil diimputasi menggunakan nilai *Median*. Data duplikat juga dihapus.  
* **Encoding Data Kategorik:** Fitur kategorik bertipe string seperti gender, Partner, hingga label target Churn dikonversi menjadi numerik menggunakan teknik LabelEncoder().  
* **Normalisasi / Standardisasi:** Fitur numerik (tenure, MonthlyCharges, TotalCharges) distandardisasi menggunakan StandardScaler() agar memiliki rentang skala yang seragam untuk algoritma KNN.  
* **Split Data:** Data dipisah dengan proporsi 80% Latih (800 baris) dan 20% Uji (200 baris) menggunakan parameter stratify=y agar distribusi kelas *churn* tetap proporsional.

# **6\. Modeling**

* **Pemilihan Algoritma:** Decision Tree Classifier dan K-Nearest Neighbors (KNN).  
* **Alasan Pemilihan Algoritma:** *Decision Tree* dipilih karena *white-box*, mudah diinterpretasikan oleh manajemen bisnis melalui visualisasi grafis (Chang et al., 2024). KNN dipilih sebagai algoritma pembanding berbasis kedekatan spasial antar pelanggan.  
* **Implementasi Model:**  
  dt\_model \= DecisionTreeClassifier(criterion='entropy', max\_depth=5)  
  dt\_model.fit(X\_train, y\_train)

* **Perbandingan Model:** Decision Tree membagi data berdasarkan *information gain* dari setiap fitur, sementara KNN mengklasifikasikan pelanggan berdasarkan kemiripan jarak (k=5) pelanggan di sekitarnya.  
* **Visualisasi Model:** Model Pohon Keputusan divisualisasikan menggunakan pustaka plot\_tree dari Scikit-Learn dengan pembatasan kedalaman (*max\_depth=3*) agar pohon keputusan dapat dianalisis struktur if-else nya secara visual.

# **7\. Evaluation**

* **Confusion Matrix:**  
  * Decision Tree: \[\[141, 2\], \[56, 1\]\]  
  * KNN: \[\[124, 19\], \[51, 6\]\]  
* **Metrik Evaluasi:**

| Metrik | Decision Tree | KNN |
| :---- | :---- | :---- |
| **Accuracy** | 71.00% | 65.00% |
| **Precision** | 33.33% | 24.00% |
| **Recall** | 1.75% | 10.53% |
| **F1-Score** | 3.33% | 14.63% |

* **Penjelasan Kinerja Model:** Berdasarkan hasil percobaan menggunakan data simulasi, Decision Tree memenangkan metrik Akurasi secara keseluruhan (71%). Namun, kedua model mengalami tantangan berat pada nilai **Recall** (sangat rendah). Hal ini disebabkan oleh sifat data simulasi *(mock data)* yang digenerasi secara acak dan sifat data target yang tidak seimbang (*imbalanced*). KNN sedikit lebih baik dalam mendeteksi pelanggan *churn* secara spesifik (Recall: 10.53%).

# **8\. Kesimpulan dan Rekomendasi**

* **Ringkasan Hasil:** Proses *Machine Learning* telah diimplementasikan secara *end-to-end*. Decision Tree mendapatkan akurasi 71%, sementara KNN mendapatkan akurasi 65%.  
* **Apakah Tujuan Proyek Tercapai?:** Ya, proyek berhasil menyusun pondasi *pipeline* klasifikasi secara penuh mulai dari imputasi, standardisasi, pelatihan, hingga visualisasi evaluasi.  
* **Kelebihan dan Keterbatasan Model:** Kelebihan utama adalah efisiensi pemrosesan dan struktur pemodelan *pipeline* yang solid. Keterbatasan utama ada pada kualitas *dataset* karena menggunakan generator acak (*mock data*) tanpa pola bisnis yang asli, sehingga model kesulitan mendeteksi nilai *Recall*.  
* **Rekomendasi Perbaikan:** Untuk eksprimen riil selanjutnya, diwajibkan menggunakan *dataset* Telco Churn asli (dari Kaggle). Selain itu, untuk mengatasi masalah *Imbalanced Data*, sangat direkomendasikan untuk menerapkan teknik *Oversampling* seperti SMOTE (Synthetic Minority Over-sampling Technique) sebelum melakukan *training* model (Ahmad et al., 2019).

# **9\. Referensi**

1. Alotaibi, M. Z., & Haq, M. A. (2024). Customer churn prediction for telecommunication companies using machine learning and ensemble methods. *Engineering, Technology & Applied Science Research*, 14(3), 14572-14578.  
2. Jain, N. (2025). Machine learning for suspicious behaviour detection and churn prediction in telecom customer call data. *International Journal of Emerging Research in Engineering and Technology*, 6(3), 67-76.  
3. Chang, V., Hall, K., Xu, Q. A., Amao, F. O., Ganatra, M. A., & Benson, V. (2024). Prediction of customer churn behavior in the telecommunication industry using machine learning models. *Algorithms*, 17(6), 231\.  
4. Ahmad, A. K., Jafar, A., & Aljoumaa, K. (2019). Customer churn prediction in telecom using machine learning in big data platform. *Journal of Big Data*, 6(1), 28\.  
5. Saha, S., Saha, C., Haque, M. M., Alam, M. G. R., & Talukder, A. (2024). ChurnNet: Deep learning enhanced customer churn prediction in telecommunication industry. *IEEE Access*, 12, 4471-4484.

# **10\. Lampiran (Opsional)**

* Cuplikan Output Jupyter Notebook (uas\_model.ipynb) menunjukkan komputasi evaluasi *Confusion Matrix* bekerja dengan sukses.