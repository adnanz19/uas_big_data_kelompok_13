# Big Data Analytics Pada Kasus Data Student's Academic Performance menggunakan Algoritma K-Nearest Neighbor

**Kelompok 13** | **Kelas A S-1 Informatika**

## 👥 Anggota Kelompok

| Nama                      | NPM / NIM  |
| :------------------------ | :--------- |
| **Pandu Nugraha Saputra** | 2310511029 |
| **Bima Adnandita** | 2310511039 |
| **Rafli Wahyu Pratama** | 2310511031 |

---

## 📝 Latar Belakang

Proyek ini didasari oleh urgensi perlunya deteksi dini performa mahasiswa untuk mencegah kegagalan akademik (dropout). Terdapat keterbatasan pada studi terdahulu, seperti penggunaan dataset berskala kecil, pengabaian faktor eksternal (sosial-ekonomi & kebiasaan belajar), serta penanganan data tidak seimbang (imbalanced dataset) yang kurang optimal. Proyek ini mengatasi keterbatasan tersebut dengan mengimplementasikan algoritma Machine Learning **K-Nearest Neighbors (KNN)** pada 1 juta baris data _Student's Academic Performance_ dari Kaggle guna menghasilkan model prediksi yang komprehensif dan dapat digeneralisasi.

## 🎯 Tujuan Proyek

1. Mengidentifikasi dan memetakan faktor-faktor utama (aspek akademik, demografi, dan sosial-ekonomi) yang paling memengaruhi IPK mahasiswa dari dataset skala besar.
2. Membangun model Machine Learning berbasis algoritma KNN yang mampu memprediksi nilai IPK serta mengklasifikasikan status risiko dropout mahasiswa secara akurat.
3. Menyediakan benchmark sistem prediktif yang terukur untuk mendukung pengambilan keputusan berbasis data (data-driven) bagi pihak manajemen institusi pendidikan.

## ⚙️ Alur Pemrosesan Data (Data Pipeline)

<img src="images/Pipeline_BigData.png" alt="Data Pipeline" width="400">

1. **Ekstraksi Data (Extract):** Mengimpor 1.000.000 baris dan 52 kolom dataset dari Kaggle.
2. **Transformasi & Pembersihan (Transform):**
   - Mengeliminasi ~50.000 data anomali/invalid (contoh: menghapus 4.489 baris data dengan IPK 4.0 palsu yang terbukti cacat secara statistik).
   - Menangani missing value dan membuang data dengan nilai ujian/tugas tidak logis (skor > 100 atau < 0).
3. **Feature Selection & Engineering:** - Melakukan reduksi dimensi fitur via analisis korelasi.
   - Mentransformasi variabel mentah menjadi indikator baru seperti _Study Efficiency Index_, _Health & Wellness Score_, dan _Total Tech Usage_.
4. **Pemodelan & Validasi (Modeling):**
   - Menggunakan teknik **Stratified Sampling 10%** (100.000 baris) untuk mengatasi tantangan komputasi berlebih dari algoritma berbasis instance seperti KNN.
   - Melatih algoritma KNN yang divalidasi menggunakan Stratified K-Fold Cross Validation.

---

## 📊 Analisis & Visualisasi Data (EDA)

Dalam proses *Exploratory Data Analysis*, kami melakukan pembersihan data dan menemukan beberapa pola deskriptif perilaku mahasiswa yang saling berkaitan:

### 1. Identifikasi & Pembersihan Anomali Data (GPA 4.0 Palsu)
Pada distribusi mentah, kami menemukan anomali fatal pada nilai **Final GPA 4.0**. Terdapat ribuan baris data siswa dengan IPK sempurna namun tercatat memiliki 0 jam belajar dan presensi yang sangat rendah. Baris *error* sistem ini kami bersihkan secara statistik untuk mencegah model memelajari pola yang salah (bias).

![Distribusi GPA Sebelum dan Sesudah Cleaning](images/distribusi_gpa.png)

### 2. Analisis Deskriptif (Temuan Perilaku Mahasiswa)
Dari data yang telah dibersihkan dan fitur baru yang telah diekstraksi, kami menemukan 3 wawasan utama mengenai keseimbangan hidup mahasiswa:

