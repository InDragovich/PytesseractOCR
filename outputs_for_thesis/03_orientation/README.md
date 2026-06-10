# Stage 03 - Koreksi Orientasi

Deteksi orientasi menggunakan **Tesseract OSD**. Jika *confidence*
> `OSD_MIN_CONFIDENCE = 2.0` dan sudut bukan 0 deg,
citra diputar. Bila OSD ragu, *fallback* membandingkan *confidence*
OCR antara orientasi normal dan 180 deg pada crop tengah citra.

## Ringkasan Keputusan (24 dokumen)

| # | Dokumen | Sudut | Conf | Source | Diputar |
|---|---|---:|---:|---|---|
| 1 | ANYERLOR (Listrik).jpg | 180 | 0.8 | - | tidak |
| 2 | BANDARBARU (Listrik).pdf | 180 | 0.1 | - | tidak |
| 3 | BANDARBARU (Telpon).pdf | 0 | 5.3 | - | tidak |
| 4 | BATANGKUIS (Air Gas).pdf | 0 | 3.3 | - | tidak |
| 5 | BATANGKUIS (Telpon).pdf | 0 | 7.5 | - | tidak |
| 6 | DEMPET (Air Gas).png | 0 | 5.5 | - | tidak |
| 7 | JERUKLEGI (Listrik).jpg | 0 | 0.0 | - | tidak |
| 8 | LEGOK (Telpon).pdf | 270 | 5.2 | OSD | ya |
| 9 | MANYAR (Listrik).pdf | 270 | 4.0 | OSD | ya |
| 10 | MANYAR (Telpon).pdf | 0 | 10.4 | - | tidak |
| 11 | MEDANPAYAGELI (Air Gas).pdf | 0 | 0.2 | - | tidak |
| 12 | MEDANPAYAGELI (Listrik).pdf | 0 | 2.9 | - | tidak |
| 13 | MEDANPAYAGELI (Telpon).pdf | 0 | 5.8 | - | tidak |
| 14 | MUARATAE (Air Gas).png | 0 | 0.0 | - | tidak |
| 15 | NAMORAMBE (Air Gas).pdf | 0 | 1.1 | - | tidak |
| 16 | NAMORAMBE (Listrik).pdf | 0 | 2.7 | - | tidak |
| 17 | NAMORAMBE (Telpon).pdf | 0 | 5.2 | - | tidak |
| 18 | PANCAJAYA (Listrik).pdf | 0 | 5.1 | - | tidak |
| 19 | PANCURBATU (Listrik).pdf | 0 | 2.1 | - | tidak |
| 20 | PANCURBATU (Telpon).pdf | 0 | 3.4 | - | tidak |
| 21 | SEPATAN (Listrik).pdf | 270 | 4.6 | OSD | ya |
| 22 | SINDANGKERTA (Telpon).jpg | 0 | 1.9 | - | tidak |
| 23 | SUKATANI (Air Gas).pdf | 0 | 4.0 | - | tidak |
| 24 | TOPOYO (Listrik).png | 0 | 0.1 | - | tidak |
