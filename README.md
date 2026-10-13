# SUMBAREKSIS — Portal Berita Indonesia

Paket terpisah dari website Kenseonn. Hosting statis GitHub Pages; Firebase Authentication untuk admin, Firestore untuk artikel, Firebase Storage untuk gambar.

## 1. Firebase terpisah
1. Buat proyek baru di https://console.firebase.google.com/ misalnya `sumbareksis-news`.
2. Buat Web App di Project settings > Your apps, lalu isi `firebase-config.js` dengan konfigurasi yang diberikan Console. `storageBucket` harus disalin persis, jangan ditebak.
3. Authentication > Sign-in method: aktifkan Email/Password. Tambah user redaksi melalui Authentication > Users.
4. Aktifkan Firestore Database. Pada Firestore, buat koleksi `admins`, dengan ID dokumen sama persis seperti UID user redaksi, dan field `enabled` bertipe Boolean `true`.
5. Salin `firestore.rules` ke Firestore > Rules, lalu Publish.
6. Aktifkan Storage bila tersedia untuk proyek/paketmu. Salin `storage.rules` ke Storage > Rules, lalu Publish. Jika Storage belum tersedia, upload foto tidak akan berfungsi sampai diaktifkan.

## 2. GitHub Pages
1. Buat repository baru, misalnya `sumbareksis-news` — jangan menimpa repository Kenseonn.
2. Unggah semua file dalam folder ini ke root repository.
3. Settings > Pages > Deploy from a branch > `main` > `/(root)` > Save.
4. Pastikan domain `USERNAME.github.io` di Firebase Authentication > Settings > Authorized domains.
5. Buka `https://USERNAME.github.io/sumbareksis-news/` dan `https://USERNAME.github.io/sumbareksis-news/admin.html`.

## 3. Menulis berita
Login di `/admin.html`, isi judul, ringkasan, kategori, penulis, isi, dan pilih foto (JPG/PNG/WebP maks. 5 MB). Pilih Draft atau Terbitkan. Artikel publik muncul di beranda setelah terbit.

## Keamanan
- Pengunjung hanya bisa membaca artikel berstatus `published`; draft hanya bisa dibaca admin.
- Perubahan artikel dan unggahan gambar membutuhkan admin aktif (`admins/{UID}` dengan `enabled: true`).
- Jangan pernah membuka izin tulis untuk semua orang. Jangan taruh service account/private key di frontend.
- Pastikan fakta, sumber, tanggal, hak cipta foto, dan privasi narasumber diverifikasi sebelum menerbitkan berita.
- Bila Firestore meminta index untuk kombinasi status/publishedAt, gunakan tautan pembuatan index dari pesan error Console.
