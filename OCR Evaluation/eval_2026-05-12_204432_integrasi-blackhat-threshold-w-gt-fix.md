# OCR Evaluation — integrasi-blackhat-threshold-w-gt-fix

**Timestamp:** 2026-05-12 20:44:32
**Tesseract:** 5.5.0.20241111
**Catatan:** hasil menunjukkan penurunan cer wer setelah dicek/diedit ulang gtnya, karena di gtnya ada yang salah sehingga perlu diperbaiki

## Ringkasan
| Metric | Value |
|---|---|
| Total dokumen | 42 |
| Avg WER | 13.75% |
| Avg CER | 6.93% |
| Avg waktu/dokumen | 2.63 s |

## Konfigurasi
**PSM per kategori:** `listrik=4`, `air=3`, `telepon=4`
**Preprocessing:** dpi=300, nlmeans_h=10, noise_threshold=1500, adaptive_block=31, adaptive_c=10

## Hasil per Dokumen
| # | File | Kategori | PSM | WER (%) | CER (%) | Total (s) |
|---|------|----------|-----|---------|---------|-----------|
| 1 | ANYERLOR (Listrik).jpg | listrik | 4 | 17.65 | 4.31 | 2.71 |
| 2 | BANDARBARU (Listrik).pdf | listrik | 4 | 21.74 | 14.99 | 5.68 |
| 3 | BANDARBARU (Telpon).pdf | telepon | 4 | 3.28 | 0.46 | 4.50 |
| 4 | BATANGKUIS (Air Gas).pdf | air | 3 | 21.32 | 12.97 | 5.63 |
| 5 | BATANGKUIS (Telpon).pdf | telepon | 4 | 8.20 | 1.39 | 4.58 |
| 6 | DEMPET (Air Gas).png | air | 3 | 53.66 | 22.72 | 2.67 |
| 7 | JERUKLEGI (Listrik).jpg | listrik | 4 | 64.71 | 28.96 | 2.02 |
| 8 | LEGOK (Telpon).pdf | telepon | 4 | 5.94 | 1.49 | 6.40 |
| 9 | MANYAR (Listrik).pdf | listrik | 4 | 23.21 | 16.13 | 4.02 |
| 10 | MANYAR (Telpon).pdf | telepon | 4 | 38.04 | 30.70 | 5.28 |
| 11 | MEDANPAYAGELI (Air Gas).pdf | air | 3 | 24.64 | 13.84 | 5.82 |
| 12 | MEDANPAYAGELI (Listrik).pdf | listrik | 4 | 16.06 | 11.21 | 6.05 |
| 13 | MEDANPAYAGELI (Telpon).pdf | telepon | 4 | 8.20 | 0.92 | 4.39 |
| 14 | MUARATAE (Air Gas).png | air | 3 | 65.57 | 26.78 | 1.77 |
| 15 | NAMORAMBE (Air Gas).pdf | air | 3 | 23.13 | 13.80 | 5.32 |
| 16 | NAMORAMBE (Listrik).pdf | listrik | 4 | 18.84 | 13.67 | 5.94 |
| 17 | NAMORAMBE (Telpon).pdf | telepon | 4 | 8.20 | 0.92 | 4.57 |
| 18 | PANCAJAYA (Listrik).pdf | listrik | 4 | 30.22 | 20.17 | 6.02 |
| 19 | PANCURBATU (Listrik).pdf | listrik | 4 | 19.71 | 12.54 | 5.96 |
| 20 | PANCURBATU (Telpon).pdf | telepon | 4 | 8.20 | 1.16 | 4.80 |
| 21 | SEPATAN (Listrik).pdf | listrik | 4 | 12.50 | 3.27 | 5.46 |
| 22 | SINDANGKERTA (Telpon).jpg | telepon | 4 | 17.35 | 4.16 | 2.48 |
| 23 | SUKATANI (Air Gas).pdf | air | 3 | 17.74 | 10.27 | 5.70 |
| 24 | TOPOYO (Listrik).png | listrik | 4 | 49.26 | 24.27 | 2.24 |
| 25 | CISOLOK (Air Gas).pdf | air | 3 | 0.00 | 0.00 | 0.03 |
| 26 | DANDER (Air Gas).pdf | air | 3 | 0.00 | 0.00 | 0.02 |
| 27 | DEMPET (Listrik).pdf | listrik | 4 | 0.00 | 0.00 | 0.03 |
| 28 | JATINEGARATEGAL (Air Gas).pdf | air | 3 | 0.00 | 0.00 | 0.04 |
| 29 | KAPAS (Listrik).pdf | listrik | 4 | 0.00 | 0.00 | 0.04 |
| 30 | KARANGANYARDEMAK (Telpon).pdf | telepon | 4 | 0.00 | 0.00 | 0.03 |
| 31 | MATAOMPANA (Air Gas).pdf | air | 3 | 0.00 | 0.00 | 0.03 |
| 32 | MUARAANCALONG (Air Gas).pdf | air | 3 | 0.00 | 0.00 | 0.03 |
| 33 | MUTING (Listrik).pdf | listrik | 4 | 0.00 | 0.00 | 0.03 |
| 34 | NAGRAK (Air Gas).pdf | air | 3 | 0.00 | 0.00 | 0.02 |
| 35 | NAGRAK (Listrik).pdf | listrik | 4 | 0.00 | 0.00 | 0.03 |
| 36 | PALANGGA (Listrik).pdf | listrik | 4 | 0.00 | 0.00 | 0.03 |
| 37 | PARUNGPANJANG (Air Gas).pdf | air | 3 | 0.00 | 0.00 | 0.04 |
| 38 | PARUNGPANJANG (Listrik).pdf | listrik | 4 | 0.00 | 0.00 | 0.03 |
| 39 | PENDAWANBARU (Listrik).pdf | listrik | 4 | 0.00 | 0.00 | 0.03 |
| 40 | TANAHMIRING (Listrik).pdf | listrik | 4 | 0.00 | 0.00 | 0.03 |
| 41 | WANCI (Listrik).pdf | listrik | 4 | 0.00 | 0.00 | 0.03 |
| 42 | WANCI (Telpon).pdf | telepon | 4 | 0.00 | 0.00 | 0.02 |