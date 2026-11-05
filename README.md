# Disturbance Intelligence — GitHub Pages

Dashboard statis untuk analisis gangguan sistem tenaga dari Google Sheets `RAW DATA`.

## Pemasangan

1. Buat repository publik baru di GitHub, misalnya `dashboard-gangguan`.
2. Unggah `index.html` ke **root** repository (README ini opsional).
3. Buka **Settings → Pages → Build and deployment**.
4. Pilih **Deploy from a branch**, branch `main`, folder `/ (root)`, lalu **Save**.
5. Tunggu deployment dan buka `https://USERNAME.github.io/dashboard-gangguan/`.

## Sumber data

- Spreadsheet ID: `1574QKolhAl7UTs9EhEC3R8kZwsQLVILjqHGzAHHTYDA`
- Worksheet: `RAW DATA`
- Endpoint: Google Visualization CSV (`/gviz/tq?tqx=out:csv&sheet=RAW%20DATA`).
- Tidak ada API key, akun Google, atau backend.

**Penting:** Untuk pembacaan langsung di browser anonim, spreadsheet harus mengizinkan akses baca publik, misalnya **General access → Anyone with the link → Viewer**. Jangan buka akses publik jika datanya rahasia. Alternatif aman adalah ekspor CSV yang sudah disanitasi ke repository, lalu mengganti URL pengambilan di `index.html` ke file CSV tersebut.

## Definisi metrik

- **Frekuensi penyebab:** jumlah baris kejadian menurut teks kolom `Sebab` sebelum `=>`.
- **Kejadian padam:** hanya baris dengan `Padam = PADAM`.
- **Dampak energi / ENS:** penjumlahan kolom `Energi` pada baris padam, diasumsikan dalam MWh.
- Jika `Energi` kosong namun `Mw Hilang` dan `Durasi Keluar` valid, digunakan pendekatan `MW Hilang × Durasi Keluar` dengan asumsi MW konstan sepanjang periode. Validasi definisi sumber sebelum digunakan sebagai KPI resmi.
- **Σ MW Hilang:** penjumlahan MW per kejadian, **bukan** beban puncak simultan.
- **Rata-rata durasi:** rerata `Durasi Keluar` hanya untuk baris padam yang memiliki nilai durasi.

Unit hitung saat ini adalah **satu baris = satu catatan kejadian**. Jika satu gangguan mempunyai lebih dari satu baris per bay, perlu ID peristiwa untuk menghindari perhitungan kejadian ganda. Nama penyebab tetap mengikuti teks sumber (normalisasi kapital/spasi saja); tidak ada fuzzy grouping otomatis.

## Catatan

Kode tidak memakai dependensi JavaScript eksternal. Data diambil ulang ketika halaman dibuka atau tombol `Muat ulang` ditekan. Saya belum dapat memverifikasi akses langsung ke spreadsheet dari lingkungan pembuatan, sehingga uji koneksi final perlu dilakukan di browser setelah GitHub Pages aktif.
