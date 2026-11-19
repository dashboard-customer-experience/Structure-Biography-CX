# Structure Demography — CX

Dashboard demografi struktur tim **Customer Experience**: Nama, Role, Segmentasi (Jabatan), Vendor, Jenis Kelamin, Agama, dan Tenure — ditampilkan dalam **chart interaktif**, tabel yang bisa di-search & difilter, dan **auto-update** langsung dari Google Sheets.

🔗 **Dashboard:** https://dashboard-customer-experience.github.io/Structure-Demography-CX/

## Fitur
- 📅 **Resume Manpower Bulanan** (Jan–Nov) — rekap Total MP, CCU/HCU/Shiftlead/New Joiner (Role) & Junior/Senior/Shiftlead (Jabatan) per bulan
- ⚖️ **Budget vs Actual** per jabatan (bar chart + tabel gap) — budget dibaca otomatis dari tab `#Budget`
- 🧮 **Cross-tab Jabatan × Role** dengan subtotal
- 📊 6 pie chart: **Vendor**, **Jabatan**, **Role**, **Jenis Kelamin**, **Agama**, **Tenure (masa kerja)**
- 🗓️ **Dropdown multi-bulan** (Januari–November 2026, riwayat tersimpan)
- ⏳ **Tenure dihitung live** dari Join Date s/d hari ini (otomatis bergeser mengikuti tanggal berjalan)
- 🔄 **Auto-update** — data ditarik langsung dari Google Sheets (Publish to web / CSV)
- 🔍 Tabel profil dengan pencarian & filter (Vendor, Role, Agama, Tenure)
- 📱 **Mobile-friendly** (responsive)

## Sumber Data
Semua tab Google Sheets di-publish via **File → Share → Publish to web → Entire Document → CSV**. Dashboard membaca tiap bulan lewat `gid` masing-masing tab. Tab `#Budget` berisi angka budget per bulan (kolom: Bulan, Shiftlead, Senior Agent, Junior Agent).

## Cara Menambah Bulan Baru (mis. Desember 2026)

1. **Buat tab baru** di spreadsheet (contoh: `Desember2026`), format kolom sama persis:
   `Nama | Employee ID | Location | Jabatan | Role | Vendor | Jenis Kelamin | Agama | Join Date`
2. Pastikan spreadsheet masih dalam mode **Publish to web → Entire Document** (sekali set, semua tab ikut ter-publish).
3. Ambil `gid` tab baru dari URL-nya, lalu di `index.html` bagian `DATA_SOURCES` tambahkan 1 baris di **paling atas**:
   ```js
   const DATA_SOURCES = [
     { label: "December 2026", url: csv("GID_TAB_DESEMBER") },  // <-- tambahkan paling atas
     { label: "November 2026", url: csv("0") },
     ...
   ];
   ```
4. Tambahkan juga bulan itu ke `RESUME_ORDER` agar muncul di tabel resume bulanan.
5. Isi budget Desember di tab `#Budget` → otomatis terbaca dashboard.

> Bulan paling atas di `DATA_SOURCES` jadi tampilan default saat dashboard dibuka.

## Catatan
- Data ditarik read-only dari link "Publish to web", jadi dashboard **tidak bisa mengubah** isi spreadsheet.
- Perubahan data/budget di spreadsheet muncul di dashboard setelah Google me-refresh cache publish (biasanya beberapa menit). Tekan tombol **⟳** untuk memuat ulang.
- Nilai Agama "Muslim" otomatis dinormalisasi menjadi "Islam".
