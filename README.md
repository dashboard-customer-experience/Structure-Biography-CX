# Structure Biography — CX

Dashboard biografi struktur tim **Customer Experience**: Nama, Role, Segmentasi (Jabatan), dan Vendor — ditampilkan dalam **pie chart interaktif**, tabel yang bisa di-search, dan **auto-update** langsung dari Google Sheets.

🔗 **Dashboard:** https://dashboard-customer-experience.github.io/Structure-Biography-CX/

## Fitur
- 📊 4 pie chart: **Vendor**, **Jabatan (Segmentasi)**, **Role**, **Jenis Kelamin**
- 🗓️ **Dropdown multi-bulan** (riwayat per bulan tersimpan)
- 🔄 **Auto-update** — data ditarik langsung dari Google Sheets (publish to web / CSV)
- 🔍 Tabel profil dengan pencarian & filter (Vendor, Role)
- 📱 **Mobile-friendly** (responsive)

## Cara Menambah Bulan Baru (mis. Desember 2026)

Tiap awal bulan, cukup 3 langkah:

1. **Buat tab baru** di spreadsheet `Structure Biography - CX` (contoh nama tab: `Desember2026`), isi datanya dengan format kolom yang sama:
   `Nama | Employee ID | Location | Jabatan | Role | Vendor | Jenis Kelamin`

2. **Publish tab itu ke web:**
   - Buka spreadsheet → **File → Share → Publish to web**
   - Dropdown 1: pilih tab baru (mis. `Desember2026`)
   - Dropdown 2: **Comma-separated values (.csv)**
   - Klik **Publish** → copy link CSV-nya

3. **Tambahkan 1 baris** di file `index.html`, pada bagian `DATA_SOURCES` (dekat atas blok `<script>`):

   ```js
   const DATA_SOURCES = [
     { label: "Desember 2026", url: "PASTE_LINK_CSV_DESEMBER" },  // <-- tambahkan di paling atas
     { label: "November 2026", url: "https://docs.google.com/.../output=csv" }
   ];
   ```
   > Bulan yang diletakkan **paling atas** akan menjadi tampilan default saat dashboard dibuka.

Selesai — commit perubahan, dan dashboard otomatis punya pilihan bulan baru. 🎉

## Catatan
- Data ditarik read-only dari link "Publish to web", jadi dashboard **tidak bisa mengubah** isi spreadsheet.
- Perubahan data di spreadsheet akan muncul di dashboard setelah Google me-refresh cache publish (biasanya beberapa menit). Tekan tombol **⟳** untuk memuat ulang.
