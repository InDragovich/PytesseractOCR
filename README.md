# Modul OCR - Sistem Verifikasi Dokumen Otomatis

Ekstraksi teks dari dokumen PDF/Gambar menggunakan **Tesseract OCR** untuk keperluan verifikasi dokumen otomatis.

Modul ini merupakan bagian dari pipeline **OCR + NER** untuk sistem verifikasi dokumen pos Indonesia.

---

## Alur Kerja (Pipeline)

```
Input PDF/Gambar
    |
    v
1. Konversi ke Gambar (PDF_DPI)
    |
    v
2. Orientasi (OSD)
   - Deteksi rotasi 90°-step via pytesseract.image_to_osd
   - Fallback 180° via confidence comparison (normal vs rotated)
    |
    v
3. Kemiringan (Skew)
   - Projection profile (variance baris piksel)
   - Murni OpenCV (tanpa Tesseract) — overhead minimal
    |
    v
4. Grayscale (RGB → 1-channel)
    |
    v
5. Resize (adaptive upscale)
   - Probe tinggi karakter via Tesseract image_to_data
   - Upscale bila median tinggi karakter < MIN_CHAR_HEIGHT_PX
    |
    v
6. Denoise (bilateral filter)
   - Edge-preserving (Tomasi & Manduchi 1998)
   - Stroke teks dipertahankan, speckle background dihilangkan
    |
    v
7. Morfologi Black Top-Hat
   - Tekan watermark/background gradual
   - Kernel skala-adaptif berdasarkan sisi terpendek gambar
    |
    v
8. Binarisasi Otsu (global)
   - Distribusi intensitas hasil Black Top-Hat mendekati bimodal
    |
    v
9. Tesseract OCR (PSM dinamis per kategori, OEM 3, --dpi PDF_DPI)
    |
    v
Post-processing
  - Whitespace cleanup
  - Garbage line removal (watermark/stempel)
    |
    v
Output: List of dict {nama_lampiran, hasil_ocr}
    |
    v
Evaluasi: WER, CER (single-line mode) → JSON / CSV / MD
```

Setiap stage mencatat waktu per dokumen ke `timing_per_doc` (9 kolom terpisah) untuk analisis trade-off.

---

## Konfigurasi Tesseract

| Parameter | Konstanta | Nilai Default | Keterangan |
|-----------|-----------|---------------|------------|
| OEM | `TESSERACT_OEM` | `3` | LSTM + legacy fallback (default Tesseract 5) |
| Bahasa utama | `TESSERACT_LANG` | `"ind+eng"` | Indonesia + English (untuk istilah teknis) |
| Bahasa probe | `TESSERACT_LANG_PROBE` | `"ind"` | Probe estimasi tinggi karakter (lebih cepat) |
| PSM utama | `CATEGORY_PSM` | Dinamis per kategori | Lihat tabel PSM di bawah |
| PSM probe (Resize) | `RESIZE_PROBE_PSM` | `6` | Uniform block of text |
| PSM fallback (OSD) | `OSD_FALLBACK_PSM` | `6` | Bila `image_to_osd` gagal |
| PSM default | `PSM_DEFAULT` | `3` | Fully automatic — kategori tak dikenal |
| `--dpi` | `PDF_DPI` / `IMAGE_DPI` | `300` / `150` | Eksplisit agar LSTM tidak salah estimasi ukuran |

### PSM per Kategori Dokumen

| Kategori | PSM | Alasan |
|----------|-----|--------|
| `listrik` | 4 | Single column — struk termal PLN |
| `air` | 3 | Fully automatic — layout bervariasi (1-2 kolom) |
| `telepon` | 4 | Single column |
| *(lainnya)* | 3 (`PSM_DEFAULT`) | Default fallback |

Kategori dideteksi otomatis dari nama file via `detect_category()`.

---

## Konstanta Preprocessing

Semua nilai yang bisa dituning tersentralisasi di **satu cell konfigurasi** di atas notebook, dikelompokkan per subseksi.

### Resize (adaptive upscale)

