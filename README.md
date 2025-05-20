# Proyek-Klasifikasi-Gambar : Vegetable Dataset
link dataset: https://www.kaggle.com/datasets/misrakahmed/vegetable-image-dataset

## Model Arsitektur
---
Model ini menggunakan Convolutional Neural Network (CNN) dengan beberapa layer konvolusi untuk ekstraksi fitur dari gambar, diikuti oleh layer fully connected untuk klasifikasi akhir.
- **Layer Konvolusi**:
  - **Conv2D (32 filter, kernel size (3, 3), fungsi aktivasi ReLU)**: Mengambil fitur dari gambar input.
  - **MaxPooling2D (pool size (2, 2))**: Downsampling untuk mengurangi dimensi fitur.
  - **Conv2D (64 filter, kernel size (3, 3), fungsi aktivasi ReLU)**: Ekstraksi fitur lebih lanjut.
  - **MaxPooling2D**: Downsampling lagi.
  - **Conv2D (128 filter, kernel size (3, 3), fungsi aktivasi ReLU)**: Ekstraksi fitur terakhir.
  - **MaxPooling2D**: Downsampling terakhir.
  
- **Layer Fully Connected**:
  - **Flatten**: Mengubah output menjadi vektor satu dimensi.
  - **Dense (128 unit, fungsi aktivasi ReLU)**: Layer fully connected dengan 128 unit.
  - **Dropout (0.5)**: Regularisasi untuk mengurangi overfitting.
  - **Dense (jumlah kelas, fungsi aktivasi Softmax)**: Layer output untuk klasifikasi multi-kelas, dengan jumlah kelas sesuai dengan `gen_train.num_classes`.
---

---
## Kompilasi Model:
- **Optimizer**: Adam dengan learning rate 0.001.
- **Loss Function**: Categorical crossentropy untuk klasifikasi multi-kelas.
- **Metrik**: Akurasi digunakan sebagai metrik evaluasi.
---

---
## Callback untuk Pelatihan:
- **EarlyStopping**: Pelatihan dihentikan jika **`val_loss`** tidak membaik selama 5 epoch berturut-turut dan bobot terbaik dipulihkan.
- **ReduceLROnPlateau**: Learning rate akan dikurangi sebesar **0.2** jika **`val_loss`** tidak membaik selama 3 epoch berturut-turut.
- **ModelCheckpoint**: Menyimpan model dengan **`val_accuracy`** tertinggi selama pelatihan.
---

---
## Pengaturan Pelatihan:
- **steps_per_epoch** dan **validation_steps** dihitung berdasarkan jumlah data dalam **generator training** dan **validation**, dengan **batch_size** yang sesuai.
- Model dilatih selama **32 epoch** dengan menggunakan generator untuk pelatihan dan validasi, serta callback yang telah disebutkan.
---

## Dataset
---
- Total gambar: ±8421 gambar
- Ukuran gambar: 512x512 piksel
- Format: `.jpg`
- Dataset sudah di split menjadi training, validation, dan testing dengan rasio 70,15,15.
---

## Hasil Pemodelan
---
Akurasi bisa disekitar 95 persen dan ini menunjukan hasil yang sangat baik.
---
