# Stage 09 - Teks Hasil OCR

Untuk setiap dokumen representatif: *ground truth*, OCR tanpa
*preprocessing*, OCR dengan *preprocessing* (pipeline+BlackHat).
Snippet 250 karakter pertama di bawah; teks penuh tersimpan di
masing-masing sub-folder.

## ANYERLOR (Listrik).jpg

**Ground Truth:**
```
PT POS INDONESIA (PERSERO) / Kantor Kpc. Bandung Cilaki 40115A / TANDA TERIMA / TAGIHAN PLN POSTPAID /  / Tanggal : 09-10-2025 09:41:20 / No.Resi : 40115A-07/2025/803129 Petugas : 550050125 /  / STRUK PEMBAYARAN TAGIHAN LISTRIK / IDPEL : 539510373303 / NAMA : KANTOR POS
```

**OCR Tanpa Preprocessing:**
```
PT POS INDONESIA (PERSERO) / Kantor Kpc. Bandung Cilaki 40115A / TANDA TERIMA / TAGIHAN PLN POSTPAID / Tanggal : 09-10-2025 09:41:20 / No.Resi : 40115A-07/2025/803129 Petugas : 550050125 / STRUK PEMBAYARAN TAGIHAN LISTRIK / IDPEL 1 539510373303 / NAMA : KANTOR POS G
```

**OCR Dengan Preprocessing+BlackHat:**
```
PT POS INDONESIA (PERSERO) / Kantor Kpc. Bandung Cilaki 40115A / TANDA TERIMA / TAGIHAN PLN POSTPAID / Tanggal : 09-10-2025 09:41:20 / No.Resi : 40115A-07/2025/803129 Petugas : 550050125 / STRUK PEMBAYARAN TAGIHAN LISTRIK / IDPEL : 539510373303 / NAMA : KANTOR POS G
```

## DEMPET (Air Gas).png

**Ground Truth:**
```
PENGELOLAAN AIR BERSIH (PAB) / TIRTO WONO / DESA BOTONGON KEC. DEMPET KAB. DEMAK /  / TAGIHAN REKENING AIR DAN NON AIR /  / Nama : SINGGIH Bulan : OKOTBER 2025 / Alamat : BOTOSENGON RT.01 RW.02 / No.Samb : 02-01.010 /  / Angka Meter Perincian Harga Air Harga Air 82.500 / 
```

**OCR Tanpa Preprocessing:**
```
PENGOLAHAN AIR BERSIH (PAB) / TIRTO WONO / DESA BOTOSENGON KEC. DEMPET KAB. DEMAK / TAGIHAN REKENING AIR DAN NON AIR / Nama : SINGGIH Bulan : OKOTBER 2025 / (Alamat : BOTOSENGON RT.01 RW.02 / No.Samb 02-01.010 / Angka Meter Perincian Harga Air Harga Air 82.500 / uM 
```

**OCR Dengan Preprocessing+BlackHat:**
```
Lan PENGOLAHAN AIR BERSIH (PAB) / TINTO WOno / DESA BOTOSENGON KEC. DEMPET KAB. DEMAK / TAGIHAN REKENING AIR DAN NON AIR / Nama SINGGIH Bulan OKOTBER 2025 / Alamat BOTOSENGON RT.01 RW.02 / No Samb 02-01.010 / Angka Motor Perinclan Harga Air (Harga Air 82.500 / Mw? r
```

## MANYAR (Telpon).pdf

**Ground Truth:**
```
PT POS INDONESIA (Persero) KOREK : 5104010002 / KANTOR POS GRESIK 61100 Pemakaian Telpon /  / KUITANSI /  / Sudah Terima Dari : Executive Manager Kantor Cabang Gresik 61100 / Uang Sebanyak : seratus ribu Rupiah / Untuk Pembayaran : Pemakaian Telepon/Telegram/Fax :
```

**OCR Tanpa Preprocessing:**
```
PT POS INDONESIA (Persero) KOREK : 5104010002 / KANTOR POS GRESIK 61100 Pemakaian Telpon / KUITANSI / Sudah Terima Dari”: Executive Manager Kantor Cabang Gresik 61100 / Uang Sebanyak : seratus ribu Rupiah / Untuk Pembayaran : Pemakaian Telepon/Telegram/Fax : O
```

**OCR Dengan Preprocessing+BlackHat:**
```
PT POS INDONESIA (Persero) KOREK : 5104010002 / KANTOR POS GRESIK 61100 Pemakaian Telpon / KUITANSI / Sudah Terima Dari”: Executive Manager Kantor Cabang Gresik 61100 / Uang Sebanyak : seratus ribu Rupiah / Untuk Pembayaran : Pemakaian Telepon/Telegram/Fax : O
```

## MUARATAE (Air Gas).png

**Ground Truth:**
```
PT POS INDONESIA (PERSERO) / Kantor Kpc. Bandung Cilaki 40115A / TANDA TERIMA / PDAM TIRTA SENDAWAR KAB. KUTAI BARAT /  / Tanggal : 16-10-2025 13:32:20 / No.Resi : 40115A-07/2025/807175 Petugas : 550050125 /  / NO.SAMBUNGAN : 1102010208 / NAMA : HENDRIKUS HENDI / ALAMAT
```

**OCR Tanpa Preprocessing:**
```
PT POS INDONESIA (PERSERO) / Kantor Kpe. Bandung Cilaki 401258 / TANDA TERIMA / PDAM TIRTA SENDAMR KAB. KUTAI BARAT / Tanggal / No. Resi / 16-10-2025 13:32:20 / 401154-67/2625/807175 | Petugas : 550856125 / No. SAMBUNGAN 192010208 / mama HENORIKUS HENOT / ALAMAT MUA TAE
```

**OCR Dengan Preprocessing+BlackHat:**
```
PT POS INDONESIA (PERSERO) / Kantor Kpc. Bandung Cilaki 40115A / TANDA TERIMA / PDAM TIRTA SENDAWAR KAB. KUTAI BARAT / Tanggal : 16-10-2625 13:32:20 / No.Resi : 480115A-07/2025/807175 Petugas : 558050125 / NO. SAMBUNGAN : 1162616288 / NAMA : HENDRIKUS HENDI / ALAMAT
```

