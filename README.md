# Tugas UTS Machine Learning

Repositori ini berisi pengerjaan Ujian Tengah Semester (UTS) mata kuliah Machine Learning untuk implementasi algoritma Linear Regression dan Logistic Regression secara mandiri menggunakan Python dan NumPy.

---

## Identitas Mahasiswa
- **Nama:** Fauzan Aristo Ramadhan
- **NIM:** 241011403335
- **Kelas:** Reguler B
- **Program Studi:** Teknik Informatika (S-1)
- **Random State:** 35 (2 digit terakhir NIM)

---

## Ringkasan Hasil Pengerjaan

### 1. Bagian A — Linear Regression (Dataset: `Ads_Data.csv`)
Tujuan bagian ini adalah memodelkan pengaruh biaya iklan ($X$, dalam juta rupiah) terhadap omset penjualan ($y$, dalam juta rupiah).

- **Persamaan Regresi (Normal Equation):**  
  $$\hat{y} = 27.6480 + 9.1215 \cdot X$$
  - Nilai intercept ($27.65$) artinya estimasi penjualan dasar saat biaya iklan nol adalah sekitar Rp27,65 juta.
  - Koefisien ($9.12$) menandakan setiap penambahan biaya iklan Rp1 juta diperkirakan menaikkan penjualan rata-rata Rp9,12 juta.

- **Tabel Evaluasi Model:**
  | Dataset | MAE (Juta Rp) | MSE | RMSE (Juta Rp) | $R^2$ Score |
  |---|:---:|:---:|:---:|:---:|
  | **Training** | 4.8030 | 40.6667 | 6.3770 | 0.9298 (92.98%) |
  | **Testing** | 3.6673 | 18.8028 | 4.3362 | **0.9688 (96.88%)** |

- **Eksperimen Learning Rate pada Gradient Descent (5000 iterasi):**
  - `lr = 0.001`: Terlalu lambat, belum konvergen sempurna setelah 5000 iterasi.
  - `lr = 0.02`: Paling optimal, hasilnya konvergen mendekati nilai analisis Normal Equation.
  - `lr = 0.1`: Divergen (gagal konvergen) karena langkah pembaruan terlalu besar sehingga nilai loss mengalami overflow.

- **Hasil Prediksi Kasus Baru:**
  - Iklan Rp4,5 Juta $\rightarrow$ Prediksi Penjualan: **Rp68,69 Juta**
  - Iklan Rp7,0 Juta $\rightarrow$ Prediksi Penjualan: **Rp91,50 Juta**
  - Iklan Rp12,0 Juta $\rightarrow$ Prediksi Penjualan: **Rp137,11 Juta** *(Ekstrapolasi: perlu dicermati karena angka 12 juta berada di luar rentang data historis 0.8–9.9 juta)*.

---

### 2. Bagian B — Logistic Regression (Dataset: `Email_Data.csv`)
Tujuan bagian ini adalah mengklasifikasikan email menjadi Spam (1) atau Bukan Spam (0) berdasarkan jumlah link ($X_1$) dan kata promo ($X_2$).

- **Persamaan Probabilitas:**  
  $$P(\text{Spam}) = \sigma(-10.3273 + 0.9351 \cdot \text{JumlahLink} + 0.8704 \cdot \text{KataPromo})$$

- **Garis Batas Keputusan (*Decision Boundary* pada $P=0.5$):**  
  $$\text{KataPromo} = 11.8650 - 1.0743 \cdot \text{JumlahLink}$$

- **Eksperimen Ambang Batas (*Threshold*):**
  | Threshold | Akurasi | Precision | Recall | F1-Score | Keterangan |
  |:---:|:---:|:---:|:---:|:---:|---|
  | **0.3** | 73.33% | 62.50% | 83.33% | 0.7143 | Terlalu sensitif (banyak email normal kena tandai spam) |
  | **0.5** | 80.00% | 71.43% | 83.33% | 0.7692 | Ambang batas standar |
  | **0.7 (Dipilih)** | **86.67%** | **100.00%** | **66.67%** | **0.8000** | **Terbaik: Presisi 100% (FP = 0), aman dari email penting terbuang** |

- **Prediksi Email Baru (Threshold 0.7):**
  - E1 (1 link, 2 promo) $\rightarrow P(\text{Spam}) = 0.0005 \rightarrow$ **Bukan Spam (0)**
  - E2 (5 link, 6 promo) $\rightarrow P(\text{Spam}) = 0.3942 \rightarrow$ **Bukan Spam (0)**
  - E3 (9 link, 10 promo) $\rightarrow P(\text{Spam}) = 0.9989 \rightarrow$ **Spam (1)**
  - E4 (2 link, 11 promo) $\rightarrow P(\text{Spam}) = 0.7534 \rightarrow$ **Spam (1)**

---

### 3. Bagian C — Pemahaman Konsep
Seluruh 5 pertanyaan konsep pada notebook sudah dijawab lengkap, mencakup alasan penamaan regresi logistik, fungsi sigmoid, perbandingan Normal Equation vs Gradient Descent, penyebab overfitting, perbandingan MSE vs Log Loss, serta pengaruh variasi NIM pada random state.

---

### 4. Bagian Bonus — Perbandingan dengan Scikit-Learn
- Pada Linear Regression, nilai intercept, koefisien, MSE, dan $R^2$ antara implementasi manual dengan scikit-learn menghasilkan angka yang persis sama.
- Pada Logistic Regression, saat regularisasi scikit-learn dinonaktifkan (`penalty=None`), hasil akurasi pada data testing sama persis dengan kode Gradient Descent manual.

---

## Berkas dalam Repositori
- `README.md` : Dokumentasi identitas dan ringkasan hasil UTS
- `tugas_UTS.ipynb` : Jupyter Notebook lengkap dengan kode, grafik, dan jawaban analisis
- `Ads_Data.csv` : Dataset untuk Linear Regression
- `Email_Data.csv` : Dataset untuk Logistic Regression
