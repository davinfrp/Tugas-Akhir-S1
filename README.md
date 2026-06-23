# Analisis Efektivitas Teknik Resampling dalam Penanganan Imbalanced Data untuk Meningkatkan Sensitivitas Model Ensemble Learning pada Dataset Penipuan Transaksi Kartu Kredit

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Ensemble%20Learning-green)
![Status](https://img.shields.io/badge/Status-Final%20Project-success)
![License](https://img.shields.io/badge/License-Academic-orange)

## 📖 Deskripsi

Repositori ini berisi implementasi dan eksperimen yang dilakukan dalam Tugas Akhir Sarjana Teknik Informatika Institut Teknologi Sepuluh Nopember (ITS) yang berjudul:

> **Analisis Efektivitas Teknik Resampling dalam Penanganan Imbalanced Data untuk Meningkatkan Sensitivitas Model Ensemble Learning pada Dataset Penipuan dalam Transaksi Kartu Kredit**

Penelitian ini berfokus pada permasalahan **imbalanced data** pada kasus **Credit Card Fraud Detection**, di mana jumlah transaksi fraud hanya sebesar **0,172%** dari seluruh transaksi. Ketidakseimbangan tersebut menyebabkan model machine learning cenderung mempelajari pola kelas mayoritas (non-fraud) dan mengabaikan karakteristik kelas minoritas (fraud).

Untuk mengatasi permasalahan tersebut, penelitian ini membandingkan berbagai teknik **resampling** yang dikombinasikan dengan beberapa metode **Ensemble Learning** guna meningkatkan kemampuan model dalam mendeteksi transaksi fraud. Fokus utama penelitian adalah meningkatkan **Recall (Sensitivity)** tanpa mengorbankan Precision dan F1-Score secara signifikan.

---

## 🎯 Tujuan Penelitian

Penelitian ini bertujuan untuk:

1. Menganalisis pengaruh teknik resampling terhadap performa model Ensemble Learning pada kasus fraud detection.
2. Mengevaluasi efektivitas berbagai teknik oversampling, undersampling, dan hybrid sampling dalam menangani ketidakseimbangan data.
3. Mengidentifikasi kombinasi model dan teknik resampling yang menghasilkan performa terbaik.
4. Menganalisis pengaruh hyperparameter tuning terhadap performa model dibandingkan parameter default.

---

## 📊 Dataset

### Credit Card Fraud Detection Dataset

- **Sumber**: Machine Learning Group, Université Libre de Bruxelles (ULB)
- **Jumlah transaksi**: 284.807
- **Jumlah transaksi fraud**: 492
- **Persentase fraud**: 0,172%
- **Jenis klasifikasi**: Binary Classification

| Label | Keterangan |
|---------|---------|
| 0 | Non-Fraud |
| 1 | Fraud |

Dataset ini telah melalui proses transformasi PCA sehingga sebagian besar fitur telah dianonimkan menjadi atribut V1 hingga V28.

---

## 🔄 Teknik Resampling yang Digunakan

### Oversampling

- Random Oversampling
- SMOTE (Synthetic Minority Oversampling Technique)
- ADASYN (Adaptive Synthetic Sampling)

### Undersampling

- Random Undersampling
- Tomek Links
- Edited Nearest Neighbor (ENN)

### Hybrid Sampling

- SMOTE-Tomek
- SMOTE-ENN

Total teknik resampling yang dievaluasi adalah **8 teknik resampling**.

---

## 🤖 Model Ensemble Learning

Penelitian ini mengevaluasi lima model Ensemble Learning yang mewakili berbagai pendekatan ensemble.

### Bagging

- Random Forest

### Boosting

- Gradient Boosting
- XGBoost

### Heterogeneous Ensemble

#### Soft Voting

Penyusun model:

- Logistic Regression
- Decision Tree
- Support Vector Machine (SVM)

### Stacking

#### Base Learner

- Random Forest
- XGBoost
- Gradient Boosting

#### Meta Learner

- Logistic Regression

---

## ⚙️ Metodologi Penelitian

```text
1. Data Collection
2. Data Preprocessing
3. Data Splitting
4. Feature Scaling
5. Resampling
6. Model Training
7. Model Evaluation
8. Hyperparameter Tuning
9. Final Evaluation
10. Result Analysis
```

### Data Preprocessing

Tahapan preprocessing meliputi:

- Pemeriksaan data
- Data splitting menggunakan Stratified Split
- Feature Scaling menggunakan StandardScaler
- Persiapan dataset untuk proses resampling

### Skenario Pengujian

#### 1. Baseline

Model dilatih menggunakan data asli tanpa teknik resampling.

#### 2. Resampling

Model dilatih menggunakan delapan teknik resampling yang berbeda.

#### 3. Hyperparameter Tuning

Lima kombinasi terbaik berdasarkan nilai F1-Score dilakukan optimasi menggunakan RandomizedSearchCV.

---

## 📏 Metrik Evaluasi

Evaluasi model dilakukan menggunakan:

- Accuracy
- Precision
- Recall
- F1-Score
- Confusion Matrix

Karena penelitian berfokus pada fraud detection, **Recall digunakan sebagai metrik utama** karena kesalahan berupa fraud yang tidak terdeteksi (False Negative) memiliki dampak yang lebih besar dibandingkan False Positive.

---

## 🔍 Hyperparameter Tuning

Metode tuning yang digunakan:

- RandomizedSearchCV
- Cross Validation

Tuning dilakukan pada lima kombinasi terbaik berdasarkan nilai F1-Score hasil evaluasi awal.

### Kombinasi yang Dituning

1. Baseline – Random Forest
2. Tomek Links – Random Forest
3. Random Oversampling – Random Forest
4. ENN – XGBoost
5. ENN – Stacking

---

## 🏆 Hasil Penelitian

### Teknik Resampling Terbaik

| Teknik Resampling | Hasil |
|------------------|--------|
| ENN | Rata-rata F1-Score tertinggi (0,8314) |
| Random Undersampling | Recall tertinggi (0,8980) |

Temuan penelitian menunjukkan bahwa teknik pembersihan data seperti **Edited Nearest Neighbor (ENN)** lebih efektif dibandingkan teknik yang secara agresif menyeimbangkan distribusi kelas.

### Kombinasi Terbaik

Jika mempertimbangkan kebutuhan fraud detection yang mengutamakan recall tinggi dengan precision tetap baik, kombinasi terbaik adalah:

| Model | Resampling | Recall | Precision | F1-Score |
|---------|---------|---------|---------|---------|
| XGBoost | ENN | 0,8367 | 0,9111 | 0,8723 |

Kombinasi **XGBoost + ENN** mampu mendeteksi lebih banyak transaksi fraud tanpa menghasilkan peningkatan False Positive yang signifikan.

---

## 📈 Confusion Matrix Kombinasi Terbaik

### XGBoost + ENN

| Kategori | Jumlah |
|-----------|-----------|
| True Positive (TP) | 82 |
| True Negative (TN) | 56.856 |
| False Positive (FP) | 8 |
| False Negative (FN) | 16 |

### Interpretasi

- Model berhasil mendeteksi **82 dari 98 transaksi fraud**.
- Recall mencapai **83,67%**.
- Precision mencapai **91,11%**.
- False Positive sangat rendah sehingga transaksi normal jarang salah diklasifikasikan sebagai fraud.

---

## 🛠️ Teknologi yang Digunakan

### Bahasa Pemrograman

- Python 3.10+

### Library

- NumPy
- Pandas
- Scikit-Learn
- Imbalanced-Learn
- XGBoost
- Matplotlib
- Seaborn
- Plotly
- Jupyter Notebook

---

## 🚀 Cara Menjalankan Proyek

### 1. Clone Repository

```bash
git clone https://github.com/username/repository-name.git
cd repository-name
```

### 2. Install Dependency

```bash
pip install -r requirements.txt
```

### 3. Jalankan Jupyter Notebook

```bash
jupyter notebook
```

---

## 📚 Kontribusi Akademik

Penelitian ini memberikan kontribusi dalam:

- Analisis komprehensif berbagai teknik resampling pada dataset fraud yang sangat tidak seimbang.
- Perbandingan beberapa pendekatan Ensemble Learning (Bagging, Boosting, Voting, dan Stacking).
- Evaluasi pengaruh hyperparameter tuning pada model fraud detection.
- Rekomendasi kombinasi model dan teknik resampling yang efektif untuk sistem deteksi fraud.

---

## 👨‍🎓 Penulis

**Davin Fisabilillah Reynard Putra**  
NRP 5025221137

Departemen Teknik Informatika  
Fakultas Teknologi Elektro dan Informatika Cerdas (FTEIC)  
Institut Teknologi Sepuluh Nopember (ITS)

### Dosen Pembimbing

- Prof. Dr. Eng. Chastine Fatichah, S.Kom., M.Kom.
- Ilham Gurat Adillion, S.Kom., M.Eng.

---

