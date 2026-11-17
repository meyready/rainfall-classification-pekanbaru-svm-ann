# Rainfall Classification in Pekanbaru Using SVM and ANN

Proyek mata kuliah **Statistical Machine Learning** ini membangun dan membandingkan model klasifikasi untuk mendeteksi apakah hujan akan terjadi pada satu jam berikutnya di Kota Pekanbaru, Indonesia.

## Ringkasan Proyek

- **Sumber data:** Open-Meteo Historical Weather API
- **Lokasi:** Pekanbaru, Indonesia (latitude 0.5104°, longitude 101.4383°)
- **Periode pengamatan:** 18 Januari–18 Oktober 2026
- **Frekuensi:** Per jam
- **Jumlah observasi:** 6.573
- **Prediktor:** 19 fitur meteorologis dan fitur hasil rekayasa
- **Target:** `target_hujan_next_1h` (0 = tidak hujan, 1 = hujan)
- **Ambang hujan:** Curah hujan pada satu jam berikutnya ≥ 0,05 mm

## Alur dan Metode

1. Mengambil data cuaca historis dari Open-Meteo.
2. Memeriksa dan membersihkan data.
3. Melakukan feature engineering, termasuk transformasi arah angin, riwayat hujan, dan waktu siklik.
4. Membagi data secara kronologis menjadi development set (80%) dan test set (20%).
5. Melakukan validasi berbasis waktu menggunakan 5-fold `TimeSeriesSplit`.
6. Membandingkan baseline, Support Vector Machine (SVM) dengan kernel RBF, dan Artificial Neural Network (ANN).
7. Memilih threshold berdasarkan prediksi out-of-fold pada development set.
8. Mengevaluasi model terpilih pada test set.

## Hasil Evaluasi pada Test Set

| Model | Accuracy | Balanced Accuracy | Precision (Hujan) | Recall (Hujan) | F2-score |
|---|---:|---:|---:|---:|---:|
| Baseline | 64,18% | 50,00% | 0,00% | 0,00% | 0,00% |
| SVM Balanced | 75,13% | 78,70% | 60,06% | 91,30% | 82,69% |
| ANN Unweighted | 73,31% | 77,28% | 58,11% | 91,30% | 81,94% |

SVM Balanced direkomendasikan berdasarkan F2-score yang lebih tinggi dan 24 false positive lebih sedikit dibandingkan ANN Unweighted. Kedua model memiliki recall hujan yang sama, yaitu 91,30%.

## Isi Repository

- `SML_Web_Mining_Open_Meteo_Feature_Engineering.ipynb` — pengambilan data, preprocessing, dan feature engineering.
- `SML_SVM_ANN_Rain_Classification.ipynb` — pemodelan, validasi, threshold tuning, dan evaluasi.
- `dataset_klasifikasi_hujan_pekanbaru.csv` — dataset final untuk pemodelan.
- `SML_Presentation.pdf` — presentasi proyek.
- `visualisasi_uas_sml.zip` — kumpulan visualisasi hasil penelitian.
- `perbandingan_metrik_test.csv` — perbandingan metrik evaluasi.
- `perbandingan_confusion_matrix_test.csv` — hasil confusion matrix.
- `ringkasan_hasil_proyek.csv` — ringkasan hasil proyek.
- `requirements.txt` — pustaka Python yang digunakan.

## Cara Menjalankan

Notebook dirancang untuk dijalankan menggunakan **Google Colab**.

### 1. Membuat Dataset

1. Buka notebook `SML_Web_Mining_Open_Meteo_Feature_Engineering.ipynb` di Google Colab.
2. Jalankan cell secara berurutan untuk mengambil data dari Open-Meteo dan melakukan feature engineering.
3. Simpan dataset hasil pengolahan dengan nama `dataset_klasifikasi_hujan_pekanbaru.csv`.

### 2. Menjalankan Pemodelan

1. Buka notebook `SML_SVM_ANN_Rain_Classification.ipynb` di Google Colab.
2. Siapkan dataset `dataset_klasifikasi_hujan_pekanbaru.csv`.
3. Unggah dataset apabila notebook meminta file input.
4. Jalankan cell secara berurutan untuk melakukan pemodelan dan evaluasi.

Instalasi pustaka dapat dilakukan menggunakan:

```bash
pip install -r requirements.txt
```

## Keterbatasan

Penelitian menggunakan data cuaca historis dari satu wilayah dan periode pengamatan tertentu. Data ini belum merupakan pengujian prakiraan operasional real-time. Pengujian pada periode dan lokasi berbeda serta evaluasi menggunakan data prakiraan cuaca diperlukan sebelum model dipertimbangkan untuk penggunaan operasional.

## Sumber Data

[Open-Meteo Historical Weather API](https://open-meteo.com/en/docs/historical-weather-api)

## Catatan

Proyek ini merupakan proyek akademik untuk mata kuliah Statistical Machine Learning. Hasil model tidak dimaksudkan sebagai layanan prakiraan cuaca operasional.
