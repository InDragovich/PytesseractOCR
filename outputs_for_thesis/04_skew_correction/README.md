# Stage 04 - Koreksi Kemiringan (Skew)

Sudut kemiringan dicari dengan ***projection profile*** -- untuk
setiap sudut kandidat di `[-SKEW_MAX_ANGLE, +SKEW_MAX_ANGLE]` step
0.5 deg, rotasi citra biner lalu hitung *variance* jumlah piksel per
baris. Sudut dengan *variance* tertinggi = teks paling horizontal.

- `SKEW_MIN_ANGLE = 1.0`
- `SKEW_MAX_ANGLE = 15.0`

## Ringkasan (1/24 dokumen dikoreksi)

| # | Dokumen | Skew (deg) | Dikoreksi |
|---|---|---:|---|
| 1 | ANYERLOR (Listrik).jpg | 0.00 | tidak |
| 2 | BANDARBARU (Listrik).pdf | 0.00 | tidak |
| 3 | BANDARBARU (Telpon).pdf | 0.00 | tidak |
| 4 | BATANGKUIS (Air Gas).pdf | 0.00 | tidak |
| 5 | BATANGKUIS (Telpon).pdf | 0.00 | tidak |
| 6 | DEMPET (Air Gas).png | -1.00 | ya |
| 7 | JERUKLEGI (Listrik).jpg | 0.00 | tidak |
| 8 | LEGOK (Telpon).pdf | 0.00 | tidak |
| 9 | MANYAR (Listrik).pdf | 0.00 | tidak |
| 10 | MANYAR (Telpon).pdf | 0.00 | tidak |
| 11 | MEDANPAYAGELI (Air Gas).pdf | 0.00 | tidak |
| 12 | MEDANPAYAGELI (Listrik).pdf | 0.00 | tidak |
| 13 | MEDANPAYAGELI (Telpon).pdf | 0.00 | tidak |
| 14 | MUARATAE (Air Gas).png | 0.00 | tidak |
| 15 | NAMORAMBE (Air Gas).pdf | 0.00 | tidak |
| 16 | NAMORAMBE (Listrik).pdf | 0.00 | tidak |
| 17 | NAMORAMBE (Telpon).pdf | 0.00 | tidak |
| 18 | PANCAJAYA (Listrik).pdf | 0.00 | tidak |
| 19 | PANCURBATU (Listrik).pdf | 0.00 | tidak |
| 20 | PANCURBATU (Telpon).pdf | 0.00 | tidak |
| 21 | SEPATAN (Listrik).pdf | 0.00 | tidak |
| 22 | SINDANGKERTA (Telpon).jpg | 0.00 | tidak |
| 23 | SUKATANI (Air Gas).pdf | 0.00 | tidak |
| 24 | TOPOYO (Listrik).png | 0.00 | tidak |
