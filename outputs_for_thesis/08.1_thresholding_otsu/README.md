# Stage 08.1 - Ablation Thresholding: Otsu

Otsu *thresholding* (global, `cv2.THRESH_BINARY + cv2.THRESH_OTSU`)
diterapkan **menggantikan** tahap *black-hat* pada pipeline. Pipeline
lain identik -> perbandingan *apple-to-apple*.

**Rata-rata CER Otsu:** 12.25%
**Rata-rata CER BlackHat (default):** 7.51%
**Selisih:** +4.74% (Otsu lebih jelek)

## CER per Dokumen (24 dokumen)

| # | Dokumen | CER +BH | CER +Otsu | Delta |
|---|---|---:|---:|---:|
| 1 | ANYERLOR (Listrik).jpg | 0.11 | 0.54 | +0.43 |
| 2 | BANDARBARU (Listrik).pdf | 11.87 | 14.89 | +3.02 |
| 3 | BANDARBARU (Telpon).pdf | 0.69 | 0.92 | +0.23 |
| 4 | BATANGKUIS (Air Gas).pdf | 9.07 | 15.38 | +6.31 |
| 5 | BATANGKUIS (Telpon).pdf | 0.46 | 2.31 | +1.85 |
| 6 | DEMPET (Air Gas).png | 18.90 | 50.74 | +31.85 |
| 7 | JERUKLEGI (Listrik).jpg | 3.36 | 2.93 | -0.43 |
| 8 | LEGOK (Telpon).pdf | 1.22 | 1.90 | +0.68 |
| 9 | MANYAR (Listrik).pdf | 13.71 | 18.28 | +4.57 |
| 10 | MANYAR (Telpon).pdf | 26.74 | 21.68 | -5.06 |
| 11 | MEDANPAYAGELI (Air Gas).pdf | 13.15 | 16.72 | +3.58 |
| 12 | MEDANPAYAGELI (Listrik).pdf | 11.42 | 12.61 | +1.19 |
| 13 | MEDANPAYAGELI (Telpon).pdf | 0.23 | 1.15 | +0.92 |
| 14 | MUARATAE (Air Gas).png | 4.39 | 4.99 | +0.61 |
| 15 | NAMORAMBE (Air Gas).pdf | 12.87 | 58.25 | +45.38 |
| 16 | NAMORAMBE (Listrik).pdf | 7.97 | 14.21 | +6.24 |
| 17 | NAMORAMBE (Telpon).pdf | 0.69 | 1.39 | +0.69 |
| 18 | PANCAJAYA (Listrik).pdf | 14.38 | 14.48 | +0.11 |
| 19 | PANCURBATU (Listrik).pdf | 11.36 | 14.04 | +2.68 |
| 20 | PANCURBATU (Telpon).pdf | 0.46 | 1.16 | +0.69 |
| 21 | SEPATAN (Listrik).pdf | 3.27 | 4.17 | +0.89 |
| 22 | SINDANGKERTA (Telpon).jpg | 0.28 | 0.55 | +0.28 |
| 23 | SUKATANI (Air Gas).pdf | 3.14 | 7.00 | +3.86 |
| 24 | TOPOYO (Listrik).png | 10.62 | 13.65 | +3.03 |
