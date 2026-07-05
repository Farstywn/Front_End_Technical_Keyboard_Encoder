# Keyboard Transform Encoder

Program sederhana buat enkoding teks pakai transformasi layout keyboard QWERTY. Dibuat pakai HTML + JS murni, tinggal buka di browser.

## Cara Pakai

1. Buka `index.html` di browser
2. Isi kolom transformasi, misalnya `H,V,H,5,V,-12`
3. Ketik atau paste teks yang mau di-enkode (bisa juga upload file `.txt`)
4. Klik **Enkode Teks**, hasilnya langsung muncul di bawah

## Transformasi yang Tersedia

Ada 3 jenis transformasi. Semuanya bekerja di atas layout keyboard QWERTY 4 baris x 10 kolom:

```
1 2 3 4 5 6 7 8 9 0
q w e r t y u i o p
a s d f g h j k l ;
z x c v b n m , . /
```

### `H` — Flip Horizontal

Balik tiap baris dari kiri ke kanan. Jadi `1` tukar sama `0`, `q` tukar sama `p`, dst.

```
Sebelum:  1 2 3 4 5 6 7 8 9 0
Sesudah:  0 9 8 7 6 5 4 3 2 1
```

### `V` — Flip Vertikal

Balik tiap kolom dari atas ke bawah. Baris 0 tukar sama baris 3, baris 1 tukar sama baris 2.

```
Kolom pertama contohnya:
1 → z
q → a
a → q
z → 1
```

### `N` (angka) — Shift / Geser

Geser semua tombol sebanyak N posisi. Anggap 40 tombol keyboard itu satu baris lurus, terus digeser. Kalau lewat ujung, balik lagi ke awal.

Positif = geser kanan, negatif = geser kiri.

Contoh shift 5:
```
Sebelum:  1 2 3 4 5 6 7 8 9 0 | q w e r t ...
Sesudah:  n m , . / 1 2 3 4 5 | 6 7 8 9 0 ...
```
5 tombol terakhir (n m , . /) pindah ke depan, sisanya geser ke kanan.

### Chaining

Transformasi bisa digabung, dipisah koma. Tiap transformasi dijalankan berurutan — output dari yang sebelumnya jadi input yang berikutnya.

Contoh `H,V,H,5,V,-12` artinya:
1. Flip horizontal
2. Flip vertikal
3. Flip horizontal lagi
4. Shift 5 ke kanan
5. Flip vertikal
6. Shift 12 ke kiri

## Catatan

- Input diasumsikan lowercase semua
- Karakter yang gak ada di keyboard (spasi, newline, huruf besar, dll) tetap lolos apa adanya, gak diubah
- Bisa handle teks panjang

## Fitur

- Visualisasi keyboard sebelum & sesudah transformasi
- Tabel pemetaan karakter (karakter asli → hasil)
- Upload file `.txt` untuk transformasi maupun teks input
- Tombol salin hasil ke clipboard

## File

- `index.html` — file utama, semua logic ada di sini (HTML + CSS + JS)
- `README.md` — dokumentasi ini
