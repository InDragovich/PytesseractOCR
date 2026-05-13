# OCR Evaluation — testing-preprocessing-metho-with-pdfbypass

**Timestamp:** 2026-05-11 01:39:49
**Tesseract:** 5.5.0.20241111
**Catatan:** terdapat perubahan hasi cer dan wer pada pdf scan, pdf text dipass

## Ringkasan
| Metric | Value |
|---|---|
| Total dokumen | 42 |
| Avg WER | 17.02% |
| Avg CER | 10.19% |
| Avg waktu/dokumen | 2.30 s |

## Konfigurasi
**PSM per kategori:** `listrik=4`, `air=3`, `telepon=4`
**Preprocessing:** dpi=300, nlmeans_h=10, noise_threshold=1500, adaptive_block=31, adaptive_c=10

## Hasil per Dokumen
| # | File | Kategori | PSM | WER (%) | CER (%) | Total (s) |
|---|------|----------|-----|---------|---------|-----------|
| 1 | ANYERLOR (Listrik).jpg | listrik | 4 | 28.57 | 8.22 | 2.59 |
| 2 | BANDARBARU (Listrik).pdf | listrik | 4 | 23.19 | 15.62 | 5.41 |
| 3 | BANDARBARU (Telpon).pdf | telepon | 4 | 3.28 | 0.46 | 4.00 |
| 4 | BATANGKUIS (Air Gas).pdf | air | 3 | 27.27 | 15.05 | 5.03 |
| 5 | BATANGKUIS (Telpon).pdf | telepon | 4 | 8.20 | 1.39 | 3.87 |
| 6 | DEMPET (Air Gas).png | air | 3 | 60.47 | 24.74 | 2.48 |
| 7 | JERUKLEGI (Listrik).jpg | listrik | 4 | 61.76 | 30.88 | 1.78 |
| 8 | LEGOK (Telpon).pdf | telepon | 4 | 6.93 | 1.63 | 5.64 |
| 9 | MANYAR (Listrik).pdf | listrik | 4 | 37.50 | 33.23 | 3.49 |
| 10 | MANYAR (Telpon).pdf | telepon | 4 | 45.36 | 33.44 | 4.02 |
| 11 | MEDANPAYAGELI (Air Gas).pdf | air | 3 | 31.11 | 17.57 | 4.95 |
| 12 | MEDANPAYAGELI (Listrik).pdf | listrik | 4 | 19.71 | 11.84 | 5.30 |
| 13 | MEDANPAYAGELI (Telpon).pdf | telepon | 4 | 9.84 | 1.16 | 3.80 |
| 14 | MUARATAE (Air Gas).png | air | 3 | 90.16 | 84.11 | 1.63 |
| 15 | NAMORAMBE (Air Gas).pdf | air | 3 | 28.68 | 16.43 | 4.79 |
| 16 | NAMORAMBE (Listrik).pdf | listrik | 4 | 18.71 | 13.52 | 5.14 |
| 17 | NAMORAMBE (Telpon).pdf | telepon | 4 | 8.20 | 1.39 | 4.03 |
| 18 | PANCAJAYA (Listrik).pdf | listrik | 4 | 64.76 | 47.47 | 5.15 |
| 19 | PANCURBATU (Listrik).pdf | listrik | 4 | 19.71 | 12.75 | 5.07 |
| 20 | PANCURBATU (Telpon).pdf | telepon | 4 | 8.20 | 1.16 | 4.21 |
| 21 | SEPATAN (Listrik).pdf | listrik | 4 | 12.50 | 3.27 | 4.71 |
| 22 | SINDANGKERTA (Telpon).jpg | telepon | 4 | 37.76 | 15.91 | 2.29 |
| 23 | SUKATANI (Air Gas).pdf | air | 3 | 18.33 | 10.70 | 4.80 |
| 24 | TOPOYO (Listrik).png | listrik | 4 | 44.85 | 26.19 | 1.92 |
| 25 | CISOLOK (Air Gas).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |
| 26 | DANDER (Air Gas).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |
| 27 | DEMPET (Listrik).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |
| 28 | JATINEGARATEGAL (Air Gas).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |
| 29 | KAPAS (Listrik).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |
| 30 | KARANGANYARDEMAK (Telpon).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |
| 31 | MATAOMPANA (Air Gas).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |
| 32 | MUARAANCALONG (Air Gas).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |
| 33 | MUTING (Listrik).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |
| 34 | NAGRAK (Air Gas).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |
| 35 | NAGRAK (Listrik).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |
| 36 | PALANGGA (Listrik).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |
| 37 | PARUNGPANJANG (Air Gas).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |
| 38 | PARUNGPANJANG (Listrik).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |
| 39 | PENDAWANBARU (Listrik).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |
| 40 | TANAHMIRING (Listrik).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |
| 41 | WANCI (Listrik).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |
| 42 | WANCI (Telpon).pdf | unknown | 4 | 0.00 | 0.00 | 0.03 |