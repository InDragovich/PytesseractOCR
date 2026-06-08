# Stage 05 - Konversi Grayscale

Konversi RGB -> 1 kanal dengan `cv2.COLOR_RGB2GRAY`. Citra yang sudah
1-kanal di-*skip* (idempotent).

## Rasional

Tesseract 5 (engine LSTM, OEM 3) bekerja lebih akurat pada *grayscale*
dibanding *binary* -- alasan mengapa *pipeline* utama tidak menerapkan
*thresholding* keras setelah tahap ini. Justifikasi empiris ada di
Stage 08 (ablation).
