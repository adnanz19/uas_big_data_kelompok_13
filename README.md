# Big Data Analytics Pada Kasus Data Student's Academic Performance menggunakan Algoritma K-Nearest Neighbor

**Kelompok 13** | **Kelas A S-1 Informatika**

## 👥 Anggota Kelompok

| Nama                      | NPM / NIM  |
| :------------------------ | :--------- |
| **Pandu Nugraha Saputra** | 2310511029 |
| **Bima Adnandita**        | 2310511039 |
| **Rafli Wahyu Pratama**   | 2310511031 |

---

## 📝 Latar Belakang

Proyek ini didasari oleh urgensi perlunya deteksi dini performa mahasiswa untuk mencegah kegagalan akademik (dropout). Terdapat keterbatasan pada studi terdahulu, seperti penggunaan dataset berskala kecil, pengabaian faktor eksternal (sosial-ekonomi & kebiasaan belajar), serta penanganan data tidak seimbang (imbalanced dataset) yang kurang optimal. Proyek ini mengatasi keterbatasan tersebut dengan mengimplementasikan algoritma Machine Learning **K-Nearest Neighbors (KNN)** pada 1 juta baris data _Student's Academic Performance_ dari Kaggle guna menghasilkan model prediksi yang komprehensif dan dapat digeneralisasi.

## 🎯 Tujuan Proyek

1. Mengidentifikasi dan memetakan faktor-faktor utama (aspek akademik, demografi, dan sosial-ekonomi) yang paling memengaruhi IPK mahasiswa dari dataset skala besar.
2. Membangun model Machine Learning berbasis algoritma KNN yang mampu memprediksi nilai IPK serta mengklasifikasikan status risiko dropout mahasiswa secara akurat.
3. Menyediakan benchmark sistem prediktif yang terukur untuk mendukung pengambilan keputusan berbasis data (data-driven) bagi pihak manajemen institusi pendidikan.

## ⚙️ Alur Pemrosesan Data (Data Pipeline)

<img src="images/Pipeline_BigData.png" alt="Data Pipeline" width="700">


1. **Ekstraksi Data (Extract):** Mengimpor 1.000.000 baris dan 52 kolom dataset dari Kaggle.
2. **Transformasi & Pembersihan (Transform):**
   - Mengeliminasi ~50.000 data anomali/invalid (contoh: menghapus 4.489 baris data dengan IPK 4.0 palsu yang terbukti cacat secara statistik).
   - Menangani missing value dan membuang data dengan nilai ujian/tugas tidak logis (skor > 100 atau < 0).
3. **Feature Selection & Engineering:** - Melakukan reduksi dimensi fitur via analisis korelasi.
   - Mentransformasi variabel mentah menjadi indikator baru seperti _Study Efficiency Index_, _Health & Wellness Score_, dan _Total Tech Usage_.
4. **Pemodelan & Validasi (Modeling):**
   - Menggunakan teknik **Stratified Sampling 10%** (100.000 baris) untuk mengatasi tantangan komputasi berlebih dari algoritma berbasis instance seperti KNN.
   - Melatih algoritma KNN yang divalidasi menggunakan Stratified K-Fold Cross Validation.

## 📊 Temuan Utama (Analisis Deskriptif)

- **Efisiensi Belajar:** Terlihat kenaikan IPK yang sangat stabil dan konsisten seiring meningkatnya tingkat efisiensi belajar.
- **Stres dan Jam Tidur:** Peningkatan jam tidur berbanding lurus dengan penurunan indeks stres mahasiswa.
- **Penggunaan Teknologi:** Penggunaan teknologi intensif terbukti berkorelasi dengan penurunan tingkat stres mental.

## 🚀 Evaluasi Performa Model ML

**1. KNN Regressor (final_gpa)**

- **Rata-rata R² Score:** 0.6493
- **Rata-rata Mean Absolute Error (MAE):** 0.2944

**2. KNN Classifier (at_risk_flag)**

- **Accuracy:** 0.78 (78%)
- **Precision (Macro Avg):** 0.78
- **Recall (Macro Avg):** 0.78
- **F1-Score (Macro Avg):** 0.78

## 💡 Kesimpulan & Rekomendasi

**Kesimpulan:**
Efisiensi belajar (rasio jam belajar efektif terhadap stres) dan kesejahteraan akademik (keseimbangan tidur, aktivitas fisik, dan stres) terbukti secara matematis berdampak langsung pada peningkatan IPK. Durasi jam belajar saja tidak cukup jika tidak diimbangi dengan kualitas kesejahteraan mahasiswa.

**Rekomendasi:**
Institusi pendidikan direkomendasikan untuk menggunakan model prediktif ini sebagai alat intervensi dini kepada mahasiswa yang terdeteksi memiliki profil kesejahteraan rendah dan risiko dropout tinggi. Intervensi dapat berupa konseling akademik atau psikologis yang ditargetkan untuk membantu mahasiswa mengelola stres dan meningkatkan efisiensi belajar.

---

## 📺 Video Presentasi Proyek

Tonton penjelasan lengkap mengenai proses analisis, pembersihan data, dan visualisasi temuan kami pada video presentasi berikut:

[![Video Presentasi Kelompok 13](https://img.youtube.com/vi/h1h2nzqtd9c/maxresdefault.jpg)](https://youtu.be/h1h2nzqtd9c)
_(Klik gambar di atas untuk memutar video)_
