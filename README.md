# Student Dropout Prediction

## SISTEM PERINGATAN DINI UNTUK MEMPREDIKSI RISIKO PUTUS STUDI MAHASISWA SEBAGAI UPAYA MENDUKUNG PENDIDIKAN BERMUTU 

Project ini merupakan penerapan Machine Learning untuk melakukan prediksi status akademik mahasiswa. Data yang digunakan berisi berbagai informasi mengenai mahasiswa yang kemudian dianalisis untuk memprediksi apakah mahasiswa termasuk dalam kategori **Dropout, Graduate, atau Enrolled**.

Project ini juga dikaitkan dengan **SDG 4: Quality Education**, khususnya dalam pemanfaatan teknologi dan data untuk membantu memahami kondisi akademik mahasiswa.

## Tujuan

Tujuan dari project ini adalah:

- Melakukan analisis terhadap data mahasiswa.
- Melakukan preprocessing pada data.
- Membangun model Machine Learning untuk klasifikasi status mahasiswa.
- Membandingkan hasil dari beberapa model Machine Learning.
- Mengevaluasi performa model menggunakan beberapa metrik evaluasi.

## Tahapan

Tahapan yang dilakukan dalam project ini meliputi:

1. Import library dan dataset.
2. Exploratory Data Analysis (EDA).
3. Data preprocessing.
4. Pembagian data training dan testing.
5. Pembuatan model Machine Learning.
6. Training model.
7. Prediksi data testing.
8. Evaluasi model.
9. Perbandingan hasil model.

## Model Machine Learning

Model yang digunakan dalam project ini adalah:

### 1. Logistic Regression

Logistic Regression digunakan untuk melakukan klasifikasi status mahasiswa berdasarkan data yang telah melalui proses preprocessing.

### 2. Decision Tree

Decision Tree digunakan sebagai model klasifikasi kedua untuk melihat hasil prediksi berdasarkan pola dan fitur yang terdapat pada data.

### 3. Random Forest

Random Forest digunakan sebagai model klasifikasi ketiga yang menggabungkan beberapa Decision Tree untuk menghasilkan prediksi yang lebih akurat dan stabil berdasarkan pola pada data.

## Evaluasi Model

Performa model dievaluasi menggunakan beberapa metrik, yaitu:

- Accuracy
- Precision
- Recall
- F1-Score
- Classification Report
- Confusion Matrix

Hasil dari kedua model kemudian disimpan dan ditampilkan dalam bentuk tabel perbandingan.

## Kategori Prediksi

Model melakukan klasifikasi terhadap tiga kategori status mahasiswa:

- **Dropout**
- **Graduate**
- **Enrolled**

## Teknologi yang Digunakan

Project ini dibuat menggunakan:

- Python
- Google Colab
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn

## Struktur Repository

```text
AI_SDG4_Student_Dropout_Prediction/
│
├── AI_SDG4_Student_Dropout_Prediction.ipynb
├── README.md
└── dataset/
    └── student_data.csv
.
