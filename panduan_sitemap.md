# Panduan & SOP Pembaruan Sitemap (Hugo)

Dokumen ini adalah panduan standar operasional (SOP) untuk memperbarui `sitemap.xml` setiap kali menambahkan postingan artikel atau tool baru, dengan memastikan **konten berstatus draft tidak masuk ke dalam sitemap**.

---

## 1. Prinsip Utama Sitemap di Hugo

1. **Eksklusi Draft Otomatis**: Hugo secara native **tidak akan memasukkan** halaman dengan tanda `draft: true` ke dalam `sitemap.xml` selama proses build produksi (`hugo` atau `hugo --minify`).
2. **Jangan Gunakan Flag Draft pada Build**: Jangan pernah menambahkan parameter `-D` atau `--buildDrafts` saat melakukan build untuk publikasi/deploy.
3. **Konfigurasi Global**: Konfigurasi sitemap aktif di `hugo.toml`:
   ```toml
   [sitemap]
     changefreq = "weekly"
     priority = 0.8
     filename = "sitemap.xml"
   ```

---

## 2. Alur Kerja (SOP) Saat Menambah Konten Baru

### Langkah 1: Pengerjaan Konten (Status Draft)
Selama artikel atau tool masih dalam tahap penulisan, kalkulator belum selesai, atau isi belum lengkap:
- Pastikan di bagian atas file `.md` (front matter):
  ```yaml
  draft: true
  ```
- *Hasil*: Konten aman dan tidak akan diindeks atau dimasukkan ke `sitemap.xml`.

### Langkah 2: Mengaktifkan Publikasi (Ready to Publish)
Setelah halaman selesai ditulis, fungsionalitas diuji, dan minimal kata terpenuhi:
1. Ubah status di front matter:
   ```yaml
   draft: false
   ```
2. Perbarui tanggal publikasi (`date`) ke tanggal saat ini:
   ```yaml
   date: 2026-10-21
   ```
   *(Tanggal ini akan otomatis menjadi tag `<lastmod>` di `sitemap.xml`)*.
3. Catat nama slug yang sudah selesai di `progress.md`.

---

## 3. Verifikasi & Build

Jalankan perintah berikut di terminal PowerShell sebelum melakukan commit:

### 1. Cek Halaman yang Siap Masuk Sitemap
```powershell
hugo list published
```
*Pastikan hanya halaman yang sudah selesai yang muncul di daftar ini.*

### 2. Cek Halaman yang Masih Ditahan (Drafts)
```powershell
hugo list drafts
```
*Pastikan halaman yang belum selesai tetap berstatus draft.*

### 3. Build Produksi Bersih
```powershell
hugo --minify
```
*Hugo akan memperbarui file `public/sitemap.xml` dengan URL produksi `https://geradorcpf.github.io/...`*.

### 4. Validasi Isi Sitemap
Periksa file `public/sitemap.xml` untuk memastikan:
- Semua link berawalan `https://geradorcpf.github.io/`.
- Tidak ada URL draft yang bocor.
- Tag `<changefreq>` dan `<priority>` terpasang dengan benar.

---

## 4. Deploy & Submit ke Mesin Pencari

1. **Commit dan Push ke GitHub**:
   ```powershell
   git add .
   git commit -m "feat: rilis konten baru dan update sitemap"
   git push origin master
   ```
2. **GitHub Actions**:
   Workflow `.github/workflows/hugo.yml` akan otomatis men-deploy versi terbaru ke GitHub Pages.

3. **Google Search Console**:
   - Buka [Google Search Console](https://search.google.com/search-console).
   - Masuk ke menu **Sitemaps**.
   - Kirimkan / resubmit URL: `https://geradorcpf.github.io/sitemap.xml`.
