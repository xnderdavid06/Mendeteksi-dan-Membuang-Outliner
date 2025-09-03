# Mendeteksi-dan-Membuang-Outliner

# 📊 Data Preprocessing: Deteksi & Pembersihan Outlier dengan IQR

Repository ini berisi langkah-langkah **data preprocessing** pada dataset (contoh: `data_set.csv`) untuk:
1. Membaca dataset
2. Inspeksi awal (cek struktur, missing values, statistik deskriptif)
3. Identifikasi kolom numerik
4. Deteksi & pembersihan outlier dengan metode **IQR**
5. Simpan dataset bersih ke file `data_bersih.xlsx`
6. Visualisasi sebelum & sesudah pembersihan

---

## 🚀 Cara Menjalankan di Google Colab

### → 1. Import library
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