| Konstanta | Default | Keterangan |
|-----------|---------|------------|
| `TARGET_CHAR_HEIGHT_PX` | `30` | Target tinggi karakter setelah upscale |
| `MIN_CHAR_HEIGHT_PX` | `25` | Ambang minimum — di bawah ini → resize |
| `H_CHAR_MARGINAL_MIN` | `15` | Batas bawah marginal (Laplacian check) |
| `MAX_UPSCALE_FACTOR` | `3.0` | Faktor upscale maksimum |
| `RESIZE_PROBE_CONF_MIN` | `40` | Confidence minimum untuk masuk perhitungan median |
| `HIGH_LAP_VAR_THRESHOLD` | `1000.0` | Skip resize bila citra sudah tajam (varian Laplacian tinggi) |

### Denoise (bilateral filter — Tomasi & Manduchi 1998)

| Konstanta | Default | Keterangan |
|-----------|---------|------------|
| `BILATERAL_DIAMETER` | `5` | Diameter neighborhood |
| `BILATERAL_SIGMA_COLOR` | `50` | Sigma di domain warna |
| `BILATERAL_SIGMA_SPACE` | `50` | Sigma di domain spasial |

### Morfologi Black Top-Hat (kernel skala-adaptif)

| Konstanta | Default | Range citra |
|-----------|---------|-------------|
| `TOPHAT_KERNEL_XS` | `7` | sisi terpendek < 600 px |
| `TOPHAT_KERNEL_SM` | `9` | 600 ≤ sisi terpendek < 800 |
| `TOPHAT_KERNEL_MIN` | `15` | 800 ≤ sisi terpendek < 1000 |
| `TOPHAT_KERNEL_MID` | `25` | 1000 ≤ sisi terpendek < 2000 |
| `TOPHAT_KERNEL_MAX` | `21` | sisi terpendek ≥ 2000 px |
| `TOPHAT_ENABLE_BIMOD_MAX` | `0.70` | Threshold bimodalitas untuk aktifkan top-hat |
| `TOPHAT_RESIDUE_FLOOR` | `25` | Residu minimum agar top-hat dilanjutkan |

### Orientasi & Kemiringan

| Konstanta | Default | Keterangan |
|-----------|---------|------------|
| `OSD_MIN_CONFIDENCE` | `2.0` | Confidence OSD minimum agar rotasi diterapkan |
| `ROTATION_CONF_DIFF` | `10` | Selisih confidence untuk aktifkan fallback rotasi 180° |
| `SKEW_MIN_ANGLE` | `1.0` | Sudut minimum skew yang perlu dikoreksi (°) |
| `SKEW_MAX_ANGLE` | `15.0` | Sudut di atas ini diabaikan |

### OCR & Garbage Detection

| Konstanta | Default | Keterangan |
|-----------|---------|------------|
| `OCR_MIN_ALNUM` | `100` | Batas minimum karakter alfanumerik sebelum fallback PSM |
| `OCR_TOKEN_CONF_MIN` | `50` | Confidence minimum token agar tidak dibuang |
| `OCR_CHAR_BLACKLIST` | `frozenset(...)` | Karakter di-scrub universal ($, @, mata uang asing, simbol legal) |
| `GARBAGE_ALNUM_RATIO` | `0.4` | Rasio alfanumerik di bawah ini → garbage |
| `GARBAGE_SINGLE_CHAR_RATIO` | `0.6` | Rasio kata satu-huruf di atas ini → garbage |
| `PDF_DIGITAL_TEXT_THRESHOLD` | `50` | Jumlah karakter minimum di PDF agar dianggap PDF Digital |

---

## Klasifikasi Grup Dokumen

Dokumen di-klasifikasi otomatis berdasarkan format file:

| Grup | Konstanta | Penanganan |
|------|-----------|------------|
| **PDF Digital** | `GROUP_PDF_DIGITAL` | Ekstrak teks langsung via `pdftotext` (tidak butuh OCR) |
| **PDF Scan** | `GROUP_PDF_SCAN` | Full OCR pipeline |
| **Gambar JPG/PNG** | `GROUP_IMAGE` | Full OCR pipeline |

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
| `.json` | Record lengkap: config, timing per tahap (9 kolom), WER/CER per dokumen |
| `.csv` | Tabel per dokumen untuk analisis di spreadsheet |
| `.md` | Ringkasan siap copy ke Notion |

