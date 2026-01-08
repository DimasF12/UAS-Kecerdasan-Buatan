# 📧 Email Spam Detection System

Sistem klasifikasi teks otomatis berbasis **Machine Learning** untuk mendeteksi email **Spam** dan **Ham** menggunakan algoritma **Gradient Boosting Classifier**.

---

## 📌 Deskripsi Proyek

Proyek ini membangun pipeline analisis data **end-to-end**, mulai dari pembersihan teks mentah hingga evaluasi model prediktif.  
Dataset yang digunakan berasal dari **Enron Email Dataset**, yang berisi arsip email historis dengan berbagai pola komunikasi bisnis dan promosi.

Tujuan utama proyek ini adalah:
- Mengklasifikasikan email sebagai **Spam** atau **Ham**
- Menghasilkan model dengan akurasi tinggi
- Mengekstraksi insight dari fitur teks yang paling berpengaruh

---

## 🚀 Alur Kerja Sistem (Pipeline)

### 1️⃣ Preprocessing Data (Cleaning)

Tahapan pembersihan teks dilakukan untuk mengurangi *noise* dan meningkatkan kualitas fitur:

- **Header Stripping**  
  Menghapus prefiks seperti `Subject:` agar model fokus pada isi pesan.
- **Lowercasing**  
  Mengubah seluruh teks menjadi huruf kecil.
- **Character Removal**  
  Menghapus karakter kontrol (`\r`, `\n`), angka, dan tanda baca.
- **Space Normalization**  
  Menghilangkan spasi ganda agar tokenisasi lebih konsisten.

---

### 2️⃣ Ekstraksi Fitur (Feature Engineering)

Menggunakan **TF-IDF Vectorization** dengan parameter:

- `max_features = 2500`  
  Memilih 2.500 kata paling informatif.
- `stop_words = 'english'`  
  Menghapus kata umum seperti *the, is, at*, dan sejenisnya.

---

### 3️⃣ Pemodelan (Modeling)

Model yang digunakan adalah **Gradient Boosting Classifier** dengan konfigurasi:

- **Number of Estimators**: `150`
- **Learning Rate**: `0.1`
- **Max Depth**: `5`

Konfigurasi ini menjaga keseimbangan antara performa model dan risiko overfitting.

---

### 4️⃣ Evaluasi Model

Evaluasi dilakukan menggunakan **20% data uji** yang tidak pernah dilihat sebelumnya.

**Hasil Evaluasi:**
- **Accuracy**: ~97%
- **Spam Recall**: ~99%

Model memiliki sensitivitas tinggi dalam mendeteksi email spam.

---

## 📊 Hasil Analisis Fitur (Insights)

Berdasarkan **feature importance**, indikator utama yang diidentifikasi model adalah:

### 🔴 Indikator Spam
- `http`
- `click`
- `remove`
- `money`

### 🟢 Indikator Ham
- `enron`
- `hpl`
- `attached`
- `thanks`

---

## ⚠️ Catatan Teknis (Data Leakage)

Terdapat indikasi **data leakage** akibat dominansi kata **"enron"** pada kelas Ham.

**Rekomendasi:**
- Lakukan filter atau masking nama organisasi
- Gunakan dataset tambahan agar model lebih general untuk email non-Enron

---

## 🛠️ Persyaratan Sistem

- **Python**: 3.8+
- **Library**:
  - pandas
  - numpy
  - scikit-learn
  - matplotlib
  - seaborn

Instalasi dependencies:
```bash
pip install pandas numpy scikit-learn matplotlib seaborn
