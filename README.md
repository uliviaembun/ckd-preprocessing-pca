# Preprocessing Data dan PCA: Chronic Kidney Disease

Proyek ini memiliki fokus utama melakukan pembersihan data yang komprehensif dan reduksi dimensi menggunakan **Principal Component Analysis (PCA)** pada dataset medis *Chronic Kidney Disease*.

Tujuannya adalah menyiapkan data mentah yang penuh dengan *missing values*, *outliers*, dan inkonsistensi menjadi dataset yang bersih dan efisien untuk pemodelan *machine learning*.

## Metodologi
Berikut adalah tahapan teknis yang dilakukan dalam *notebook*:

1.  **Exploratory Data Analysis (EDA)**
    * Analisis distribusi fitur.
    * Visualisasi korelasi antar fitur (Matriks Korelasi & Pair Plot).
    * Analisis ketidaksamaan (*Dissimilarity Analysis*) menggunakan *Gower Distance*.

2.  **Penanganan Missing Values**
    * **Identifikasi Pola:** Menggunakan *heatmap* dari library `missingno`.
    * **Imputasi Median:** Diterapkan pada data numerik dengan distribusi *skewed* (`age`, `bp`, `sc`, `sod`, `pot`, `hemo`, `pcv`).
    * **KNN Imputer:** Diterapkan pada fitur ordinal untuk menjaga struktur data.
    * **Imputasi Logis (Domain Knowledge):** Mengisi nilai `rbc` dan `pc` dengan "abnormal" jika target kelas adalah "ckd", dan sebaliknya.
    * **Dropping:** Menghapus baris pada fitur dengan jumlah *missing value* yang sangat sedikit.

3.  **Data Cleaning & Outlier Removal**
    * Memperbaiki kesalahan penulisan (*typo*) dan menghapus karakter tersembunyi (seperti `\t`) pada data kategorikal.
    * Mendeteksi dan menangani *outlier* menggunakan metode **Interquartile Range (IQR)**.

4.  **Dimensionality Reduction (PCA)**
    * Mereduksi dimensi data menjadi **10 fitur numerik** dan **8 fitur kategorikal**.
    * Konfigurasi ini berhasil mempertahankan **91% variansi informasi** dari dataset asli.

## Sumber Data & Reproduksibilitas
Dataset diambil langsung dari **UCI Machine Learning Repository** menggunakan library `ucimlrepo`. Hal ini memastikan kode dapat dijalankan oleh siapa saja tanpa perlu mengunduh file CSV manual.

```python
from ucimlrepo import fetch_ucirepo
import pandas as pd

# Fetch dataset (ID 336: Chronic Kidney Disease)
chronic_kidney_disease = fetch_ucirepo(id=336)

# Extract features and targets
X = chronic_kidney_disease.data.features
y = chronic_kidney_disease.data.targets

# Combine into single DataFrame
Data = pd.concat([X, y], axis=1)
```

## Struktur Repository
- `Laporan.pdf`: laporan lengkap berisi landasan teori, analisis mendalam, dan interpretasi hasil.
- `main-notebook.ipynb`: source code berupa Jupyter Notebook yang berisi seluruh proses preprocessing dari awal hingga akhir.

## Penulis
**Ulivia Embun Tresna Wardani** 
*Fakultas Matematika dan Ilmu Pengetahuan Alam*
*Institut Teknologi Bandung (2025)*
