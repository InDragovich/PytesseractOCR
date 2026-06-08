# Stage 06 - Denoising (Bilateral Filter)

*Bilateral filter* dipilih karena ***edge-preserving*** -- menghaluskan
*speckle* background tanpa mengaburkan tepi teks.

- `BILATERAL_DIAMETER = 5`
- `BILATERAL_SIGMA_COLOR = 50`
- `BILATERAL_SIGMA_SPACE = 50`

## Justifikasi Pemilihan

Ablation sebelumnya (file `OCR Evaluation/eval_2026-05-20_*denoise*`):

- Bilateral: avg CER **7.50%** (dipilih)
- Median 5x5: avg CER 10.93%
- NlMeans / median fallback: avg CER 8.15%
