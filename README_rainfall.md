# Rainfall Classification in Pekanbaru Using SVM and ANN

Proyek mata kuliah **Statistical Machine Learning** ini membangun dan membandingkan model klasifikasi untuk mendeteksi apakah hujan akan terjadi pada satu jam berikutnya di Kota Pekanbaru, Indonesia.

## Ringkasan proyek

- **Sumber data:** Open-Meteo Historical Weather API
- **Lokasi:** Pekanbaru, Indonesia (latitude 0.5104°, longitude 101.4383°)
- **Periode pengamatan:** 18 Januari–18 Oktober 2026
- **Frekuensi:** per jam
- **Jumlah observasi:** 6.573
- **Prediktor:** 19 fitur meteorologis dan fitur hasil rekayasa
- **Target:** `target_hujan_next_1h` (0 = tidak hujan, 1 = hujan)
- **Ambang hujan:** curah hujan pada satu jam berikutnya ≥ 0,05 mm

## Alur dan metode

1. Mengambil data cuaca historis dari Open-Meteo.
2. Memeriksa dan membersihkan data.
3. Melakukan feature engineering, termasuk transformasi arah angin, riwayat hujan, dan waktu siklik.
4. Membagi data secara kronologis menjadi development set (80%) dan test set (20%).
5. Melakukan validasi berbasis waktu menggunakan 5-fold `TimeSeriesSplit`.
6. Membandingkan baseline, Support Vector Machine (SVM) dengan kernel RBF, dan Artificial Neural Network (ANN).
7. Memilih threshold berdasarkan prediksi out-of-fold pada development set.
8. Mengevaluasi model terpilih pada test set.

## Hasil utama pada test set

| Model | Accuracy | Balanced Accuracy | Precision (Hujan) | Recall (Hujan) | F2-score |
|---|---:|---:|---:|---:|---:|
| Baseline | 64,18% | 50,00% | 0,00% | 0,00% | 0,00% |
| SVM Balanced | 75,13% | 78,70% | 60,06% | 91,30% | 82,69% |
| ANN Unweighted | 73,31% | 77,28% | 58,11% | 91,30% | 81,94% |

SVM Balanced direkomendasikan berdasarkan F2-score yang lebih tinggi dan 24 false positive lebih sedikit dibandingkan ANN Unweighted. Kedua model memiliki recall hujan yang sama, yaitu 91,30%.

## Isi repository

- `SML_Web_Mining_Open_Meteo_Feature_Engineering.ipynb` — pengambilan data, preprocessing, dan feature engineering.
- `SML_SVM_ANN_Rain_Classification.ipynb` — pemodelan, validasi, threshold tuning, dan evaluasi.
- `dataset_klasifikasi_hujan_pekanbaru.csv` — dataset final untuk pemodelan.
- `SML_Presentation.pdf` — presentasi proyek.
- `visualizations/` — visualisasi hasil penelitian.
- `results/` — ringkasan metrik dan confusion matrix.
- `requirements.txt` — pustaka Python yang digunakan.

## Cara menjalankan

Notebook dirancang untuk dijalankan di **Google Colab**.

### Opsi 1 — Membuat ulang dataset
1. Buka notebook `SML_Web_Mining_Open_Meteo_Feature_Engineering.ipynb` di Google Colab.
2. Jalankan seluruh cell untuk mengambil data dari Open-Meteo dan membentuk dataset final.
3. Unduh atau simpan file `dataset_klasifikasi_hujan_pekanbaru.csv`.

### Opsi 2 — Menggunakan dataset yang disediakan
1. Buka notebook `SML_SVM_ANN_Rain_Classification.ipynb` di Google Colab.
2. Unggah `dataset_klasifikasi_hujan_pekanbaru.csv` ketika notebook meminta file dataset.
3. Pastikan nama file sesuai dengan nama yang dibaca notebook.
4. Jalankan cell secara berurutan.

Instalasi pustaka dapat dilakukan di lingkungan Python/Colab menggunakan:

```bash
pip install -r requirements.txt
```

## Keterbatasan

Penelitian menggunakan data cuaca historis dari satu wilayah dan periode pengamatan tertentu. Data ini belum merupakan pengujian prakiraan operasional real-time. Pengujian pada periode dan lokasi berbeda serta evaluasi menggunakan data prakiraan cuaca diperlukan sebelum model dipertimbangkan untuk penggunaan operasional.

## Sumber data

Open-Meteo Historical Weather API: https://open-meteo.com/en/docs/historical-weather-api

## Catatan

Proyek ini merupakan proyek akademik untuk mata kuliah Statistical Machine Learning. Hasil model tidak dimaksudkan sebagai layanan prakiraan cuaca operasional.
