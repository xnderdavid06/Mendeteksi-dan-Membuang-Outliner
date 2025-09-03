📊 Eksplorasi & Pembersihan Outlier dengan Metode IQR


1. Import library
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

2. Baca dataset

# Ganti "data_set.csv" dengan nama file dataset kamu
df = pd.read_csv("data_set.csv")

3. Inspeksi awal

print("=== Info dataset ===")
print(df.info())

print("\n=== Contoh data awal ===")
print(df.head())

print("\n=== Descriptive statistics ===")
print(df.describe())

print("\n=== Jumlah nilai kosong tiap kolom ===")
print(df.isnull().sum())

4. Identifikasi kolom numerik

num_cols = df.select_dtypes(include=[np.number]).columns.tolist()
print("\n=== Kolom numerik ===")
print(num_cols)

5. Deteksi & pembersihan outlier dengan IQR

def remove_outliers_iqr(data, cols):
    df_clean = data.copy()
    for col in cols:
        Q1 = df_clean[col].quantile(0.25)
        Q3 = df_clean[col].quantile(0.75)
        IQR = Q3 - Q1
        lower = Q1 - 1.5 * IQR
        upper = Q3 + 1.5 * IQR
        df_clean = df_clean[(df_clean[col] >= lower) & (df_clean[col] <= upper)]
    return df_clean

df_clean = remove_outliers_iqr(df, num_cols)

print(f"\nUkuran sebelum: {df.shape}, sesudah: {df_clean.shape}")


6. Simpan dataset bersih

df_clean.to_excel("data_bersih.xlsx", index=False)
print("\n✅ Dataset bersih disimpan sebagai data_bersih.xlsx")

7. Visualisasi Boxplot sebelum & sesudah pembersihan

for col in num_cols:
    plt.figure(figsize=(10,5))
    
    # Boxplot sebelum
    plt.subplot(1,2,1)
    sns.boxplot(y=df[col])
    plt.title(f"Before - {col}")
    
    # Boxplot sesudah
    plt.subplot(1,2,2)
    sns.boxplot(y=df_clean[col])
    plt.title(f"After - {col}")
    
    plt.tight_layout()
    plt.show()
