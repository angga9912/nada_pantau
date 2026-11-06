# Nada Pantau

Dashboard web untuk admin Nada Pos: memantau rekap penjualan harian semua cabang dari jauh.
Satu file `index.html`, tanpa build. Membaca rekap penjualan dari Firestore project `nadapos-4ba51`, dan (khusus pemilik toko) mendaftarkan toko serta mengelola cabang.

## Pasang di Vercel
1. Upload `index.html`, `vercel.json`, dan `README.md` ke repo GitHub ini.
2. Vercel > Add New > Project > pilih repo ini > Framework Preset: Other > Deploy. Root Directory dikosongkan.
3. Firebase Console > Authentication > Settings > Authorized domains > Add domain: isi domain Vercel (mis. `nada-pantau.vercel.app`).
4. Buka domain itu, masuk dengan email akun admin. Kode Toko otomatis = UID akun admin.

## Catatan
- Admin tambahan (bukan pemilik): daftarkan di `toko/{UID pemilik}/anggota/{UID admin}` dengan `peran` = `ADMIN`, lalu masukkan Kode Toko saat diminta.
- Konfigurasi Firebase di `index.html` bukan rahasia. Keamanan data dijaga `firestore.rules` di repo Nada Pos.
- Versi Firebase JS SDK dikunci (10.12.2) di baris `import`.

## Daftar toko dan kelola cabang
- **Daftar toko baru:** di layar masuk pilih "Belum punya toko? Daftar di sini", isi nama toko, email, password, dan Kode Aktivasi dari penjual. Kode dibuat penjual di Firestore (`aktivasi/{kode}`, isi `aktif: true`, `batasCabang`) dan hanya bisa dipakai sekali.
- **Kelola cabang:** muncul di dashboard pemilik toko. Buat undangan (nama cabang + kode cabang), berikan kode 10 karakter ke pengelola cabang (berlaku 7 hari, sekali pakai). Undangan bisa dibatalkan, dan akses cabang yang sudah bergabung bisa dicabut.
- Jumlah cabang (anggota + undangan menunggu) dibatasi `batasCabang` dari kode aktivasi. Batas ini ditegakkan di tampilan; aturan Firestore menjaga keabsahan kodenya.
- Admin tambahan (bukan pemilik) tidak melihat Kelola cabang.
