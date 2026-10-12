# 🎓 Early Warning System (EWS) Risiko Dropout Mahasiswa
> **Proyek AI Kelompok 4** — Sistem Peringatan Dini Akademik Berbasis Machine Learning untuk Memprediksi dan Mengurutkan Tingkat Risiko Dropout Mahasiswa.

---

## 📌 Ringkasan Proyek
Proyek ini bertujuan untuk membangun **Early Warning System (EWS)** yang dapat memprediksi status akademik mahasiswa ke dalam 3 kategori (*Dropout*, *Enrolled*, atau *Graduate*). Selain melakukan klasifikasi, sistem ini mengurutkan mahasiswa berdasarkan skor risiko terjadinya *dropout* sehingga pihak perguruan tinggi dapat melakukan intervensi atau bimbingan akademik sejak dini.

Model dikembangkan menggunakan algoritma **Decision Tree** dan **Random Forest** berdasarkan data performa akademik semester awal serta latar belakang sosio-ekonomi mahasiswa.

---

## 📊 Dataset
* **Nama Dataset:** [Predict Students' Dropout and Academic Success (UCI Machine Learning Repository ID 697)](https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success)
* **Ukuran Dataset:** 4.424 baris data mahasiswa
* **Jumlah Fitur:** 36 fitur input + 1 target
* **Konteks Data:** Pendidikan Tinggi di Portugal

### Variabel Target (`Target`):
* `Graduate` (Lulus): 2.209 mahasiswa (49.93%)
* `Dropout` (Putus Sekolah/Kuliah): 1.421 mahasiswa (32.12%)
* `Enrolled` (Masih Aktif): 794 mahasiswa (17.95%)

### Fitur-Fitur Utama yang Digunakan:
* **Performa Akademik:** Jumlah mata kuliah diambil, lulus, dan nilai semester 1 & 2 (`Curricular units 1st/2nd sem`).
* **Finansial & Bantuan:** Status kelancaran pembayaran SPP (`Tuition fees up to date`) dan penerima beasiswa (`Scholarship holder`).
* **Demografi & Pendaftaran:** Nilai ujian masuk, usia saat mendaftar, kualifikasi/pendidikan orang tua, status pernikahan, dan tingkat pengangguran/inflasi daerah.

---

## 🔍 Temuan Utama Exploratory Data Analysis (EDA)
1. **Performa Akademik Semester 1:** Mahasiswa dengan status *Graduate* rata-rata meluluskan 6,23 mata kuliah di semester 1 dengan nilai rata-rata 12,64/20. Sementara mahasiswa *Dropout* hanya meluluskan rata-rata 2,55 mata kuliah dengan nilai rata-rata 7,26/20.
2. **Status Pembayaran SPP (`Tuition fees`):** Mahasiswa yang menunggak pembayaran SPP memiliki tingkat *dropout* hingga **86.55%**, sedangkan mahasiswa yang pembayarannya lancar hanya memiliki tingkat *dropout* sebesar **24.74%**.
3. **Penerima Beasiswa (`Scholarship holder`):** Penerima beasiswa memiliki angka kelulusan jauh lebih tinggi (**75.98%**) dibandingkan bukan penerima beasiswa (**41.32%**).

---

## 🛠️ Algoritma & Metodologi
Proyek ini mengimplementasikan alur kerja *Data Science* / *Machine Learning* lengkap menggunakan Python:

1. **Data Ingestion & Cleaning:**
   * Deteksi nilai kosong (*missing values*) dan duplikasi data.
   * Pembersihan format teks/spasi pada variabel target.
2. **Exploratory Data Analysis (EDA):**
   * Visualisasi distribusi kelas target & analisis ketidakseimbangan kelas (*class imbalance*).
   * Visualisasi *Boxplot* & *Bar Plot* fitur akademik dan keuangan terhadap status mahasiswa.
3. **Supervised Learning Modeling:**
   * **Decision Tree Classifier**
   * **Random Forest Classifier**
4. **Ranking Risiko Dropout:**
   * Mengurutkan risiko *dropout* mahasiswa berdasarkan peluang/skor probabilitas prediksi model.

---

## 💻 Teknologi yang Digunakan
* **Bahasa Pemrograman:** Python 3.x
* **Lingkungan Pengembangan:** Google Colab / Jupyter Notebook
* **Library Utama:**
  * `pandas` & `numpy` — Manipulasi & Analisis Data
  * `matplotlib` & `seaborn` — Visualisasi Data
  * `scikit-learn` — Pemodelan Machine Learning (Decision Tree & Random Forest)

---

## 👥 Anggota Kelompok (Kelompok 4)
* **Fatimah Shabirah**
* *(Tambahkan nama anggota kelompok lainnya di sini)*
*
