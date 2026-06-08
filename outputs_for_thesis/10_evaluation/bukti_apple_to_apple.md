# Bukti Evaluasi Apple-to-Apple

Dokumen ini meringkas **kontrol variabel** pada seluruh skenario
evaluasi OCR sehingga perbandingan antar skenario dapat dipertanggung-
jawabkan sebagai *apple-to-apple* (instruksi pembimbing Bimbingan 6).

*Sumber data:* `eval_2026-06-08_151216_bab5-konsolidasi-psm6-gtfix.json` + `eval_2026-06-08_151345_ablation-thresholding.json`  
*Tesseract:* 5.5.0.20241111  
*Total dokumen OCR (in-scope):* **24**  
*Total dokumen text-layer (eksklusi):* **18**

## 1. Kontrol Variabel

Semua skenario berjalan dengan parameter berikut **identik**:

| Parameter | Nilai | Berlaku untuk |
|---|---|---|
| Dataset | 24 dokumen OCR (lihat daftar §2) | Semua skenario |
| *Ground truth* | File `.txt` di `dokumen_testing/ground_truth/` | Semua skenario |
| Tesseract engine | OEM 3 (LSTM) | Semua skenario |
| Bahasa OCR | `ind+eng` | Semua skenario |
| PSM per kategori | `listrik=4`, `air=3`, `telepon=4` | Semua skenario |
| Fallback PSM | 3 (otomatis bila alnum < 100) | Semua skenario |
| DPI PDF | 300 | Semua skenario |
| DPI gambar | 150 | Semua skenario |
| Mode evaluasi | *Single-line* (jiwer) | Semua skenario |
| Metrik | WER, CER, waktu pemrosesan | Semua skenario |

## 2. Variabel yang Berubah per Skenario

| Skenario | Yang berubah | Yang tetap |
|---|---|---|
| **Baseline** | Tanpa *preprocessing* sama sekali | Tesseract config, GT, dataset |
| **Pipeline + BlackHat** | Full *preprocessing* (orientasi, *grayscale*, *resize*, *denoise*, *black-hat*) | Tesseract config, GT, dataset |
| **Pipeline + Otsu** | Sama seperti BlackHat, hanya tahap *watermark suppression* diganti dengan Otsu *thresholding* | Tahap pipeline lain identik |
| **Pipeline + AdaptiveGauss** | Sama, tahap *watermark suppression* diganti `cv2.adaptiveThreshold` Gaussian | Tahap pipeline lain identik |

**Penegasan:** semua skenario menerima input dokumen yang sama,
diuji terhadap *ground truth* yang sama, dengan parameter pipeline
lain yang identik. Hanya satu variabel berubah per skenario.

## 3. Daftar 24 Dokumen OCR (Identik antar Skenario)

| # | Dokumen | Kategori | Format |
|---|---|---|---|
| 1 | ANYERLOR (Listrik).jpg | listrik | JPG |
| 2 | BANDARBARU (Listrik).pdf | listrik | PDF |
| 3 | BANDARBARU (Telpon).pdf | telepon | PDF |
| 4 | BATANGKUIS (Air Gas).pdf | air | PDF |
| 5 | BATANGKUIS (Telpon).pdf | telepon | PDF |
| 6 | DEMPET (Air Gas).png | air | PNG |
| 7 | JERUKLEGI (Listrik).jpg | listrik | JPG |
| 8 | LEGOK (Telpon).pdf | telepon | PDF |
| 9 | MANYAR (Listrik).pdf | listrik | PDF |
| 10 | MANYAR (Telpon).pdf | telepon | PDF |
| 11 | MEDANPAYAGELI (Air Gas).pdf | air | PDF |
| 12 | MEDANPAYAGELI (Listrik).pdf | listrik | PDF |
| 13 | MEDANPAYAGELI (Telpon).pdf | telepon | PDF |
| 14 | MUARATAE (Air Gas).png | air | PNG |
| 15 | NAMORAMBE (Air Gas).pdf | air | PDF |
| 16 | NAMORAMBE (Listrik).pdf | listrik | PDF |
| 17 | NAMORAMBE (Telpon).pdf | telepon | PDF |
| 18 | PANCAJAYA (Listrik).pdf | listrik | PDF |
| 19 | PANCURBATU (Listrik).pdf | listrik | PDF |
| 20 | PANCURBATU (Telpon).pdf | telepon | PDF |
| 21 | SEPATAN (Listrik).pdf | listrik | PDF |
| 22 | SINDANGKERTA (Telpon).jpg | telepon | JPG |
| 23 | SUKATANI (Air Gas).pdf | air | PDF |
| 24 | TOPOYO (Listrik).png | listrik | PNG |

