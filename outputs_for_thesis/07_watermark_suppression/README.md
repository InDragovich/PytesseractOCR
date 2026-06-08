# Stage 07 - Watermark Suppression (Morfologi Black-Hat)

Penekanan watermark via ***morphological closing*** dengan kernel
besar. *Closing* mengisi *stroke* teks tipis namun mempertahankan
*watermark* besar. Selisih `background - gray` lalu di-*invert*
menjaga teks tetap gelap.

## Kernel Skala-Adaptif

| Sisi terpendek (px) | Kernel |
|---|---:|
| < 600       | 7 |
| 600 - 800   | 9 |
| 800 - 1000  | 15 |
| 1000 - 2000 | 25 |
| >= 2000     | 21 |

- `TOPHAT_RESIDUE_FLOOR = 25` (residu watermark lemah dihapus)

## Temuan: Dokumen yang Memburuk Setelah Black-Hat

Tidak setiap dokumen membaik dengan *preprocessing*. Berikut
**5 dokumen** dengan CER lebih tinggi setelah
pipeline+BlackHat dibanding baseline:

| Dokumen | CER baseline | CER +BH | Delta |
|---|---:|---:|---:|
| BANDARBARU (Telpon).pdf | 0.46% | 0.69% | +0.23 |
| DEMPET (Air Gas).png | 14.65% | 18.90% | +4.25 |
| MEDANPAYAGELI (Listrik).pdf | 11.21% | 11.42% | +0.22 |
| PANCAJAYA (Listrik).pdf | 10.73% | 14.38% | +3.65 |
| SEPATAN (Listrik).pdf | 2.83% | 3.27% | +0.45 |

**Catatan untuk Bab V:** dokumen di atas tidak dihapus dari evaluasi.
Justru menjadi bukti bahwa *preprocessing* tidak selalu meningkatkan
hasil OCR -- temuan ini diperlukan untuk analisis kasus per kasus
(mis. kualitas asli sudah baik, watermark minim, resolusi tinggi).
