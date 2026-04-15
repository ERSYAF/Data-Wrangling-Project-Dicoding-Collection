# Data Wrangling Project: Dicoding Collection

## 📌 Deskripsi Proyek

Proyek ini merupakan latihan **data wrangling (pengolahan data)** menggunakan dataset dari **Dicoding Collection (DiCo)**, sebuah perusahaan fashion yang menjual produknya melalui platform online.

Dataset ini berisi histori transaksi penjualan beserta informasi terkait pelanggan, produk, dan pesanan. Tujuan utama dari proyek ini adalah untuk:

* Mengumpulkan data dari berbagai sumber
* Menilai kualitas data (data assessment)
* Membersihkan data (data cleaning)
* Mempersiapkan data untuk analisis lebih lanjut

---

## 🗂️ Struktur Dataset

Dataset terdiri dari 4 tabel utama:

### 1. **Customers**

Berisi informasi pelanggan:

* `customer_id`
* `customer_name`
* `gender`
* `age`
* `home_address`
* `zip_code`
* `city`
* `state`
* `country`

### 2. **Orders**

Berisi informasi pesanan:

* `order_id`
* `customer_id`
* `order_date`
* `delivery_date`

### 3. **Products**

Berisi informasi produk:

* `product_id`
* `product_type`
* `product_name`
* `size`
* `colour`
* `price`
* `quantity`
* `description`

### 4. **Sales**

Berisi detail transaksi:

* `sales_id`
* `order_id`
* `product_id`
* `price_per_unit`
* `quantity`
* `total_price`

---

## ⚙️ Teknologi yang Digunakan

Proyek ini menggunakan library Python berikut:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

---

## 🔄 Tahapan Proyek

### 1. 📥 Gathering Data

Data diambil langsung dari repository Dicoding menggunakan `pandas.read_csv()`:

```python
customers_df = pd.read_csv("https://raw.githubusercontent.com/dicodingacademy/dicoding_dataset/main/DicodingCollection/customers.csv")
orders_df = pd.read_csv("https://raw.githubusercontent.com/dicodingacademy/dicoding_dataset/main/DicodingCollection/orders.csv")
product_df = pd.read_csv("https://raw.githubusercontent.com/dicodingacademy/dicoding_dataset/main/DicodingCollection/products.csv")
sales_df = pd.read_csv("https://raw.githubusercontent.com/dicodingacademy/dicoding_dataset/main/DicodingCollection/sales.csv")
```

---

### 2. 🔍 Assessing Data (Penilaian Data)

Pada tahap ini dilakukan analisis kualitas data menggunakan:

* `.info()` → mengecek tipe data & jumlah data
* `.isna().sum()` → mendeteksi missing values
* `.duplicated().sum()` → mendeteksi duplikasi
* `.describe()` → statistik deskriptif

#### Temuan Masalah:

* **customers_df**

  * Missing value pada kolom `gender`
  * Terdapat data duplikat
  * Nilai tidak wajar pada kolom `age`

* **orders_df**

  * Tipe data `order_date` & `delivery_date` masih `object`

* **product_df**

  * Terdapat data duplikat

* **sales_df**

  * Missing value pada kolom `total_price`

---

### 3. 🧹 Cleaning Data (Pembersihan Data)

#### ✅ Customers

* Menghapus duplikasi:

```python
customers_df.drop_duplicates(inplace=True)
```

* Mengatasi missing value (`gender`) dengan **imputation**:

```python
customers_df.fillna(value="Prefer not to say", inplace=True)
```

* Memperbaiki nilai tidak wajar (`age`):

```python
customers_df.age.replace(customers_df.age.max(), 70, inplace=True)
customers_df.age.replace(customers_df.age.max(), 50, inplace=True)
```

---

#### ✅ Orders

* Mengubah tipe data ke datetime:

```python
datetime_columns = ["order_date", "delivery_date"]

for column in datetime_columns:
    orders_df[column] = pd.to_datetime(orders_df[column])
```

---

#### ✅ Products

* Menghapus data duplikat:

```python
product_df.drop_duplicates(inplace=True)
```

---

#### ✅ Sales

* Mengisi missing value pada `total_price`:

```python
sales_df["total_price"] = sales_df["price_per_unit"] * sales_df["quantity"]
```

---

## 📈 Hasil Akhir

Setelah proses data wrangling:

* Tidak ada missing values
* Tidak ada data duplikat
* Tipe data sudah sesuai
* Nilai data lebih akurat dan valid

Dataset siap digunakan untuk:

* Exploratory Data Analysis (EDA)
* Data Visualization
* Machine Learning
* Business Insight Analysis

---

## 🚀 Cara Menjalankan Proyek

1. Clone repository:

```bash
git clone https://github.com/username/repository-name.git
```

2. Install dependencies:

```bash
pip install numpy pandas matplotlib seaborn
```

3. Jalankan notebook / script Python

---

## 🎯 Tujuan Pembelajaran

Melalui proyek ini, kamu akan memahami:

* Konsep dasar data wrangling
* Cara menangani missing value
* Teknik menghapus duplikasi data
* Perbaikan tipe data
* Validasi dan pembersihan data

---

## ✨ Insight

Data yang bersih adalah fondasi utama dalam analisis data dan machine learning. Kesalahan kecil seperti missing value atau duplikasi dapat berdampak besar pada hasil analisis.

---


