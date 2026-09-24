# PM_P4 — Preprocessing & Feature Engineering

Pertemuan 4: **Preprocessing & Feature Engineering**.

## Ringkasan Praktikum

Notebook mengolah dataset karyawan buatan (10 baris) yang sengaja mengandung nilai hilang, kolom kategorikal, dan skala fitur yang berbeda. Tahapan yang dilakukan:

1. **Menangani nilai hilang** — imputasi median pada kolom `usia` dan `pendapatan`.
2. **Memisahkan fitur (X) dan label (y)** — label `membeli` dipisah dari fitur lainnya.
3. **Encoding kategorikal**
   - `pendidikan` (ordinal: SMA < S1 < S2) → label encoding.
   - `kota` (nominal) → one-hot encoding.
4. **Split data latih/uji** — dilakukan **sebelum** scaling untuk mencegah data leakage.
5. **Penskalaan fitur** — `StandardScaler` di-*fit* pada data latih, lalu diterapkan ke data latih & uji.
6. **Verifikasi akhir** — memastikan tidak ada nilai hilang, seluruh kolom numerik, dan skala seragam.

## Latihan Mandiri

- Perbandingan imputasi **median vs mean** pada kolom `usia`.
- Penerapan **MinMaxScaler** sebagai alternatif `StandardScaler`.
- Penambahan kolom kategorikal baru (`status_pernikahan`) dengan one-hot encoding.
- Penjelasan alasan `fit_transform` hanya dilakukan pada data latih, sedangkan data uji hanya `transform`.

## Refleksi

- Pentingnya urutan **split dulu, baru scaling** untuk mencegah data leakage.
- Kapan menggunakan **label encoding** (data ordinal) vs **one-hot encoding** (data nominal).
- Perbedaan **normalisasi** (MinMaxScaler, rentang 0–1) dan **standardisasi** (StandardScaler, mean 0 & std 1).

## Temuan

Saat mengerjakan Latihan Mandiri No. 1 (perbandingan imputasi median vs mean), ditemukan bahwa menghitung mean/median langsung dari `df` yang sudah diimputasi di Langkah 1 menghasilkan perbandingan yang tidak valid (kolom `usia` sudah tidak punya nilai hilang lagi). Perbaikannya: hitung mean & median dari salinan data **mentah** (`pd.DataFrame(data)`, sebelum imputasi Langkah 1), sehingga perbandingan antara imputasi median (35.0) dan mean (≈36.13) benar-benar terlihat pada baris yang tadinya kosong.
