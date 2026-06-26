# Project Machine Learning - Group B

## Analisis Klasifikasi untuk Deteksi Hantavirus Menggunakan Metode Machine Learning

Repository ini berisi project akhir mata kuliah Machine Learning, Program Studi S1 Statistika, Universitas Jenderal Soedirman. Project ini membangun dan mengevaluasi model klasifikasi machine learning untuk mendeteksi infeksi Hantavirus berdasarkan parameter klinis dan laboratorium pasien.

---

## Tim Penyusun

| Nama | NIM |
|---|---|
| Ramy Farras Irsyady | K1D024045 |
| Yufi Safangat | K1D024048 |
| Al Fath Miftahurizki | K1D024051 |
| Nur Aliyah Zizi Hamidah | K1D024053 |
| Afifah Thara Arendra | K1D024067 |

Dosen Pengampu: Luthfia Maharani, S.Stat., M.Stat.

---

## Latar Belakang

Hantavirus merupakan virus yang ditularkan melalui hewan pengerat dan dapat menyebabkan dua sindrom klinis serius, yaitu Hemorrhagic Fever with Renal Syndrome (HFRS) dan Hantavirus Pulmonary Syndrome (HPS), dengan tingkat kematian HPS yang dapat mencapai 30-40%. Gejala awal yang tidak spesifik membuat deteksi dini menjadi tantangan medis. Project ini bertujuan membangun sistem deteksi berbasis data menggunakan machine learning untuk membantu skrining dan diagnosis dini infeksi Hantavirus.

## Tujuan

1. Menganalisis karakteristik dan distribusi data rekam medis pasien.
2. Mengidentifikasi fitur klinis dan laboratorium yang paling berpengaruh terhadap status infeksi Hantavirus.
3. Membandingkan performa beberapa algoritma machine learning (Decision Tree, KNN, XGBoost).
4. Mengevaluasi pengaruh seleksi fitur dan hyperparameter tuning terhadap performa model.

---

## Dataset

- Nama: Hantavirus Detection Dataset
- Sumber: https://www.kaggle.com/datasets/tousifahamedrahat12/hantavirus-detection-dataset
- Jumlah Data: 10.000 observasi
- Jumlah Fitur: 8 variabel independen (numerik) + 1 variabel target (biner)

| Variabel | Deskripsi |
|---|---|
| Age | Usia pasien (tahun) |
| WBC_Count_K/uL | Jumlah sel darah putih |
| Platelet_Count_K/uL | Jumlah trombosit |
| CRP_mg/L | Kadar C-Reactive Protein |
| ALT_U/L | Kadar enzim ALT |
| AST_U/L | Kadar enzim AST |
| BUN_mg/dL | Blood Urea Nitrogen |
| Creatinine_mg/dL | Kadar kreatinin |
| Hantavirus_Positive | Target (0 = negatif, 1 = positif) |

Distribusi kelas target bersifat tidak seimbang (imbalanced): sekitar 74,3% negatif vs 25,7% positif.

---

## Metodologi

### 1. Exploratory Data Analysis (EDA)
- Statistik deskriptif, histogram, boxplot (deteksi outlier), scatter plot, dan heatmap korelasi.
- Tidak ditemukan missing value maupun data duplikat.
- CRP_mg/L memiliki korelasi tertinggi terhadap target (r = 0,86), diikuti ALT, AST, Creatinine, dan BUN.

### 2. Preprocessing
- Standarisasi fitur menggunakan StandardScaler.
- Seleksi fitur menggunakan XGBoost Feature Importance, menghasilkan 5 fitur terbaik: CRP_mg/L, Creatinine_mg/dL, ALT_U/L, AST_U/L, BUN_mg/dL.
- Pembagian data latih dan uji dengan rasio 80:20 (stratified split).

### 3. Pemodelan
Tiga algoritma klasifikasi dibangun dan dibandingkan:
- Decision Tree Classifier
- K-Nearest Neighbors (KNN), k=5
- XGBoost Classifier

### 4. Hyperparameter Tuning
Dilakukan pada model XGBoost menggunakan GridSearchCV (3-fold cross-validation), dengan metrik optimasi Recall kelas 1 karena pentingnya meminimalkan false negative dalam konteks medis.

Parameter yang dituning:
- n_estimators: 100, 200, 300
- learning_rate: 0.01, 0.1, 0.2
- max_depth: 3, 5, 7
- colsample_bytree: 0.7, 0.8, 1.0
- gamma: 0, 0.1, 0.2

### 5. Eksperimen Reduksi Fitur
Menguji performa model dengan 3 fitur terbaik (CRP, Creatinine, ALT) dan 2 fitur terbaik (CRP, Creatinine) untuk menilai efisiensi vs performa.

---

## Hasil Utama

- XGBoost (Tuned) menjadi model terbaik dengan performa tertinggi di seluruh metrik evaluasi (Accuracy, Precision, Recall, F1-Score) dibandingkan Decision Tree dan KNN.
- Hyperparameter tuning meningkatkan performa secara signifikan, terutama pada Recall kelas 1.
- Reduksi fitur menjadi 3 fitur (CRP, Creatinine, ALT/AST) masih memberikan performa yang mendekati model 5 fitur, namun reduksi ke 2 fitur menurunkan kemampuan deteksi (Recall) secara lebih nyata.
- Fitur dengan kontribusi tertinggi: CRP_mg/L (90,56%), diikuti Creatinine_mg/dL, ALT_U/L, AST_U/L, dan BUN_mg/dL, sejalan dengan dasar klinis infeksi Hantavirus yang menyebabkan inflamasi sistemik dan kerusakan ginjal/hati.

---

## Struktur Repository

```
Project_Machine_Learning_Group_B/
├── Hantavirus Detection Dataset/   # Dataset yang digunakan
├── PPT GROUP B ML (1).pdf          # Slide presentasi project
├── Project_ML.ipynb                # Notebook analisis dan pemodelan
├── Project_ML_no ai.ipynb          # Notebook versi manual (tanpa bantuan AI)
└── README.md
```

---

## Cara Menjalankan

1. Clone repository ini:
   ```
   git clone https://github.com/Fatt-dev/Project_Machine_Learning_Group_B.git
   ```
2. Pastikan library berikut sudah terinstal:
   ```
   pip install pandas numpy scikit-learn xgboost matplotlib seaborn
   ```
3. Jalankan notebook Project_ML.ipynb menggunakan Jupyter Notebook atau Google Colab.

---

## Saran Pengembangan

- Validasi model menggunakan data rekam medis nyata.
- Eksplorasi algoritma lanjutan (Random Forest, LightGBM, deep learning tabular).
- Penanganan class imbalance lebih lanjut (SMOTE, ADASYN, class weighting).
- Penambahan interpretabilitas model menggunakan SHAP atau LIME.
- Pengembangan antarmuka aplikasi web/mobile untuk implementasi praktis.

---

## Lisensi

Project ini dibuat untuk keperluan akademik sebagai bagian dari tugas mata kuliah Machine Learning, Program Studi S1 Statistika, Universitas Jenderal Soedirman.
