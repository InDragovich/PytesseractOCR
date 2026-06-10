# Output Dokumentasi untuk Buku Tugas Akhir

Folder ini berisi *artifact* terorganisir per tahap *pipeline* OCR,
siap dipakai sebagai bahan **Bab IV** (alur proses) dan **Bab V**
(evaluasi & analisis).

## Struktur

- `01_input_summary/` -- Ringkasan dokumen input
- `02_conversion/` -- Konversi PDF/gambar -> citra
- `03_orientation/` -- Koreksi orientasi (OSD)
- `04_skew_correction/` -- Koreksi kemiringan (projection profile)
- `05_grayscale/` -- Konversi grayscale
- `06_denoising/` -- Denoising (bilateral)
- `07_watermark_suppression/` -- Watermark suppression (black-hat)
- `08.1_thresholding_otsu/` -- Ablation: Otsu
- `08.2_thresholding_adaptive/` -- Ablation: Adaptive Gaussian
- `09_ocr_text/` -- Teks hasil OCR
- `10_evaluation/` -- Evaluasi (CER, WER, waktu)

## Catatan Pemakaian

- Tidak setiap PNG perlu masuk buku -- pilih contoh paling representatif.
- File `README.md` per stage berisi narasi singkat siap dipakai sebagai
  bahan tulisan; sesuaikan gaya bahasa dengan buku Anda.
- File evaluasi penuh ada di `10_evaluation/` (JSON + CSV + MD).
- Bila ada data sensitif pada teks OCR, lakukan penyensoran manual
  sebelum memasukkan ke buku.

## Dokumen Representatif (untuk contoh visual)

- ANYERLOR (Listrik).jpg
- DEMPET (Air Gas).png
- MANYAR (Telpon).pdf
- MUARATAE (Air Gas).png
