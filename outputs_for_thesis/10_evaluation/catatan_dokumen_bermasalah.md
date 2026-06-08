# Catatan Dokumen Bermasalah

> **Catatan redaksi:** Citra contoh di bawah berasal dari folder
> `outputs_for_thesis/02_conversion/` dalam kondisi *un-redacted*.
> Sebelum dipasang di buku TA, **blur / hitamkan area dengan**
> **informasi pelanggan** (nama, NIK, alamat, nomor pelanggan).
> Area teks tagihan / nominal aman ditampilkan karena merupakan
> objek evaluasi OCR.

Analisis terkonsolidasi dokumen *worst-case* dan *best-case* pada
*pipeline* utama (BlackHat), untuk mendukung pembahasan **Bab V**
dan menjawab pertanyaan pembimbing *"pada kasus seperti apa hasil
OCR menurun?"*

*Sumber data:* `eval_2026-06-08_151216_bab5-konsolidasi-psm6-gtfix.json`  
*Total dokumen OCR dievaluasi:* **24**

## Ringkasan Status (toleransi ±1% CER absolut)

| Status | Jumlah | Definisi |
|---|---:|---|
| Membaik (preprocessing membantu) | 11 | ΔCER > +1% |
| Memburuk (preprocessing menurunkan) | 2 | ΔCER < −1% |
| Stabil (perbedaan tidak signifikan) | 11 | \|ΔCER\| ≤ 1% |

**Catatan:** 2/24 dokumen (8%) 
memburuk setelah *preprocessing*. Persentase ini ***penting***  
diakui di Bab V -- *preprocessing* tidak selalu meningkatkan hasil OCR.

## 1. Top 5 Worst-Case (CER Tertinggi Setelah Pipeline)

### 1. MANYAR (Telpon).pdf

![Citra asli MANYAR (Telpon)](../02_conversion/MANYAR (Telpon)_original.png)

- **Kategori:** telepon | **Format:** PDF | **Resolusi:** 2313x1439
- **Status:** membaik
- **CER per skenario:**
  - Baseline (raw): 30.70%
  - Pipeline + BlackHat: **26.74%** (default)
  - Pipeline + Otsu: 21.68%
  - Pipeline + AdaptiveGauss: 22.31%
  - **Winner pada dokumen ini:** Otsu
- **Word stats:** 64/92 kata benar, 18 hilang, 16 salah

**Dugaan penyebab:**

- 18 kata **hilang** -- watermark/blur menutupi atau token di-drop oleh confidence filter.
- Strategi terbaik untuk dokumen ini = **Otsu**, bukan BlackHat -- temuan menarik tapi tidak digunakan sebagai default karena BlackHat menang rata-rata.

### 2. DEMPET (Air Gas).png

![Citra asli DEMPET (Air Gas)](../02_conversion/DEMPET (Air Gas)_original.png)

- **Kategori:** air | **Format:** PNG | **Resolusi:** 895x550
- **Status:** memburuk
- **CER per skenario:**
  - Baseline (raw): 14.65%
  - Pipeline + BlackHat: **18.90%** (default)
  - Pipeline + Otsu: 50.74%
  - Pipeline + AdaptiveGauss: 22.08%
  - **Winner pada dokumen ini:** baseline
- **Word stats:** 51/82 kata benar, 5 hilang, 36 salah

**Dugaan penyebab:**

- Resolusi rendah (sisi terpendek 550px) -- adaptive resize diaktifkan, namun upscaling tidak menambah informasi nyata.
- Format gambar (bukan PDF) -- berasal dari foto/scan langsung; umumnya lebih bervariasi kualitasnya.
- Preprocessing **memperburuk** CER +4.25% absolut -- kandidat untuk pembahasan limitasi pipeline.
- 36 kata salah/insersi -- Tesseract membaca karakter mirip (mis. 0/O, 1/l/I) atau watermark masuk.
- Strategi terbaik untuk dokumen ini = **baseline**, bukan BlackHat -- temuan menarik tapi tidak digunakan sebagai default karena BlackHat menang rata-rata.

### 3. PANCAJAYA (Listrik).pdf

![Citra asli PANCAJAYA (Listrik)](../02_conversion/PANCAJAYA (Listrik)_original.png)

- **Kategori:** listrik | **Format:** PDF | **Resolusi:** 2550x3300
- **Status:** memburuk
- **CER per skenario:**
  - Baseline (raw): 10.73%
  - Pipeline + BlackHat: **14.38%** (default)
  - Pipeline + Otsu: 14.48%
  - Pipeline + AdaptiveGauss: 18.88%
  - **Winner pada dokumen ini:** baseline
- **Word stats:** 113/139 kata benar, 5 hilang, 25 salah

**Dugaan penyebab:**

- Resolusi tinggi (2550x3300) -- kualitas asli sudah baik, preprocessing berisiko menghapus detail teks tipis.
- Preprocessing **memperburuk** CER +3.65% absolut -- kandidat untuk pembahasan limitasi pipeline.
- 25 kata salah/insersi -- Tesseract membaca karakter mirip (mis. 0/O, 1/l/I) atau watermark masuk.
- Strategi terbaik untuk dokumen ini = **baseline**, bukan BlackHat -- temuan menarik tapi tidak digunakan sebagai default karena BlackHat menang rata-rata.

### 4. MANYAR (Listrik).pdf

![Citra asli MANYAR (Listrik)](../02_conversion/MANYAR (Listrik)_original.png)

