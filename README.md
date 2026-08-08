# Cek Uang Masuk — PWA

Aplikasi web laporan uang masuk harian (upload Excel → tabel & ringkasan), sudah dikonfigurasi sebagai **PWA (Progressive Web App)** sehingga bisa di-install seperti aplikasi native di HP/laptop.

## Isi folder
- `index.html` — aplikasi utama
- `manifest.json` — konfigurasi PWA (nama, ikon, warna)
- `sw.js` — service worker (bikin aplikasi bisa jalan offline & installable)
- `icon-192.png`, `icon-512.png` — ikon aplikasi

## Cara deploy ke GitHub Pages

1. Buat repository baru di GitHub (bisa public/private, tapi GitHub Pages gratis hanya untuk public repo kecuali punya GitHub Pro/Team).
2. Upload **semua file di folder ini** (index.html, manifest.json, sw.js, icon-192.png, icon-512.png) ke root repository tersebut (jangan dimasukkan ke subfolder).
3. Buka **Settings → Pages** di repo tersebut.
4. Pada bagian **Source**, pilih branch `main` (atau `master`) dan folder `/ (root)`, lalu klik **Save**.
5. Tunggu 1–2 menit, GitHub akan memberi URL seperti:
   `https://<username>.github.io/<nama-repo>/`
6. Buka URL itu di HP (Chrome/Safari) atau laptop.

## Cara install sebagai aplikasi

- **Android (Chrome):** buka URL di atas → akan muncul menu ☰ di aplikasi, pilih **"📲 Install Aplikasi"**, atau Chrome otomatis menampilkan banner "Tambahkan ke layar Utama".
- **iPhone (Safari):** buka URL → tombol Share (kotak dengan panah) → **"Add to Home Screen"**.
- **Desktop (Chrome/Edge):** akan muncul ikon install (⊕) di address bar, atau lewat menu ☰ di aplikasi.

Setelah diinstall, aplikasi akan punya ikon sendiri, terbuka fullscreen tanpa address bar, dan tetap bisa dibuka meski koneksi lambat/offline (karena file inti sudah tersimpan di cache browser).

## Catatan penting

- **HTTPS wajib** untuk PWA & service worker — GitHub Pages otomatis pakai HTTPS, jadi aman.
- Library pembaca Excel (`xlsx.js`) dimuat dari CDN (`cdn.jsdelivr.net`) dan ikut di-cache oleh service worker saat pertama kali dibuka online, supaya upload Excel tetap bisa dilakukan walau nanti sedang offline (selama sudah pernah dibuka sekali secara online).
- Setiap kali kamu update `index.html` di GitHub, browser pengguna lama mungkin masih pakai versi cache. Untuk memaksa update, ubah nilai `CACHE_NAME` di `sw.js` (misal dari `v1` jadi `v2`) setiap kali deploy ulang.
- Data Excel diproses 100% di browser pengguna (client-side) — tidak ada data yang dikirim ke server manapun.