### Breakdown Waktu (9 Stage)

`timing_per_doc[<nama_file>]` mencatat:

```
Konversi | OSD | Skew | Grayscale | Resize | Denoise | BlackHat | Otsu | Ekstraksi
```

`TOTAL = sum(values)`. Memudahkan analisis trade-off di Bab V (misal: OSD ~80× lebih lambat dari Skew karena panggil Tesseract).

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
- Tesseract OCR 5+ ([download](https://github.com/UB-Mannheim/tesseract/wiki))
- Poppler ([download](https://github.com/oschwartz10612/poppler-windows/releases))
- Tessdata bahasa Indonesia (`ind`) dan English (`eng`)

### Langkah

1. Sesuaikan `TESSERACT_PATH` dan `POPPLER_PATH` di cell instalasi (paling atas)
2. Sesuaikan `BASE_FOLDER` dan `DOCUMENTS_FOLDER` ke folder dokumen yang akan diproses
3. Sesuaikan `GROUND_TRUTH_FOLDER` ke folder file `.txt` ground truth (opsional)
4. Ubah nilai konstanta di cell konfigurasi bila ingin eksperimen tanpa menyentuh kode lain
5. **Restart kernel & Run All Cells** secara berurutan
6. Hasil OCR tersedia di `ocr_results_list`, evaluasi di `OCR Evaluation/`

---

## Dependencies

| Package | Fungsi |
|---------|--------|
| `pytesseract` | Interface Python ke Tesseract OCR |
| `pdf2image` | Konversi PDF ke gambar |
| `Pillow` | Manipulasi gambar |
| `opencv-python` | Preprocessing gambar (grayscale, bilateral, morfologi, Otsu) |
| `numpy` | Operasi array citra |
| `python-Levenshtein` | Perhitungan jarak edit |
| `jiwer` | Perhitungan WER dan CER |

---

## Catatan Desain

- **Tesseract LSTM (OEM 3)** menerima citra hasil binarisasi Otsu di tahap 8. Black Top-Hat (tahap 7) menormalkan distribusi intensitas sehingga Otsu mendapatkan threshold yang bersih.
- **Skew correction murni OpenCV** (projection profile) — tidak panggil Tesseract → overhead ~0.03s vs OSD ~2.3s.
- **Resize berbasis probe Tesseract** menambah 1 panggilan `image_to_data` per dokumen di tahap preparation. Ini sumber utama selisih waktu antara baseline dan pipeline.
- **Flag `--dpi` eksplisit** mencegah LSTM salah estimasi ukuran karakter saat menerima numpy array (tanpa metadata resolusi).
- **PDF Digital** (text-extractable) di-skip OCR, ekstrak langsung via `pdftotext` → CER 0% dengan waktu < 0.3s/dokumen.
- **Dokumen dengan watermark/stempel** cenderung CER lebih tinggi. Garbage line removal + Black Top-Hat membantu, tetapi tidak menghilangkan sepenuhnya.

---

## Version

### v1.0.2 — Refactor simplifikasi
1. **Layer 1** — Rename stage: Resize, Denoise, Morfologi Black Top-Hat. Label timing `Threshold` → `BlackHat`, tambah `Otsu`. Hapus 6 cell SAVE dead code.
2. **Layer 2** — Konsolidasi ~30 konstanta ke satu cell konfigurasi. Ekstrak Tesseract config (`TESSERACT_LANG`, `TESSERACT_OEM`, `OSD_FALLBACK_PSM`) dari hardcoded.
3. **Layer 3** — Pecah timing `Orientasi` jadi `OSD` + `Skew` terpisah → analisis trade-off lebih granular.
4. **Verifikasi parity** — WER/CER per dokumen identik byte-per-byte antar layer (24 OCR + 18 PDF digital).

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