## 4. Cross-Reference: Dokumen × Skenario

Setiap dokumen diuji pada **keempat skenario** -- tidak ada *cherry-
picking* per dokumen.

| # | Dokumen | Baseline | +BH | +Otsu | +AdpGauss |
|---|---|:-:|:-:|:-:|:-:|
| 1 | ANYERLOR (Listrik).jpg | ✓ | ✓ | ✓ | ✓ |
| 2 | BANDARBARU (Listrik).pdf | ✓ | ✓ | ✓ | ✓ |
| 3 | BANDARBARU (Telpon).pdf | ✓ | ✓ | ✓ | ✓ |
| 4 | BATANGKUIS (Air Gas).pdf | ✓ | ✓ | ✓ | ✓ |
| 5 | BATANGKUIS (Telpon).pdf | ✓ | ✓ | ✓ | ✓ |
| 6 | DEMPET (Air Gas).png | ✓ | ✓ | ✓ | ✓ |
| 7 | JERUKLEGI (Listrik).jpg | ✓ | ✓ | ✓ | ✓ |
| 8 | LEGOK (Telpon).pdf | ✓ | ✓ | ✓ | ✓ |
| 9 | MANYAR (Listrik).pdf | ✓ | ✓ | ✓ | ✓ |
| 10 | MANYAR (Telpon).pdf | ✓ | ✓ | ✓ | ✓ |
| 11 | MEDANPAYAGELI (Air Gas).pdf | ✓ | ✓ | ✓ | ✓ |
| 12 | MEDANPAYAGELI (Listrik).pdf | ✓ | ✓ | ✓ | ✓ |
| 13 | MEDANPAYAGELI (Telpon).pdf | ✓ | ✓ | ✓ | ✓ |
| 14 | MUARATAE (Air Gas).png | ✓ | ✓ | ✓ | ✓ |
| 15 | NAMORAMBE (Air Gas).pdf | ✓ | ✓ | ✓ | ✓ |
| 16 | NAMORAMBE (Listrik).pdf | ✓ | ✓ | ✓ | ✓ |
| 17 | NAMORAMBE (Telpon).pdf | ✓ | ✓ | ✓ | ✓ |
| 18 | PANCAJAYA (Listrik).pdf | ✓ | ✓ | ✓ | ✓ |
| 19 | PANCURBATU (Listrik).pdf | ✓ | ✓ | ✓ | ✓ |
| 20 | PANCURBATU (Telpon).pdf | ✓ | ✓ | ✓ | ✓ |
| 21 | SEPATAN (Listrik).pdf | ✓ | ✓ | ✓ | ✓ |
| 22 | SINDANGKERTA (Telpon).jpg | ✓ | ✓ | ✓ | ✓ |
| 23 | SUKATANI (Air Gas).pdf | ✓ | ✓ | ✓ | ✓ |
| 24 | TOPOYO (Listrik).png | ✓ | ✓ | ✓ | ✓ |

## 5. Eksklusi: 18 Dokumen PDF Digital (Text-Layer)

Dokumen PDF dengan *text layer* diekstrak via `pdftotext` (Poppler),
**tidak melalui Tesseract**. WER/CER ekstraksi ini ~0% karena teks
diambil langsung dari struktur PDF, bukan dari piksel citra.

Eksklusi dilakukan agar **rata-rata WER/CER OCR tidak terdilusi**
oleh skor-0 dari jalur non-OCR. Mencampurkan keduanya akan membuat
rata-rata menyesatkan dan tidak mencerminkan performa OCR-citra
sebenarnya (instruksi pembimbing).

## 6. Reproduksibilitas

- Seluruh hasil tersimpan dengan *timestamp* di `OCR Evaluation/`.
- Konfigurasi pipeline terpusat di Cell 5 notebook (sentralisasi path).
- File JSON menyimpan parameter eksperimen untuk audit.
- Rerun notebook menghasilkan angka konsisten (varians <1% antar
  run karena overhead I/O, bukan algoritma).