**A. Efisiensi Belajar vs GPA**
![Efisiensi Belajar vs GPA](images/efisiensi_gpa.png)
- **Temuan:** Terdapat kenaikan IPK yang sangat stabil dan konsisten seiring meningkatnya tingkat efisiensi belajar (rasio antara durasi belajar yang efektif dengan presensi/pemahaman). Hal ini membuktikan bahwa kualitas belajar lebih penting daripada sekadar kuantitas jam belajar.

**B. Jam Tidur vs Indeks Stres**
![Jam Tidur vs Indeks Stres](images/tidur_stres.png)
- **Temuan:** Peningkatan durasi jam tidur berbanding lurus secara signifikan dengan penurunan indeks stres mahasiswa. Kurang tidur terbukti menjadi pemicu utama tingginya beban mental mahasiswa.

**C. Penggunaan Teknologi vs Stres Mental**
![Penggunaan Teknologi vs Stres Mental](images/teknologi_stres.png)
- **Temuan:** Penggunaan teknologi intensif pada dataset ini terbukti berkorelasi dengan *penurunan* tingkat stres mental. Hal ini mengindikasikan bahwa teknologi sering digunakan sebagai sarana hiburan (game/media sosial) untuk relaksasi di luar jam akademik.

### 3. Peta Korelasi Variabel (Heatmap)
Analisis multivariat menunjukkan bagaimana faktor-faktor di atas secara keseluruhan memengaruhi IPK akhir.

![Heatmap Korelasi](images/heatmap_korelasi.png)

- **Temuan Utama Heatmap:** Variabel akademik (seperti `standardized_exam_score`) memiliki korelasi positif paling kuat terhadap `final_gpa`. Di sisi lain, terdapat korelasi negatif yang jelas antara tingkat stres tinggi dengan penurunan performa (peningkatan *flag* risiko *dropout*).

---

## 🚀 Evaluasi Performa Model ML

Setelah dilatih menggunakan data yang bersih, model KNN menunjukkan performa yang menjanjikan:

**1. KNN Regressor (Prediksi final_gpa)**
- **Rata-rata R² Score:** 0.6493
- **Rata-rata Mean Absolute Error (MAE):** 0.2944

**2. KNN Classifier (Deteksi at_risk_flag)**
- **Accuracy:** 0.78 (78%)
- **Precision (Macro Avg):** 0.78
- **Recall (Macro Avg):** 0.78
- **F1-Score (Macro Avg):** 0.78

---

## 💡 Insight & Tindak Lanjut Strategis

Dari hasil pemodelan dan analisis EDA di atas, manajemen institusi pendidikan dapat memetakan mahasiswa ke dalam profil tertentu untuk melakukan intervensi berbasis data (*data-driven*):

🎓 **Profil 1: Top Performer (Efisiensi Tinggi)**
- **Karakteristik:** Memiliki *Study Efficiency Index* tinggi. Mereka membuktikan bahwa IPK unggul dicapai bukan dari durasi belajar ekstrem, melainkan keseimbangan antara fokus akademik dan jam tidur yang teratur.
- **Tindak Lanjut:** Jadikan kelompok ini sebagai agen pendampingan (*peer-mentor*) bagi mahasiswa di tingkat bawahnya, serta berikan apresiasi/beasiswa.

⚠️ **Profil 2: Berisiko Tinggi (Risiko Dropout)**
- **Karakteristik:** Terdeteksi memiliki indeks stres tinggi, jam tidur minim, dan efisiensi belajar rendah. Kondisi kumulatif ini secara matematis menggerus IPK mereka hingga diklasifikasikan ke dalam `at_risk_flag`.
- **Tindak Lanjut (Sistem Peringatan Dini):** Ketika model memprediksi status risiko (*at risk*), kampus harus segera mengalokasikan bimbingan konseling proaktif serta lokakarya manajemen waktu, *sebelum* kegagalan akademik terjadi.

**Kesimpulan Utama:**
Durasi jam belajar saja **tidak cukup** jika tidak diimbangi dengan kualitas kesejahteraan mahasiswa. Efisiensi belajar dan kesejahteraan mental (tidur, stres, aktivitas relaksasi) adalah pilar penentu IPK yang sebenarnya.

---

## 📺 Video Presentasi Proyek

Tonton penjelasan lengkap mengenai proses analisis, pembersihan data, dan visualisasi temuan kami pada video presentasi berikut:

[![Video Presentasi Kelompok 13](https://img.youtube.com/vi/h1h2nzqtd9c/maxresdefault.jpg)](https://youtu.be/h1h2nzqtd9c)
_(Klik gambar di atas untuk memutar video)_