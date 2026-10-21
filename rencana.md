# Rencana: menambahkan tools dan artikel dari laporan.md

Situs: Hugo (pt-BR), deploy GitHub Pages. Sumber: `laporan.md` (4devs.com.br + invertexto.com).

## Hasil tahap 1 (sudah dikerjakan)

| Item | Jumlah / lokasi |
|---|---|
| Halaman tool kosong (draft) | 212 file di `content/ferramentas/` |
| Halaman artikel kosong (draft) | 16 file baru di `content/artigos/` |
| Hub | `content/ferramentas/_index.md` + `layouts/ferramentas/list.html` |
| Navbar | "Ferramentas" ditaruh sebelum "Artigos" (`hugo.toml`) |
| Related tools otomatis | `layouts/partials/related-tools.html`, dipanggil di `layouts/_default/single.html` |
| Kartu, ikon, data kategori | `layouts/partials/tool-card.html`, `icon.html`, `data/ferramentas_categorias.yaml` |
| Daftar slug | `daftarslugs.md` |

Setiap file tool/artikel hanya berisi front matter: `title`, `seoTitle`, `description`, `summary`, `date`, `draft: true`, `category`, `tags`, `keywords`. Isi (body) kosong.

## Cara kerja

- **URL**: tool di `/ferramentas/<slug>/`, artikel di `/artigos/<slug>/`.
- **Draft**: Hugo tidak membangun halaman `draft: true`. Karena itu hub dan related tools hanya menampilkan tool yang sudah terbit (tidak ada link mati). Selama semua masih draft, hub menampilkan kartu "Mais usadas" dan pesan "Novas ferramentas a caminho".
- **Hub**: dikelompokkan per kategori (urutan di `data/ferramentas_categorias.yaml`), ada pencarian dan filter kategori (JavaScript, tanpa library). 27 halaman inscrição estadual per UF tampil sebagai pil kecil "Por estado" (field `compact: true`).
- **Related tools (5 tool berbeda, setelah akhir artikel)**: skor = jumlah bobot tag yang sama; tag langka (mis. `cnpj`) bobotnya lebih besar dari tag umum (mis. `gerador`). Bonus kecil jika kategori sama. Seri dipecah berdasarkan kedekatan slug, supaya 27 halaman UF tidak menampilkan 5 tool yang sama. Jika tag cocok kurang dari 5, sisanya diisi tool lain agar tetap 5. Berlaku untuk halaman tool dan artikel. Tidak perlu menjalankan script atau mengedit file `.md`; Hugo menghitungnya saat build.
- Untuk 13 artikel lama, hanya `category` dan `tags` yang ditambahkan di front matter (isi tidak disentuh), supaya blok related muncul juga di sana.

## Tahap 2: mengisi dan menerbitkan (belum dikerjakan)

1. **Urutan prioritas**: mulai dari kelompok yang dekat dengan topik situs dan trafik CPF: generator/validator CNPJ, RG, CEP, CNH, PIS, título de eleitor, certidões, cartão; lalu inscrição estadual; lalu kalkulator dan tool teks.
2. **Per tool**: tulis logika (JavaScript di browser, seperti `cpf-tool.html`), isi 300+ kata (cara pakai, contoh, FAQ), lalu ubah `draft: true` menjadi `false`. Tool berdasarkan perhitungan (digit verifikasi, area, MMC) cukup JavaScript; tool yang butuh server (Whois, DNS Lookup, Consulta CNPJ/CEP, Tabela Fipe, kurs, Localizar IP) butuh API pihak ketiga, jadi dikerjakan belakangan.
3. **Template tool**: saat tool pertama siap, buat `layouts/ferramentas/single.html` (atau `layout:` di front matter, seperti `validador`) dengan skema JSON-LD WebApplication + FAQPage dan slot iklan, mengikuti `validador.html`.
4. **Terbitkan bertahap**: 10 sampai 20 tool per rilis lebih aman untuk AdSense dan indexing daripada 200 halaman sekaligus. Jangan menerbitkan halaman yang masih kosong.
5. **Sebelum rilis**: `hugo --minify`, cek sitemap, kirim ulang di Search Console.

## Keputusan dan risiko yang perlu Anda putuskan

- **Hub kosong di navbar**: selama belum ada tool terbit, `/ferramentas/` hanya berisi 2 kartu dan pesan "segera hadir", tetapi tetap masuk sitemap. Pertimbangkan menambah `noindex` sampai tool pertama terbit, atau menunda menaruh "Ferramentas" di navbar.
- **Tool Instagram (6 tool, 9 artikel) dan Contador de Inscritos**: tidak sesuai niche CPF/dokumen, dan sebagian (follow otomatis, melihat story anonim, hapus pengikut massal) melanggar aturan Instagram atau butuh login pengguna. Ada di daftar sebagai draft; saya sarankan tidak diterbitkan. Cukup hapus filenya jika tidak jadi.
- **Generator dokumen palsu** (RG, CNH, cartão, certidões, título, conta bancária): pakai nada yang sama dengan situs ini, yaitu angka acak hanya untuk testes, dengan catatan jelas di tiap halaman.
- **Konten sumber**: laporan.md hanya berisi H1 dan URL. Judul, deskripsi, dan ringkasan saya tulis sendiri dari nama dan tujuan tiap tool, tanpa membuka satu per satu halaman sumber. Tulis isi dengan kata-kata sendiri; jangan menyalin teks 4devs/invertexto.
- **Judul bertahun** (Calendário 2026, Feriados 2026, Salário Mínimo 2026, Calendário Lunar 2026): slug memuat tahun; perlu pembaruan tiap tahun.
- **Dilewati**: halaman indeks "Matemática" dan "Computação" (diganti hub), "Sobre", "Contato", "Blog" (sudah ada di situs Anda).
