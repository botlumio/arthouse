# arthouse

> *pixels. patterns. paradoxes.*

**arthouse** adalah landing page satu halaman untuk komunitas galeri seni digital dan Telegram bot kurasi karya seni. Dibangun dengan HTML, CSS, dan vanilla JavaScript — tanpa framework, tanpa dependensi build.

---

## 📁 Struktur File

```
arthouse/
├── arthouse.html       # File utama — seluruh halaman (HTML + CSS + JS)
└── README.md           # Dokumentasi ini
```

Seluruh kode (HTML, CSS, JavaScript) terdapat dalam satu file `arthouse.html`.

---

## 🎨 Desain & Visual

### Palet Warna

| Variabel    | Nilai                        | Penggunaan                          |
|-------------|------------------------------|-------------------------------------|
| `--bg`      | `#080807`                    | Background utama                    |
| `--bg2`     | `#0f0f0d`                    | Background terminal / card          |
| `--white`   | `#f0ece2`                    | Teks utama                          |
| `--dim`     | `rgba(240,236,226, 0.92)`    | Teks paragraf / subtitle            |
| `--faint`   | `rgba(240,236,226, 0.70)`    | Teks sekunder / label kecil         |
| `--gold`    | `#d4a843`                    | Aksen utama, CTA, highlight         |
| `--amber`   | `#e8891a`                    | Aksen sekunder, hover state         |
| `--green`   | `#4ade80`                    | Indikator online, prompt terminal   |
| `--line`    | `rgba(255,255,255, 0.08)`    | Border / garis pemisah              |

### Tipografi

| Font                | Digunakan untuk                            |
|---------------------|--------------------------------------------|
| **IBM Plex Mono**   | Body, navigasi, label, tombol, kode        |
| **Playfair Display**| Heading besar, judul hero, blockquote      |

Font di-load dari Google Fonts via `<link>` di `<head>`.

### Efek Visual

- **Scanlines** — overlay tipis di seluruh halaman via `body::after` untuk nuansa retro/CRT
- **Grid background** — pola grid halus di bagian hero via `::before` pseudo-element
- **Reveal animation** — elemen masuk dengan fade + slide-up saat di-scroll (IntersectionObserver)
- **Ticker animation** — dua ticker berjalan secara loop: satu di atas (dark), satu di bawah (gold)
- **Blinking cursor** — cursor berkedip di hero section
- **Typewriter** — teks diketik otomatis saat halaman dimuat

---

## 🧩 Struktur Halaman

### 1. Top Ticker (Fixed)
Bar fixed di bagian atas layar. Menampilkan informasi scrolling otomatis:
- Label `LIVE` berwarna gold
- Item: `arthouse`, `@arthousebase`, `pixels. patterns. paradoxes.`, `gallery & art creators`, `est. jan 2026`, `t.me/arthousexbt_bot`
- Item diduplikasi untuk efek loop tanpa jeda

### 2. Hero Section (`#hero`)
Layar penuh (100svh). Berisi:
- Typewriter prompt dengan cursor berkedip
- Judul besar `arthouse` (serif italic, skala hingga 180px)
- Subtitle singkat tentang galeri
- Dua tombol CTA: **Open the Bot** (solid gold) dan **How it works** (ghost)
- Label vertikal `@arthousebase — 2026` di pojok kanan bawah

### 3. Stats Bar
Tiga kolom statistik:
- `148` Following
- `69` Followers
- `Jan` Est. 2026

### 4. How It Works (`#how`)
Lima langkah proses dalam format list bernomor:

| No. | Langkah                    | Deskripsi                                           |
|-----|----------------------------|-----------------------------------------------------|
| 01  | Say hi on Telegram         | Buka `@arthousexbt_bot` atau temukan di X           |
| 02  | Share your work            | Kirim karya, link koleksi, atau demo                |
| 03  | Receive curatorial feedback| Bot memberikan konteks, catatan kurasi, analisis    |
| 04  | Iterate & evolve           | Perbaiki karya, kembali untuk sesi berikutnya       |
| 05  | Join the creator network   | Kontributor terbaik masuk jaringan kolektor         |

