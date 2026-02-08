# Modul OCR - Sistem Verifikasi Dokumen Otomatis

Ekstraksi teks dari dokumen PDF/Gambar menggunakan **Tesseract OCR** untuk keperluan verifikasi dokumen otomatis.

Modul ini merupakan bagian dari pipeline **OCR + NER** untuk sistem verifikasi dokumen pos Indonesia.

---

## Alur Kerja (Pipeline)

```
Input PDF/Gambar
    |
    v
Konversi ke Gambar (300 DPI)
    |
    v
Orientation & Skew Correction
  - Deteksi rotasi via OSD
  - Fallback rotasi 180 via confidence check
  - Koreksi kemiringan (skew) via minAreaRect
    |
    v
Grayscaling
    |
    v
Adaptive Noise Removal
  - Gaussian 5x5 (noisy, >1500)
  - Gaussian 3x3 (moderate, >500)
  - No blur (clean, <=500)
    |
    v
[CLAHE, Sharpening, Thresholding, Morphology — dinonaktifkan]
    |
    v
Tesseract OCR (Grayscale, PSM 3, OEM 3)
    |
    v
Post-processing
  - Whitespace cleanup
  - Garbage line removal (watermark/stempel)
    |
    v
Output: List + JSON
    |
    v
Evaluasi (opsional): Similarity, WER, CER
```

---

## Konfigurasi Tesseract

| Parameter | Nilai | Keterangan |
|-----------|-------|------------|
| OEM | 3 | LSTM neural network engine |
| PSM | 3 | Fully automatic page segmentation |
| Bahasa | `ind+eng` | Indonesia + English |
| Input | Grayscale | LSTM lebih akurat pada grayscale dibanding binary |
| DPI | 300 | Resolusi konversi PDF |

---

## Post-processing: Garbage Line Removal

Menghapus baris-baris noise dari watermark, stempel, dan artefak visual menggunakan 3 kriteria:

1. **Baris sangat pendek** — 1-2 karakter yang bukan angka
2. **Rasio alfanumerik rendah** — kurang dari 40% dan panjang kurang dari 20 karakter
3. **Pola karakter tunggal terpisah** — lebih dari 60% kata hanya 1 karakter, panjang kurang dari 30

---

## Format Output

Hasil OCR tersedia dalam 2 format:

| Output | Tipe | Kapan Dipakai |
|--------|------|---------------|
| `ocr_results_list` | `list[dict]` | Jika OCR dan NER di notebook yang sama |
| `ocr_results.json` | File JSON | Jika OCR dan NER di notebook berbeda |

Struktur data:

```json
[
  {
    "document_name": "BANDARBARU (Listrik).pdf",
    "ocr_result": "PT POS INDONESIA (PERSERO)\nKantor Kpc..."
  }
]
```

| Field | Tipe | Keterangan |
|-------|------|------------|
| `document_name` | `string` | Nama file dokumen (termasuk ekstensi) |
| `ocr_result` | `string` | Teks lengkap hasil OCR |

---

## Metrik Evaluasi

Evaluasi dilakukan dalam mode **single-line** (semua whitespace di-normalize menjadi single space).

| Metrik | Library | Keterangan |
|--------|---------|------------|
| Raw Document Similarity | `SequenceMatcher` | Kesamaan keseluruhan (0-100%) |
| WER (Word Error Rate) | `jiwer` | Error level kata |
| CER (Character Error Rate) | `jiwer` | Error level karakter, paling relevan untuk verifikasi nominal |

### Benchmark CER

| CER | Kategori |
|-----|----------|
| ≤ 1% | Sangat Baik |
| 1-5% | Baik |
| 5-10% | Cukup |
| 10-20% | Perlu Perbaikan |
| > 20% | Kurang |

---

## Cara Pakai

### Prasyarat

- Python 3.x
- Tesseract OCR ([download](https://github.com/UB-Mannheim/tesseract/wiki))
- Poppler ([download](https://github.com/oschwartz10612/poppler-windows/releases))
- Tessdata bahasa Indonesia (`ind`)

### Langkah

1. Sesuaikan `TESSERACT_PATH` dan `POPPLER_PATH` di cell konfigurasi
2. Sesuaikan `DOCUMENTS_FOLDER` ke folder dokumen yang akan diproses
3. Sesuaikan `GROUND_TRUTH_FOLDER` ke folder file `.txt` ground truth (opsional)
4. Jalankan semua cell secara berurutan
5. Hasil OCR tersedia di `ocr_results_list` dan `ocr_results.json`

---

## Dependencies

| Package | Fungsi |
|---------|--------|
| `pytesseract` | Interface Python ke Tesseract OCR |
| `pdf2image` | Konversi PDF ke gambar |
| `Pillow` | Manipulasi gambar |
| `opencv-python` | Preprocessing gambar |
| `python-Levenshtein` | Perhitungan jarak edit |
| `jiwer` | Perhitungan WER dan CER |

---

## Catatan

- **CLAHE, Sharpening, Thresholding, dan Morphology dinonaktifkan** karena Tesseract LSTM (OEM 3) lebih akurat pada gambar grayscale dibanding binary.
- **Dokumen dengan watermark/stempel** cenderung memiliki CER lebih tinggi. Garbage line removal membantu mengurangi noise, tetapi tidak bisa menghilangkan sepenuhnya.
- **Dokumen digital bersih** (tanpa watermark) bisa mencapai CER kurang dari 1%.
## Version
1.0.1
1. Skip Preprocessing step CLAHE, THRESHOLDING, MORPHOLOGICAL OPERATIONS
2. Add clean garbage line
3. Add output OCR using List
4. Add time on each processing, start at conversion file to image.
