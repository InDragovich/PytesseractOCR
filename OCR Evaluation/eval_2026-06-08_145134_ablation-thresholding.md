# Ablation Thresholding (2026-06-08_145134)

*Timestamp:* 2026-06-08_145134  
*Total dokumen OCR (apple-to-apple):* 24

## Ringkasan Akurasi & Waktu (4 Skenario)

| Skenario | Avg WER (%) | Avg CER (%) | Avg Waktu (s) |
|---|---:|---:|---:|
| Baseline (raw) | 19.53 | 9.89 | 1.70 |
| Pipeline + BlackHat | 15.31 | 7.51 | 7.61 |
| Pipeline + Otsu | 23.14 | 12.25 | 7.46 |
| Pipeline + AdaptiveGauss | 23.45 | 10.53 | 7.61 |

## Vote per Strategi (Dokumen dengan CER Terendah)

| Strategi | Vote |
|---|---:|
| Baseline (raw) | 5/24 |
| Pipeline + BlackHat | 16/24 |
| Pipeline + Otsu | 2/24 |
| Pipeline + AdaptiveGauss | 1/24 |

## Detail CER per Dokumen

| # | Dokumen | Baseline | +BH | +Otsu | +AdpGauss | Winner |
|---|---|---:|---:|---:|---:|---|
| 1 | ANYERLOR (Listrik).jpg | 1.40 | 0.11 | 0.54 | 2.16 | **+BH** |
| 2 | BANDARBARU (Listrik).pdf | 14.78 | 11.87 | 14.89 | 18.12 | **+BH** |
| 3 | BANDARBARU (Telpon).pdf | 0.46 | 0.69 | 0.92 | 0.46 | **raw** |
| 4 | BATANGKUIS (Air Gas).pdf | 13.09 | 9.07 | 15.38 | 9.18 | **+BH** |
| 5 | BATANGKUIS (Telpon).pdf | 0.92 | 0.46 | 2.31 | 0.69 | **+BH** |
| 6 | DEMPET (Air Gas).png | 14.65 | 18.90 | 50.74 | 22.08 | **raw** |
| 7 | JERUKLEGI (Listrik).jpg | 13.77 | 3.36 | 2.93 | 6.51 | **+Otsu** |
| 8 | LEGOK (Telpon).pdf | 1.36 | 1.22 | 1.90 | 2.58 | **+BH** |
| 9 | MANYAR (Listrik).pdf | 18.68 | 13.71 | 18.28 | 10.08 | **+AdpGauss** |
| 10 | MANYAR (Telpon).pdf | 30.70 | 26.74 | 21.68 | 22.31 | **+Otsu** |
| 11 | MEDANPAYAGELI (Air Gas).pdf | 13.73 | 13.15 | 16.72 | 18.22 | **+BH** |
| 12 | MEDANPAYAGELI (Listrik).pdf | 11.21 | 11.42 | 12.61 | 14.76 | **raw** |
| 13 | MEDANPAYAGELI (Telpon).pdf | 0.92 | 0.23 | 1.15 | 0.46 | **+BH** |
| 14 | MUARATAE (Air Gas).png | 20.88 | 4.39 | 4.99 | 8.93 | **+BH** |
| 15 | NAMORAMBE (Air Gas).pdf | 13.80 | 12.87 | 58.25 | 20.35 | **+BH** |
| 16 | NAMORAMBE (Listrik).pdf | 13.67 | 7.97 | 14.21 | 18.30 | **+BH** |
| 17 | NAMORAMBE (Telpon).pdf | 0.92 | 0.69 | 1.39 | 0.92 | **+BH** |
| 18 | PANCAJAYA (Listrik).pdf | 10.73 | 14.38 | 14.48 | 18.88 | **raw** |
| 19 | PANCURBATU (Listrik).pdf | 12.54 | 11.36 | 14.04 | 18.33 | **+BH** |
| 20 | PANCURBATU (Telpon).pdf | 0.93 | 0.46 | 1.16 | 1.16 | **+BH** |
| 21 | SEPATAN (Listrik).pdf | 2.83 | 3.27 | 4.17 | 5.51 | **raw** |
| 22 | SINDANGKERTA (Telpon).jpg | 1.11 | 0.28 | 0.55 | 5.40 | **+BH** |
| 23 | SUKATANI (Air Gas).pdf | 8.09 | 3.14 | 7.00 | 15.10 | **+BH** |
| 24 | TOPOYO (Listrik).png | 16.25 | 10.62 | 13.65 | 12.13 | **+BH** |

## Parameter

- `adaptive_block_size = 31`
- `adaptive_c = 10`

## Interpretasi

- Pipeline + BlackHat menang baik secara rata-rata WER/CER maupun
  vote per-dokumen.
- Otsu dan Adaptive Gaussian *thresholding* menambah error karena
  binarisasi keras menghapus detail teks tipis dan menebalkan derau
  watermark pada dokumen struk POSPAY.
- Tabel ini berfungsi sebagai justifikasi empiris pemilihan
  BlackHat (tanpa binarisasi keras) di *pipeline* utama.