### 5. Live Session Demo (`#demo`)
Mockup terminal chat yang mensimulasikan sesi nyata dengan bot. Menampilkan:
- Sistem log (`// session started`, `// connected`)
- Pesan bot (prefix `bot ›` berwarna amber)
- Pesan user (prefix `you ›` berwarna green)
- Catatan bot (indented, warna redup)
- Input row dengan tombol **Open Bot ↗** mengarah ke Telegram

### 6. Manifesto (`#about`)
- Blockquote besar bergaya serif italic
- Teks manifesto tentang filosofi arthouse
- Highlight kata `algorithm` (gold) dan `intuition` (amber)

### 7. Gold Ticker
Bar penuh berwarna gold dengan teks hitam, berjalan lebih cepat dari ticker atas. Item: `arthouse`, `pixels`, `patterns`, `paradoxes`, `@arthousebase`, `gallery & art creators`.

### 8. Bottom CTA (`#cta`)
- Teks pembuka `// ready to create?`
- Heading besar `start now. open the bot.`
- Dua tombol: link langsung ke Telegram bot & link ke X

### 9. Footer
- Logo `arthouse` + link sosial (𝕏 Twitter, ✈ Telegram)
- Navigasi internal: Process, The Bot, Manifesto, Open Bot
- Copyright line

---

## ⚙️ JavaScript

### Reveal on Scroll
```js
const io = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      setTimeout(() => e.target.classList.add('visible'), delay);
      io.unobserve(e.target);
    }
  });
}, { threshold: 0.08 });
```
Semua elemen dengan class `.reveal` akan fade-in + slide-up saat masuk viewport. Delay bertingkat tiap 60ms berdasarkan urutan elemen (maks 5 elemen per grup).

### Typewriter Effect
```js
const phrase = 'arthouse_init.exe — gallery & art creators';
// Mengetik karakter satu per satu dengan interval 38ms
// Delay awal 700ms sebelum mulai
```

---

## 🔗 Tautan Eksternal

| Tujuan             | URL                                  |
|--------------------|--------------------------------------|
| Telegram Bot       | https://t.me/arthousexbt_bot         |
| X (Twitter)        | https://x.com/arthousebase           |
| Google Fonts       | https://fonts.googleapis.com         |

---

## 📱 Responsivitas

Halaman menggunakan pendekatan **mobile-first**. Breakpoint desktop diterapkan via:

```css
@media (min-width: 768px) {
  /* padding lebih besar, tombol horizontal, footer row */
}
```

| Elemen           | Mobile                  | Desktop (≥768px)             |
|------------------|-------------------------|------------------------------|
| Hero padding     | `80px 24px`             | `100px 48px`                 |
| CTA buttons      | Kolom vertikal          | Baris horizontal             |
| Step padding     | `22px 24px`             | `24px 48px`                  |
| Footer           | Kolom vertikal          | Baris horizontal (flex-wrap) |

---

## 🚀 Cara Menjalankan

Tidak ada build step. Cukup buka file di browser:

```bash
# Opsi 1 — buka langsung
open arthouse.html

# Opsi 2 — serve lokal (opsional, untuk development)
npx serve .
# atau
python3 -m http.server 8080
```

> **Catatan:** Font IBM Plex Mono dan Playfair Display dimuat dari Google Fonts. Pastikan terhubung ke internet agar tampil dengan benar.

---

## ✏️ Kustomisasi

### Mengganti Warna Aksen
Edit variabel CSS di `:root` dalam `<style>`:
```css
--gold:  #d4a843;   /* ubah ke warna pilihan */
--amber: #e8891a;
```

### Mengubah Statistik
Cari bagian `<!-- STATS -->` dan ubah nilai:
```html
<span class="stat-val">148</span>   <!-- Following -->
<span class="stat-val">69</span>    <!-- Followers -->
```

### Mengganti Link Bot
Cari-ganti semua kemunculan `https://t.me/arthousexbt_bot` dengan link bot Anda.

### Menambah Item Ticker
Tambah `<span class="ticker-item">teks baru</span>` di dalam `.ticker-track`, lalu duplikat di bagian kedua untuk menjaga loop tetap seamless.

---

## 📄 Lisensi

© 2026 arthouse · All rights reserved.
