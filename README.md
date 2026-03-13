# 📈 Timeseries Modelling - Auto ARIMA Forecasting
**Timeseries Modelling | Machine Learning Bootcamp - Dibimbing.id**

**Author:** Lhedya Monica Ismon

---

## 🎯 Objective
Sebagai Data Scientist, melakukan analisis dan pemodelan data timeseries 
penjualan bulanan menggunakan Auto ARIMA untuk memprediksi nilai penjualan 
24 bulan ke depan, dengan menganalisis trend, seasonality, decomposition, 
dan stationarity data terlebih dahulu.

---

## 🗃️ Dataset
| Info | Detail |
|------|--------|
| Nama Dataset | a10.csv — Monthly Sales Dataset |
| Sumber | GitHub selva86/datasets (repositori publik) |
| Periode | Januari 1991 – Juni 2008 (17 tahun) |
| Frekuensi | Bulanan (12 data per tahun) |
| Kolom | date (bulan-tahun), value (nilai penjualan bulanan) |
| Tools | Google Colab, Python |

---

## 📋 Analysis Steps
1. Load dataset & data understanding
2. EDA — trend, seasonality, decomposition, ACF/PACF
3. ADF Test — cek stationarity & tipe data
4. Transformation method (log + differencing)
5. Train/test split (80/20)
6. Auto ARIMA modelling & prediction
7. Evaluasi model (MAE, MSE, MAPE)
8. Future prediction 24 bulan ke depan

---

## 📊 Hasil EDA

| Komponen | Hasil |
|----------|-------|
| **Trend** | Tren naik positif konsisten dari 1991–2008 |
| **Seasonality** | Pola musiman 12 bulan — puncak akhir tahun, lembah awal tahun |
| **Decomposition** | Multiplicative — amplitudo musiman meningkat seiring tren |
| **ACF/PACF** | Puncak signifikan di lag 12, 24, 36 — periode musiman = 12 bulan |

---

## 🔬 ADF Test - Stationarity Check

| Kondisi | ADF Statistic | p-value | Kesimpulan |
|---------|--------------|---------|------------|
| Sebelum Transformasi | Sangat tinggi | 1.0 (> 0.05) | Tidak Stasioner |
| Setelah Transformasi | Negatif (kecil) | < 0.05 | Stasioner |

**Transformation Method:**
1. **Log Transformation** — menstabilkan varians yang terus membesar (sifat multiplicative)
2. **Differencing** — menghilangkan tren naik jangka panjang

---

## 🤖 Model Auto ARIMA

| Parameter | Nilai |
|-----------|-------|
| Tipe Model | SARIMA (Seasonal ARIMA) via pmdarima |
| Periode Musiman | m = 12 bulan |
| Train/Test Split | 80% train / 20% test |
| Parameter p, q | 0 sampai 5 (auto search) |
| Differencing d | 1 (tetap, sudah di-differencing manual) |
| Seasonal D | 1, m = 12 |
| stepwise | True (efisiensi pencarian) |
| n_fits | Maks 50 model |

---

## 📈 Evaluasi Model

| Metrik | Train | Test | Interpretasi |
|--------|-------|------|-------------|
| **MAE** | 0.054 | 0.097 | Kesalahan rata-rata sangat kecil |
| **MSE** | 0.0098 | 0.0126 | Error besar jarang terjadi |
| **MAPE** | 1.37% | 1.93% | Model meleset hanya ~1.93% |

---

## 💡 Kesimpulan

**Trend & Seasonality:**
Data penjualan bulanan menunjukkan tren naik positif yang konsisten sejak 
1991 hingga 2008 dengan pola musiman 12 bulan yang jelas — puncak di akhir 
tahun dan lembah di awal tahun. Amplitudo musiman yang terus membesar 
membuktikan data bersifat multiplicative, bukan additive.

**Stationarity:**
Sebelum transformasi, data tidak stasioner (p-value = 1.0). Setelah 
diterapkan log transformation dan differencing, data berhasil menjadi 
stasioner (p-value < 0.05) dan siap dimodelkan dengan Auto ARIMA.

**Model Terbaik:**
Auto ARIMA (SARIMA) adalah model terbaik untuk dataset ini karena berhasil 
menangkap tren naik jangka panjang dan pola musiman 12 bulan secara otomatis. 
Dengan MAPE test hanya 1.93%, model ini sangat akurat untuk forecasting 
industri. Tidak terjadi overfitting — performa train (1.37%) dan test (1.93%) 
sangat konsisten.

**Future Prediction (24 Bulan):**
Model memprediksi tren penjualan terus meningkat dengan pola musiman tahunan 
yang terjaga. Fluktuasi musiman semakin besar seiring tren — sesuai sifat 
multiplicative data. Hasil prediksi disimpan di future_predictions.xlsx dan 
model disimpan di full_arima_model.pkl.

---

## ✅ Kelebihan Model
- MAPE test 1.93% — akurasi sangat tinggi untuk data timeseries nyata
- Tidak overfitting — performa train dan test sangat konsisten
- Auto ARIMA berhasil menangkap komponen musiman 12 bulan secara otomatis
- Pipeline transformasi (log + diff) berhasil mengubah data non-stasioner
- Model tersimpan sebagai .pkl — siap dipakai tanpa melatih ulang

## ⚠️ Keterbatasan Model
- ARIMA bersifat linear — kurang optimal untuk pola non-linear kompleks
- Belum ada visualisasi confidence interval pada prediksi
- Belum dibandingkan dengan model lain seperti ETS atau Prophet
- Data univariate — bisa ditingkatkan dengan fitur eksternal

---

## 💼 Business Impact

| Area | Manfaat |
|------|---------|
| **Manajemen Stok** | Antisipasi stok sesuai prediksi musiman — tidak berlebihan/kekurangan |
| **Perencanaan Produksi** | Jadwal kapasitas lebih efisien 24 bulan ke depan |
| **Strategi Promosi** | Kampanye tepat waktu menjelang puncak musiman akhir tahun |
| **Perencanaan Anggaran** | Proyeksi revenue lebih akurat untuk target bisnis |
| **Output Siap Pakai** | future_predictions.xlsx & full_arima_model.pkl tersedia langsung |

---

## 🔧 Tools & Libraries
\`\`\`python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from statsmodels.tsa.stattools import adfuller
from statsmodels.tsa.seasonal import seasonal_decompose
from pmdarima import auto_arima
from sklearn.metrics import mean_absolute_error, mean_squared_error
import joblib
\`\`\`

---

## 📁 File Structure
- \`notebook/\` — Google Colab (.ipynb)
- \`screenshots/\` — Visualisasi trend, decomposition, forecast
- \`portfolio/\` — Dokumentasi lengkap (.docx)

---

*Lhedya Monica Ismon | Machine Learning Bootcamp | Dibimbing.id*