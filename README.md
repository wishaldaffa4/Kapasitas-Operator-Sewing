# Kapasitas Operator — Panduan Deploy ke Vercel

Webapp ini murni HTML + JavaScript (tidak perlu proses build), jadi deploy-nya simpel.

## 1. Push ke GitHub

1. Buat repository baru di GitHub (bisa **private** — tidak masalah, Vercel tetap bisa akses repo private kamu).
2. Di komputer kamu, masuk ke folder ini lalu jalankan:
   ```bash
   git init
   git add .
   git commit -m "Initial commit: Kapasitas Operator webapp"
   git branch -M main
   git remote add origin https://github.com/USERNAME/NAMA-REPO.git
   git push -u origin main
   ```
   (Ganti `USERNAME/NAMA-REPO` dengan repo yang kamu buat.)

   Kalau tidak familiar dengan Git/terminal, cara lain: buka repo di GitHub.com → **Add file → Upload files** → drag & drop `index.html` dan `vercel.json` dari folder ini → Commit.

## 2. Hubungkan ke Vercel

1. Buka [vercel.com](https://vercel.com) → daftar/login (bisa langsung pakai akun GitHub).
2. Klik **Add New → Project**.
3. Pilih repo GitHub yang baru kamu buat tadi.
4. Di halaman konfigurasi, **Framework Preset** akan otomatis terdeteksi sebagai "Other" — biarkan saja, tidak perlu isi Build Command atau Output Directory apa pun.
5. Klik **Deploy**.
6. Tunggu proses selesai (biasanya 10–30 detik) → Vercel akan memberi URL publik, contoh: `https://kapasitas-operator.vercel.app`.

Selesai — link itu yang dibagikan ke tim kamu. Tidak perlu install apa pun di sisi user, tinggal buka lewat browser.

## 3. Update setelah ada revisi

Setiap kali ada file baru dari saya (revisi lanjutan):
1. Ganti isi `index.html` di repo GitHub kamu dengan versi baru (lewat `git push` lagi, atau upload manual replace file di GitHub.com).
2. Vercel **otomatis** re-deploy begitu ada perubahan baru di branch `main` — tidak perlu klik apa pun di Vercel.

## 4. Yang berubah dari versi artifact/HTML lokal

- Sebelumnya data tersimpan lewat `window.storage` (khusus lingkungan Claude). Di versi ini datanya memakai **Google Sheets sebagai sumber utama** — setiap webapp dibuka, data Assignment & Kapasitas otomatis ditarik ulang dari Sheets, supaya semua user melihat versi terbaru.
- Konsekuensinya: kalau ada perubahan yang **belum di-klik "Simpan & cetak ke Sheets"** dan kamu keburu refresh/tutup browser, perubahan itu bisa hilang (tertimpa data lama dari Sheets). **Biasakan klik tombol simpan sebelum menutup tab**, terutama setelah selesai input banyak data.
- URL Apps Script sudah **ditanam langsung di kode** (hardcoded) — tidak perlu diisi manual sama sekali, di device apa pun. Kolom URL di tab Pengaturan tetap ada kalau nanti perlu ganti ke deployment baru.
- Versi ini sudah termasuk semua fitur terbaru: dashboard Line x Tanggal, navigasi Enter pindah baris, tampilan kartu otomatis di layar HP, sidebar (Input Kapasitas → Assignment Operator → Pengaturan), dan validasi operator belum diisi output sebelum sinkron ke Sheets.
- Ada tombol **"Muat ulang Assignment + Kapasitas dari Sheets"** di tab Pengaturan untuk menarik data terbaru manual kapan saja (berguna kalau kolega lain baru selesai input di device lain).

## 5. Custom domain (opsional)

Kalau ingin domain sendiri (misal `kapasitas.namaperusahaan.com`) bukan yang `.vercel.app`, bisa diatur di Vercel → Project Settings → Domains, lalu arahkan DNS domain kamu sesuai instruksi yang muncul.
