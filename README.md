# Modul OCR - Sistem Verifikasi Dokumen Otomatis

Ekstraksi teks dari dokumen PDF/Gambar menggunakan **Tesseract OCR** untuk keperluan verifikasi dokumen otomatis.

Modul ini merupakan bagian dari pipeline **OCR + NER** untuk sistem verifikasi dokumen pos Indonesia.

---

## Alur Kerja (Pipeline)

```
Input PDF/Gambar
    |
    v
Konversi ke Gambar (PDF_DPI)
    |
    v
Orientation & Skew Correction
  - Deteksi rotasi via OSD
  - Fallback rotasi 180° via confidence check
  - Koreksi kemiringan (skew) via minAreaRect
    |
    v
Grayscaling
    |
    v
Adaptive Noise Removal
  - NlMeans h=10 (JPG/foto fisik)
  - Gaussian 3x3 (PDF noise, varian Laplacian >1500)
  - Pass-through (PDF bersih, varian <=1500)
    |
    v
Thresholding
  - Adaptive Gaussian (JPG/foto fisik)
  - Pass-through (PDF — Tesseract LSTM lebih akurat pada grayscale)
    |
    v
Tesseract OCR (PSM dinamis per kategori, OEM 3, --dpi PDF_DPI)
    |
    v
Post-processing
  - Whitespace cleanup
  - Garbage line removal (watermark/stempel)
    |
    v
Output: List
    |
    v
Evaluasi (opsional): WER, CER — disimpan ke JSON/CSV/MD
```

---

## Konfigurasi Tesseract

| Parameter | Nilai | Keterangan |
|-----------|-------|------------|
| OEM | 3 | LSTM neural network engine |
| PSM | Dinamis per kategori | Lihat tabel PSM di bawah |
| Bahasa | `ind+eng` | Indonesia + English |
| Input | Grayscale (PDF) / Binary (JPG) | LSTM lebih akurat pada grayscale |
| `--dpi` | `PDF_DPI` (default 300) | Eksplisit agar LSTM tidak salah estimasi ukuran karakter |

### PSM per Kategori Dokumen

| Kategori | PSM | Alasan |
|----------|-----|--------|
| `listrik` | 4 | Single column — struk termal PLN |
| `air` | 3 | Fully automatic — layout bervariasi |
| `telepon` | 4 | Single column |
| *(lainnya)* | 4 | Default fallback |

Kategori dideteksi otomatis dari nama file via `detect_category()`.

---

## Konstanta Preprocessing

Semua nilai yang bisa dituning tersentralisasi di cell konfigurasi:

| Konstanta | Default | Keterangan |
|-----------|---------|------------|
| `PDF_DPI` | `300` | Resolusi konversi PDF & flag `--dpi` Tesseract |
| `NLMEANS_H` | `10` | Kekuatan filter `fastNlMeansDenoising` (JPG) |
| `NOISE_VARIANCE_THRESHOLD` | `1500` | Batas varian Laplacian untuk aktifkan Gaussian blur (PDF) |
| `ADAPTIVE_BLOCK_SIZE` | `31` | Ukuran block `adaptiveThreshold` (harus ganjil) |
| `ADAPTIVE_C` | `10` | Offset konstanta `adaptiveThreshold` |
| `OCR_MIN_ALNUM` | `100` | Batas minimum karakter alfanumerik sebelum fallback PSM |
| `GARBAGE_ALNUM_RATIO` | `0.4` | Rasio alfanumerik di bawah ini dianggap garbage |
| `GARBAGE_SINGLE_CHAR_RATIO` | `0.6` | Rasio kata satu-huruf di atas ini dianggap garbage |
| `OSD_MIN_CONFIDENCE` | `1.0` | Confidence OSD minimum agar rotasi diterapkan |
| `ROTATION_CONF_DIFF` | `10` | Selisih confidence untuk aktifkan fallback rotasi 180° |
| `SKEW_MIN_ANGLE` | `0.5` | Sudut minimum skew yang perlu dikoreksi (derajat) |
| `SKEW_MAX_ANGLE` | `15.0` | Sudut di atas ini diabaikan (kemungkinan deteksi salah) |

---

