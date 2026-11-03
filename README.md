# Nada Pantau

Dashboard web untuk admin Nada Pos: memantau rekap penjualan harian semua cabang dari jauh.
Satu file `index.html`, tanpa build. Membaca (tidak menulis) data dari Firestore project `nadapos-4ba51`.

## Pasang di Vercel
1. Upload `index.html`, `vercel.json`, dan `README.md` ke repo GitHub ini.
2. Vercel > Add New > Project > pilih repo ini > Framework Preset: Other > Deploy. Root Directory dikosongkan.
3. Firebase Console > Authentication > Settings > Authorized domains > Add domain: isi domain Vercel (mis. `nada-pantau.vercel.app`).
4. Buka domain itu, masuk dengan email akun admin. Kode Toko otomatis = UID akun admin.

## Catatan
- Admin tambahan (bukan pemilik): daftarkan di `toko/{UID pemilik}/anggota/{UID admin}` dengan `peran` = `ADMIN`, lalu masukkan Kode Toko saat diminta.
- Konfigurasi Firebase di `index.html` bukan rahasia. Keamanan data dijaga `firestore.rules` di repo Nada Pos.
- Versi Firebase JS SDK dikunci (10.12.2) di baris `import`.
