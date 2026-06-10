# Stage 08.2 - Ablation Thresholding: Adaptive Gaussian

`cv2.adaptiveThreshold` mode `ADAPTIVE_THRESH_GAUSSIAN_C`,
menggantikan tahap *black-hat*.

- `ADAPTIVE_BLOCK_SIZE = 31`
- `ADAPTIVE_C = 10`

**Rata-rata CER:** 10.53%
**vs BlackHat:** +3.02%

## CER per Dokumen

| # | Dokumen | CER +BH | CER +AdpGauss | Delta |
|---|---|---:|---:|---:|
| 1 | ANYERLOR (Listrik).jpg | 0.11 | 2.16 | +2.05 |
| 2 | BANDARBARU (Listrik).pdf | 11.87 | 18.12 | +6.26 |
| 3 | BANDARBARU (Telpon).pdf | 0.69 | 0.46 | -0.23 |
| 4 | BATANGKUIS (Air Gas).pdf | 9.07 | 9.18 | +0.11 |
| 5 | BATANGKUIS (Telpon).pdf | 0.46 | 0.69 | +0.23 |
| 6 | DEMPET (Air Gas).png | 18.90 | 22.08 | +3.18 |
| 7 | JERUKLEGI (Listrik).jpg | 3.36 | 6.51 | +3.15 |
| 8 | LEGOK (Telpon).pdf | 1.22 | 2.58 | +1.36 |
| 9 | MANYAR (Listrik).pdf | 13.71 | 10.08 | -3.63 |
| 10 | MANYAR (Telpon).pdf | 26.74 | 22.31 | -4.43 |
| 11 | MEDANPAYAGELI (Air Gas).pdf | 13.15 | 18.22 | +5.07 |
| 12 | MEDANPAYAGELI (Listrik).pdf | 11.42 | 14.76 | +3.34 |
| 13 | MEDANPAYAGELI (Telpon).pdf | 0.23 | 0.46 | +0.23 |
| 14 | MUARATAE (Air Gas).png | 4.39 | 8.93 | +4.54 |
| 15 | NAMORAMBE (Air Gas).pdf | 12.87 | 20.35 | +7.49 |
| 16 | NAMORAMBE (Listrik).pdf | 7.97 | 18.30 | +10.33 |
| 17 | NAMORAMBE (Telpon).pdf | 0.69 | 0.92 | +0.23 |
| 18 | PANCAJAYA (Listrik).pdf | 14.38 | 18.88 | +4.51 |
| 19 | PANCURBATU (Listrik).pdf | 11.36 | 18.33 | +6.97 |
| 20 | PANCURBATU (Telpon).pdf | 0.46 | 1.16 | +0.69 |
| 21 | SEPATAN (Listrik).pdf | 3.27 | 5.51 | +2.23 |
| 22 | SINDANGKERTA (Telpon).jpg | 0.28 | 5.40 | +5.12 |
| 23 | SUKATANI (Air Gas).pdf | 3.14 | 15.10 | +11.96 |
| 24 | TOPOYO (Listrik).png | 10.62 | 12.13 | +1.52 |