- **Kategori:** listrik | **Format:** PDF | **Resolusi:** 1193x2298
- **Status:** membaik
- **CER per skenario:**
  - Baseline (raw): 18.68%
  - Pipeline + BlackHat: **13.71%** (default)
  - Pipeline + Otsu: 18.28%
  - Pipeline + AdaptiveGauss: 10.08%
  - **Winner pada dokumen ini:** AdpGauss
- **Word stats:** 90/112 kata benar, 7 hilang, 15 salah

**Dugaan penyebab:**

- 7 kata **hilang** -- watermark/blur menutupi atau token di-drop oleh confidence filter.
- Strategi terbaik untuk dokumen ini = **AdpGauss**, bukan BlackHat -- temuan menarik tapi tidak digunakan sebagai default karena BlackHat menang rata-rata.

### 5. MEDANPAYAGELI (Air Gas).pdf

![Citra asli MEDANPAYAGELI (Air Gas)](../02_conversion/MEDANPAYAGELI (Air Gas)_original.png)

- **Kategori:** air | **Format:** PDF | **Resolusi:** 2481x3508
- **Status:** stabil
- **CER per skenario:**
  - Baseline (raw): 13.73%
  - Pipeline + BlackHat: **13.15%** (default)
  - Pipeline + Otsu: 16.72%
  - Pipeline + AdaptiveGauss: 18.22%
  - **Winner pada dokumen ini:** BH
- **Word stats:** 110/138 kata benar, 8 hilang, 25 salah

**Dugaan penyebab:**

- Resolusi tinggi (2481x3508) -- kualitas asli sudah baik, preprocessing berisiko menghapus detail teks tipis.
- 8 kata **hilang** -- watermark/blur menutupi atau token di-drop oleh confidence filter.
- 25 kata salah/insersi -- Tesseract membaca karakter mirip (mis. 0/O, 1/l/I) atau watermark masuk.

## 2. Top 5 Best-Case (CER Terendah) -- sebagai pembanding

### 1. ANYERLOR (Listrik).jpg -- CER 0.11%

- **Kategori:** listrik | **Format:** JPG | **Resolusi:** 875x621
- **Status:** membaik
- **Word stats:** 136/137 kata benar

### 2. MEDANPAYAGELI (Telpon).pdf -- CER 0.23%

- **Kategori:** telepon | **Format:** PDF | **Resolusi:** 2481x3508
- **Status:** stabil
- **Word stats:** 60/61 kata benar

### 3. SINDANGKERTA (Telpon).jpg -- CER 0.28%

- **Kategori:** telepon | **Format:** JPG | **Resolusi:** 868x581
- **Status:** stabil
- **Word stats:** 96/98 kata benar

### 4. BATANGKUIS (Telpon).pdf -- CER 0.46%

- **Kategori:** telepon | **Format:** PDF | **Resolusi:** 2481x3508
- **Status:** stabil
- **Word stats:** 59/61 kata benar

### 5. PANCURBATU (Telpon).pdf -- CER 0.46%

- **Kategori:** telepon | **Format:** PDF | **Resolusi:** 2481x3508
- **Status:** stabil
- **Word stats:** 59/61 kata benar

## 3. Pola Lintas Outlier

### Distribusi Format File

| Format | Worst-5 | Best-5 | Total Korpus |
|---|---:|---:|---:|
| .jpg | 0 | 2 | 3 |
| .pdf | 4 | 3 | 18 |
| .png | 1 | 0 | 3 |

### Distribusi Kategori

| Kategori | Worst-5 | Best-5 | Total Korpus |
|---|---:|---:|---:|
| air | 2 | 0 | 6 |
| listrik | 2 | 1 | 10 |
| telepon | 1 | 4 | 8 |

### Observasi

- **Kategori air/gas** muncul lebih sering di *worst-case*, kemungkinan karena layout PDAM/POSPAY lebih bervariasi dengan watermark + tabel pembayaran yang padat.
- **Kategori telepon** umumnya stabil (banyak text-layer PDF yang sudah masuk jalur `pdftotext`); outlier yang muncul biasanya PDF Scan dengan kualitas rendah.
- **Resolusi sisi terpendek**: rata-rata *worst-5* = 1643px vs *best-5* = 1729px -- tidak ada korelasi yang kuat antara resolusi dan kesulitan OCR pada dataset ini.

## 4. Rekomendasi Pembahasan Bab V

1. **Tampilkan tabel status** (membaik/memburuk/stabil) sebagai bukti
   kejujuran evaluasi -- bukan memilih hanya yang menang.
2. **Bahas 3-5 worst-case** dengan dugaan penyebab konkret seperti di
   atas. Hindari kalimat generik *"kualitas dokumen rendah"*; gunakan
   karakteristik spesifik (resolusi, watermark, kategori).
3. **Jelaskan dokumen memburuk** sebagai limitasi *pipeline*, bukan
   kegagalan metodologi. Resolusi tinggi + tanpa *watermark* memang
   tidak butuh *preprocessing*; pipeline dirancang untuk kasus rata-
   rata, bukan setiap kasus.
4. **Konteks vote ablation**: BlackHat menang di 16/24 dokumen, bukan
   24/24. Itu cukup untuk menjadi *default*, namun ada ruang untuk
   *adaptive strategy* pada penelitian lanjutan (di luar scope TA).

## 5. Sumber Data untuk Reproduksi

- Bab V konsolidasi: `eval_2026-06-08_151216_bab5-konsolidasi-psm6-gtfix.json`
- Ablation thresholding: `eval_2026-06-08_151345_ablation-thresholding.json`
- File pendukung lain di `outputs_for_thesis/10_evaluation/`
