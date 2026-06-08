# Stage 10 - Evaluasi

Sumber utama angka **Bab V**. File JSON/CSV/MD lengkap disalin
otomatis dari `OCR Evaluation/` (run terakhir) ke folder ini.

## Ringkasan 4 Skenario Ablation

| Skenario | Avg WER (%) | Avg CER (%) | Avg Waktu (s) |
|---|---:|---:|---:|
| Baseline (raw) | 19.53 | 9.89 | 1.68 |
| Pipeline + BlackHat | 15.31 | 7.51 | 7.53 |
| Pipeline + Otsu | 23.14 | 12.25 | 7.39 |
| Pipeline + AdaptiveGauss | 23.45 | 10.53 | 7.55 |

## Status Dokumen: Membaik / Memburuk / Stabil

Toleransi stabil: +/- 1.0% CER absolut.

| Status | Jumlah |
|---|---:|
| membaik | 11 |
| memburuk | 2 |
| stabil | 11 |

## Detail per Dokumen

| Dokumen | CER baseline | CER +BH | Delta CER | Status |
|---|---:|---:|---:|---|
| ANYERLOR (Listrik).jpg | 1.40% | 0.11% | +1.29% | membaik |
| BANDARBARU (Listrik).pdf | 14.78% | 11.87% | +2.91% | membaik |
| BANDARBARU (Telpon).pdf | 0.46% | 0.69% | -0.23% | stabil |
| BATANGKUIS (Air Gas).pdf | 13.09% | 9.07% | +4.02% | membaik |
| BATANGKUIS (Telpon).pdf | 0.92% | 0.46% | +0.46% | stabil |
| DEMPET (Air Gas).png | 14.65% | 18.90% | -4.25% | memburuk |
| JERUKLEGI (Listrik).jpg | 13.77% | 3.36% | +10.41% | membaik |
| LEGOK (Telpon).pdf | 1.36% | 1.22% | +0.14% | stabil |
| MANYAR (Listrik).pdf | 18.68% | 13.71% | +4.97% | membaik |
| MANYAR (Telpon).pdf | 30.70% | 26.74% | +3.96% | membaik |
| MEDANPAYAGELI (Air Gas).pdf | 13.73% | 13.15% | +0.58% | stabil |
| MEDANPAYAGELI (Listrik).pdf | 11.21% | 11.42% | -0.22% | stabil |
| MEDANPAYAGELI (Telpon).pdf | 0.92% | 0.23% | +0.69% | stabil |
| MUARATAE (Air Gas).png | 20.88% | 4.39% | +16.49% | membaik |
| NAMORAMBE (Air Gas).pdf | 13.80% | 12.87% | +0.94% | stabil |
| NAMORAMBE (Listrik).pdf | 13.67% | 7.97% | +5.71% | membaik |
| NAMORAMBE (Telpon).pdf | 0.92% | 0.69% | +0.23% | stabil |
| PANCAJAYA (Listrik).pdf | 10.73% | 14.38% | -3.65% | memburuk |
| PANCURBATU (Listrik).pdf | 12.54% | 11.36% | +1.18% | membaik |
| PANCURBATU (Telpon).pdf | 0.93% | 0.46% | +0.46% | stabil |
| SEPATAN (Listrik).pdf | 2.83% | 3.27% | -0.45% | stabil |
| SINDANGKERTA (Telpon).jpg | 1.11% | 0.28% | +0.83% | stabil |
| SUKATANI (Air Gas).pdf | 8.09% | 3.14% | +4.95% | membaik |
| TOPOYO (Listrik).png | 16.25% | 10.62% | +5.63% | membaik |

## Dugaan Penyebab

Dokumen **memburuk** setelah pipeline+BlackHat umumnya berciri:
- Resolusi asli sudah cukup tinggi -> *resize* justru menambah artefak.
- *Watermark* minim / tidak ada -> *black-hat* menghapus stroke teks tipis.
- Format PDF berkualitas tinggi (mendekati *PDF Digital*).

Dokumen **memburuk dengan margin besar** (Delta > 5%) layak dianalisis
kasus per kasus sebagai limitasi pipeline pada Bab V.

## File Evaluasi Terbaru (disalin)

- `eval_2026-06-08_151345_ablation-thresholding.json`
- `eval_2026-06-08_151345_ablation-thresholding.csv`
- `eval_2026-06-08_151216_bab5-konsolidasi-psm6-gtfix.md`
- `eval_2026-06-08_151216_bab5-konsolidasi-psm6-gtfix.csv`
- `eval_2026-06-08_151216_bab5-konsolidasi-psm6-gtfix.json`
- `eval_2026-06-08_151214_crisp-dm-pseudocode-doc-group-revised-eval-8.md`