## Post-processing: Garbage Line Removal

Menghapus baris noise dari watermark, stempel, dan artefak visual menggunakan 4 kriteria:

1. **Baris sangat pendek** — 1-2 karakter yang bukan angka
2. **Rasio alfanumerik rendah** — di bawah `GARBAGE_ALNUM_RATIO` dan panjang kurang dari 20 karakter
3. **Pola karakter tunggal terpisah** — rasio kata satu-huruf di atas `GARBAGE_SINGLE_CHAR_RATIO`, panjang kurang dari 30
4. **Hanya simbol separator** — baris yang hanya berisi `|`, `-`, `=` tanpa teks bermakna

---

## Format Output

Hasil OCR disimpan di variabel `ocr_results_list`:

```python
[
  {
    "nama_lampiran": "BANDARBARU (Listrik).pdf",
    "hasil_ocr": "PT POS INDONESIA (PERSERO)\nKantor Kpc..."
  }
]
```

| Field | Tipe | Keterangan |
|-------|------|------------|
| `nama_lampiran` | `string` | Nama file dokumen (termasuk ekstensi) |
| `hasil_ocr` | `string` | Teks lengkap hasil OCR |

---

## Evaluasi & Penyimpanan Hasil

Evaluasi dilakukan dalam mode **single-line** (semua whitespace di-normalize menjadi single space).

| Metrik | Library | Keterangan |
|--------|---------|------------|
| WER (Word Error Rate) | `jiwer` | Error level kata |
| CER (Character Error Rate) | `jiwer` | Error level karakter, paling relevan untuk verifikasi nominal |

Hasil evaluasi otomatis disimpan ke folder `OCR Evaluation/` dalam 3 format:

| Format | Isi |
|--------|-----|
| `.json` | Record lengkap: config, timing per tahap, WER/CER per dokumen |
| `.csv` | Tabel per dokumen untuk analisis di spreadsheet |
| `.md` | Ringkasan siap copy ke Notion |

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
2. Sesuaikan `BASE_FOLDER` dan `CATEGORY` ke folder dokumen yang akan diproses
3. Sesuaikan `GROUND_TRUTH_FOLDER` ke folder file `.txt` ground truth (opsional)
4. Ubah nilai di `CATEGORY_PSM` jika ingin eksperimen PSM tanpa menyentuh kode lain
5. Jalankan semua cell secara berurutan
6. Hasil OCR tersedia di `ocr_results_list`

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

- **CLAHE, Sharpening, dan Morphology dinonaktifkan** karena Tesseract LSTM (OEM 3) lebih akurat pada gambar grayscale dibanding binary.
- **Thresholding hanya aktif untuk JPG** (foto fisik dengan pencahayaan tidak merata). PDF digital dilewatkan langsung ke Tesseract sebagai grayscale.
- **Flag `--dpi` eksplisit** mencegah LSTM salah estimasi ukuran karakter saat menerima numpy array (tanpa metadata resolusi).
- **Dokumen dengan watermark/stempel** cenderung memiliki CER lebih tinggi. Garbage line removal membantu, tetapi tidak bisa menghilangkan sepenuhnya.
- **Dokumen digital bersih** (tanpa watermark) bisa mencapai CER kurang dari 1%.

---

## Version

### v1.0.1
1. Decouple `PDF_DPI` sebagai konstanta — dipakai di konversi PDF dan flag `--dpi` Tesseract
2. PSM dinamis per kategori dokumen via `CATEGORY_PSM` dan `detect_category()`
3. Semua magic number preprocessing dipindah ke konstanta terpusat
4. Thresholding adaptive hanya untuk JPG; PDF pass-through grayscale
5. Noise removal disederhanakan: NlMeans (JPG), Gaussian 3x3 (PDF noisy), pass-through (PDF bersih)
6. Garbage line removal ditambah kriteria ke-4 (simbol separator)
7. Penyimpanan hasil evaluasi otomatis ke JSON, CSV, dan MD

### v1.0.0
1. Skip preprocessing CLAHE, Thresholding, Morphological Operations
2. Garbage line removal
3. Output OCR menggunakan List
4. Timing per tahap dimulai dari konversi file ke gambar
