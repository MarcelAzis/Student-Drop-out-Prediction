[README_revisi.md](https://github.com/user-attachments/files/33257765/README_revisi.md)
# Student Dropout Prediction

## Sistem Peringatan Dini Risiko Putus Studi Mahasiswa untuk Mendukung SDG 4

Proyek ini menerapkan *machine learning* untuk mengklasifikasikan status akademik mahasiswa ke dalam tiga kelas, yaitu **Dropout**, **Enrolled**, dan **Graduate**, berdasarkan tujuh fitur akademik dan karakteristik mahasiswa.

Proyek ini dikaitkan dengan **Sustainable Development Goal (SDG) 4: Quality Education (Pendidikan Berkualitas)**. Hasil model dirancang sebagai alat bantu awal untuk mengidentifikasi mahasiswa yang mungkin membutuhkan pemeriksaan atau pendampingan lebih lanjut. Prediksi bukan vonis, dan tidak boleh menjadi satu-satunya dasar pengambilan keputusan tentang mahasiswa.

> **Batasan penting:** dataset berasal dari konteks pendidikan tinggi di Portugal. Hasil model belum membuktikan bahwa sistem dapat memprediksi dropout secara prospektif di perguruan tinggi Indonesia. Penerapan nyata membutuhkan validasi menggunakan data lokal, evaluasi waktu prediksi yang tepat, pemeriksaan bias, dan perlindungan privasi.

## Tujuan Proyek

- Memeriksa kualitas data dan melakukan *Exploratory Data Analysis* (EDA).
- Menggunakan tujuh fitur yang ditetapkan sebagai masukan model.
- Melatih dan membandingkan model Decision Tree dan Random Forest.
- Menggunakan GridSearchCV dengan 3-fold cross-validation untuk mencari parameter terbaik berdasarkan accuracy validasi pada data training.
- Mengevaluasi model menggunakan accuracy, precision, recall, F1-score, Macro F1, Recall Dropout, dan confusion matrix.
- Menyusun daftar prioritas pemeriksaan berdasarkan skor model untuk kelas Dropout.
- Mendemonstrasikan prediksi dari input manual dengan tujuh fitur.

## Dataset

Dataset yang digunakan adalah **[Predict Students' Dropout and Academic Success](https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success)** dari UCI Machine Learning Repository.

Karakteristik dataset asli:

- **Jumlah observasi:** 4.424 mahasiswa.
- **Jumlah kolom:** 37, terdiri dari 36 fitur dan satu kolom target.
- **Kolom target:** `Target`.
- **Kelas target:** `Dropout`, `Enrolled`, dan `Graduate`.
- **Konteks data:** pendidikan tinggi di Portugal.

Dataset perlu diunduh dari sumber resmi dan disiapkan sebagai file CSV untuk diunggah ke Google Colab. README ini tidak menyertakan dataset secara otomatis; lokasi dan nama file pada repository harus mengikuti file yang benar-benar diunggah.

**Periksa format CSV sebelum menjalankan notebook.** Jika file yang diunduh menggunakan titik koma sebagai pemisah kolom, file harus dibaca dengan delimiter yang sesuai (misalnya `sep=';'`). Setelah pemuatan, pastikan kolom `Target` dan nama-nama fitur terbaca sebagai kolom terpisah, bukan sebagai satu kolom panjang.

## Fitur yang Digunakan

Model menggunakan tujuh fitur berikut. Kolom `Target` adalah label yang diprediksi, bukan fitur input.

| No. | Nama kolom | Keterangan |
|---:|---|---|
| 1 | `Curricular units 1st sem (enrolled)` | Jumlah unit/mata kuliah yang diambil pada semester pertama |
| 2 | `Curricular units 1st sem (approved)` | Jumlah unit/mata kuliah yang lulus pada semester pertama |
| 3 | `Curricular units 1st sem (grade)` | Nilai rata-rata/indikator nilai semester pertama sesuai definisi dataset |
| 4 | `Tuition fees up to date` | Indikator status pembayaran biaya kuliah sesuai pengodean dataset |
| 5 | `Scholarship holder` | Indikator penerima beasiswa sesuai pengodean dataset |
| 6 | `Admission grade` | Nilai masuk mahasiswa |
| 7 | `Age at enrollment` | Usia mahasiswa saat mulai kuliah |

Pemilihan fitur dilakukan secara manual untuk membatasi masukan model. Ketujuh fitur ini **tidak otomatis merupakan tujuh fitur paling berpengaruh**. Feature importance yang dihasilkan model menunjukkan kepentingan prediktif dalam model, bukan hubungan sebab-akibat.

## Alur Pengerjaan

1. Mengimpor library dan mengunggah dataset.
2. Memeriksa struktur data, nilai kosong, baris duplikat, dan distribusi target.
3. Melakukan EDA terhadap distribusi kelas dan beberapa fitur.
4. Memilih tujuh fitur input dan kolom `Target`.
5. Membagi data menjadi training dan testing dengan rasio 80:20 serta stratifikasi target.
6. Melatih Decision Tree dan Random Forest.
7. Melakukan pencarian parameter dengan GridSearchCV dan 3-fold cross-validation pada data training.
8. Membandingkan model berdasarkan hasil cross-validation, lalu mengevaluasi model pada data testing.
9. Menampilkan metrik evaluasi, confusion matrix, dan feature importance.
10. Mengurutkan data testing berdasarkan skor Dropout dan menghitung Precision@20 sebagai analisis tambahan.
11. Mendemonstrasikan prediksi untuk input manual.

Pembagian training/testing dan proses optimasi harus dilakukan tanpa menggunakan data testing untuk memilih parameter. Data testing digunakan untuk evaluasi akhir agar estimasi performa tidak terlalu optimistis.

## Model Machine Learning

### Decision Tree

Decision Tree membangun aturan keputusan berbentuk pohon berdasarkan fitur input. Model ini relatif mudah dijelaskan, tetapi dapat mengalami *overfitting* jika kompleksitasnya tidak dikendalikan.

### Random Forest

Random Forest menggabungkan prediksi banyak pohon keputusan. Model ini menjadi pembanding bagi Decision Tree dan dapat menangkap pola yang lebih beragam.

Parameter dan rentang pencarian yang benar-benar digunakan mengikuti kode pada notebook. Hasil model terbaik harus ditentukan dari hasil cross-validation pada data training, bukan dengan memilih model berdasarkan hasil testing.

## Evaluasi Model

Metrik evaluasi yang digunakan meliputi:

- **Accuracy:** proporsi seluruh prediksi yang benar.
- **Precision per kelas:** ketepatan prediksi untuk setiap kelas.
- **Recall per kelas:** proporsi anggota aktual setiap kelas yang berhasil dikenali.
- **F1-score:** gabungan precision dan recall.
- **Macro F1:** rata-rata F1-score ketiga kelas dengan bobot yang sama.
- **Recall Dropout:** proporsi mahasiswa berlabel aktual `Dropout` yang berhasil dikenali model.
- **Confusion matrix:** jumlah prediksi benar dan kesalahan antar kelas.

Hasil kedua model sebaiknya dibandingkan menggunakan metrik yang sama. Karena tujuan proyek adalah membantu mengidentifikasi kemungkinan dropout, Recall Dropout penting untuk diperhatikan bersama precision, Macro F1, dan accuracy. Meningkatkan recall saja dapat menambah *false positive*, sehingga hasil tetap perlu diperiksa manusia.

**Target accuracy di atas 70% adalah sasaran eksperimen, bukan hasil yang dijamin.** Angka performa final hanya boleh dicantumkan setelah notebook dijalankan pada dataset yang benar dan hasilnya dicatat.

## Early Warning System (EWS)

Sebagai demonstrasi EWS, model menggunakan skor yang dihasilkan `predict_proba()` untuk kelas `Dropout`, lalu mengurutkan baris data testing dari skor tertinggi ke terendah. Notebook dapat menampilkan hingga 20 baris teratas dan menghitung Precision@20, yaitu proporsi data yang benar-benar berlabel `Dropout` di antara 20 baris teratas tersebut (atau seluruh baris yang tersedia jika jumlahnya kurang dari 20).

Daftar ini merupakan **demonstrasi pemeringkatan retrospektif pada data testing**, bukan daftar mahasiswa aktif yang sudah tervalidasi untuk intervensi nyata. Dalam penggunaan operasional, perlu dipastikan bahwa fitur tersedia pada saat prediksi, label target merujuk pada kejadian setelah waktu prediksi, dan daftar hanya dapat diakses petugas berwenang.

Skor `predict_proba()` tidak otomatis merupakan probabilitas risiko yang terkalibrasi. Skor tinggi berarti model menempatkan data tersebut lebih tinggi dalam urutan prediksi, bukan kepastian bahwa mahasiswa akan dropout.

## Prediksi Input Manual

Notebook menyediakan demonstrasi prediksi dengan memasukkan tujuh fitur secara manual. Nilai harus mengikuti definisi, pengodean, dan skala dataset asli.

- Nilai semester pertama mengikuti skala pada dataset sumber (umumnya 0–20 untuk nilai yang relevan).
- `Tuition fees up to date` dan `Scholarship holder` menggunakan pengodean dataset, umumnya 0/1.
- `Admission grade` mengikuti skala dataset sumber (umumnya 0–200).
- Jumlah unit/mata kuliah dan usia harus berupa nilai yang masuk akal sesuai definisi kolom.

Jangan menganggap skala nilai atau pengodean tersebut setara langsung dengan sistem penilaian perguruan tinggi Indonesia. Input manual hanya demonstrasi teknis; untuk penggunaan nyata, fitur dan skala harus disesuaikan serta divalidasi dengan data lokal.

## Arti Kelas Target

- **Dropout:** mahasiswa yang tercatat pada kelas putus studi dalam dataset.
- **Enrolled:** mahasiswa yang tercatat masih menjalani studi pada titik pencatatan dataset.
- **Graduate:** mahasiswa yang tercatat telah menyelesaikan studi.

`Enrolled` adalah **status akademik**, bukan kategori risiko sedang dan bukan bukti bahwa mahasiswa aman dari dropout. Status aktual dan skor risiko model adalah dua hal yang berbeda.

## Teknologi

- Python
- Google Colab
- Pandas
- NumPy
- Matplotlib
- Scikit-learn

## Struktur Repository

Contoh struktur repository (sesuaikan dengan file yang benar-benar ada di GitHub):

```text
Student-Drop-out-Prediction/
├── README.md
├── SDG4_Early_Warning_7_Fitur_3_Kelas.ipynb
└── dataset/                 # opsional, jika dataset memang disimpan di repository
    └── data.csv
```

Jika dataset tidak disimpan di GitHub, hapus bagian `dataset/` dari struktur di atas dan jelaskan bahwa pengguna perlu mengunduh dataset dari UCI. Pertimbangkan lisensi, ketentuan sumber, privasi, dan ukuran file sebelum mengunggah data ke repository publik.

## Cara Menjalankan

1. Unduh dataset dari [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success).
2. Buka file `SDG4_Early_Warning_7_Fitur_3_Kelas.ipynb` di Google Colab.
3. Jalankan cell secara berurutan. Jika notebook meminta unggahan, unggah file dataset CSV yang sesuai.
4. Pastikan pemuatan data berhasil: jumlah kolom masuk akal, nama fitur terbaca terpisah, dan kolom `Target` tersedia.
5. Periksa hasil pemeriksaan data dan EDA.
6. Jalankan pembagian data, pelatihan model, dan evaluasi.
7. Bandingkan metrik kedua model dan periksa confusion matrix, terutama kesalahan pada kelas `Dropout`.
8. Periksa feature importance dan daftar pemeringkatan EWS dengan memahami batasannya.
9. Coba input manual hanya untuk demonstrasi.

Nama file, format delimiter, dan lokasi dataset harus sesuai dengan kode pada notebook. Hasil dapat berbeda akibat versi library, perubahan dataset, pembagian data, atau konfigurasi eksperimen.

## Kesimpulan dan Penggunaan yang Bertanggung Jawab

Proyek ini mendemonstrasikan klasifikasi status akademik tiga kelas dan pemeringkatan skor Dropout sebagai pendekatan awal EWS yang dikaitkan dengan SDG 4. Keberhasilan proyek tidak hanya dinilai dari accuracy, tetapi juga dari kemampuan mengenali kelas Dropout dan memahami kesalahan prediksi.

Hasil model dapat membantu menentukan siapa yang perlu **ditinjau lebih lanjut**, misalnya untuk menawarkan konseling atau dukungan akademik/finansial. Model tidak boleh digunakan untuk memberi label permanen, menghukum, menolak layanan, atau mengambil keputusan penting tanpa pemeriksaan manusia. Implementasi nyata membutuhkan validasi lokal, pengujian pada periode waktu yang sesuai, pemeriksaan bias dan kalibrasi, tata kelola akses, serta perlindungan data mahasiswa.

## Referensi

Realinho, V., Machado, J., Baptista, L., & Martins, M. V. (2021). *Predict Students' Dropout and Academic Success*. UCI Machine Learning Repository.

Dataset: https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success
