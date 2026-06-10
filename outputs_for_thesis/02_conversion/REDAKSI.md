# Peringatan Redaksi Data Sensitif

Citra dokumen di folder ini berasal dari sumber **un-redacted** untuk
keperluan arsip eksperimen internal. Saat akan dipakai sebagai
*figure* di buku Tugas Akhir, **lakukan redaksi manual** pada area
berikut sebelum embed:

- Nama pelanggan
- NIK / nomor identitas
- Alamat
- Nomor pelanggan / nomor langganan
- Tanda tangan (bila ada)

Area aman ditampilkan (karena merupakan objek evaluasi OCR):

- Header dokumen (nama loket, kategori, periode)
- Tabel tagihan / nominal
- *Watermark* (justru menarik untuk pembahasan limitasi)
- Footer / barcode

Cara redaksi yang disarankan:

1. Buka PNG di image editor (mis. Paint, GIMP, Photoshop).
2. Pasang kotak hitam atau blur area sensitif.
3. Simpan dengan suffix `_redacted` (mis. `MANYAR_Telpon_original_redacted.png`).
4. Embed versi `_redacted` ke buku, **jangan** versi asli.
