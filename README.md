# arthouse

> *pixels. patterns. paradoxes.*

**arthouse** is a single-page landing page for a digital art gallery community and AI-powered Telegram curation bot. Built with HTML, CSS, and vanilla JavaScript — no framework, no build dependencies.

---

## 📁 File Structure

```
arthouse/
├── arthouse.html       # Main file — entire page (HTML + CSS + JS)
└── README.md           # This documentation
```

All code (HTML, CSS, JavaScript) lives in a single `arthouse.html` file.

---

## 🎨 Design & Visuals

### Color Palette

| Variable    | Value                        | Usage                               |
|-------------|------------------------------|-------------------------------------|
| `--bg`      | `#080807`                    | Main background                     |
| `--bg2`     | `#0f0f0d`                    | Terminal / card background          |
| `--white`   | `#f0ece2`                    | Primary text                        |
| `--dim`     | `rgba(240,236,226, 0.92)`    | Paragraph text / subtitles          |
| `--faint`   | `rgba(240,236,226, 0.70)`    | Secondary text / small labels       |
| `--gold`    | `#d4a843`                    | Primary accent, CTA, highlights     |
| `--amber`   | `#e8891a`                    | Secondary accent, hover states      |
| `--green`   | `#4ade80`                    | Online indicator, terminal prompt   |
| `--line`    | `rgba(255,255,255, 0.08)`    | Borders / dividers                  |

### Typography

| Font                | Used for                                       |
|---------------------|------------------------------------------------|
| **IBM Plex Mono**   | Body text, navigation, labels, buttons, code   |
| **Playfair Display**| Large headings, hero title, blockquotes        |

Both fonts are loaded from Google Fonts via `<link>` in `<head>`.

### Visual Effects

- **Scanlines** — subtle full-page overlay via `body::after` for a retro/CRT aesthetic
- **Grid background** — faint grid pattern in the hero section via `::before` pseudo-element
- **Reveal animation** — elements fade in + slide up on scroll using IntersectionObserver
- **Ticker animation** — two infinite-loop tickers: one at the top (dark), one at the bottom (gold)
- **Blinking cursor** — animated cursor in the hero section
- **Typewriter** — text is auto-typed on page load

---

## 🧩 Page Structure

### 1. Top Ticker (Fixed)
Fixed bar at the top of the screen with auto-scrolling text:
- Gold `LIVE` label on the left
- Items: `arthouse`, `@arthousebase`, `pixels. patterns. paradoxes.`, `gallery & art creators`, `est. jan 2026`, `t.me/arthousexbt_bot`
- Items are duplicated for a seamless infinite loop

### 2. Hero Section (`#hero`)
Full-screen (100svh). Contains:
- Typewriter prompt with blinking cursor
- Large `arthouse` heading (italic serif, scales up to 180px)
- Short subtitle about the gallery
- Two CTA buttons: **Open the Bot** (solid gold) and **How it works** (ghost)
- Vertical label `@arthousebase — 2026` in the bottom-right corner

### 3. Stats Bar
Three-column statistics display:
- `148` Following
- `69` Followers
- `Jan` Est. 2026

### 4. How It Works (`#how`)
Five-step process in a numbered list format:

| No. | Step                       | Description                                              |
|-----|----------------------------|----------------------------------------------------------|
| 01  | Say hi on Telegram         | Open `@arthousexbt_bot` or find `@arthousebase` on X     |
| 02  | Share your work            | Submit artwork, collection links, or a demo              |
| 03  | Receive curatorial feedback| Bot provides context, curation notes, and analysis       |
| 04  | Iterate & evolve           | Refine your work and return for more sessions            |
| 05  | Join the creator network   | Top contributors enter the arthouse collector network    |

### 5. Live Session Demo (`#demo`)
A terminal chat mockup simulating a real bot session. Displays:
- System logs (`// session started`, `// connected`)
- Bot messages (prefixed with `bot ›` in amber)
- User messages (prefixed with `you ›` in green)
- Bot notes (indented, dimmed color)
- Input row with an **Open Bot ↗** button linking to Telegram

### 6. Manifesto (`#about`)
- Large serif italic blockquote
- Manifesto text about arthouse's philosophy
- Highlighted words: `algorithm` (gold) and `intuition` (amber)

### 7. Gold Ticker
Full-width gold bar with black text, running faster than the top ticker. Items: `arthouse`, `pixels`, `patterns`, `paradoxes`, `@arthousebase`, `gallery & art creators`.

### 8. Bottom CTA (`#cta`)
- Pre-text `// ready to create?`
- Large heading `start now. open the bot.`
- Two buttons: direct link to the Telegram bot & link to X

### 9. Footer
- `arthouse` logo + social links (𝕏 Twitter, ✈ Telegram)
- Internal navigation: Process, The Bot, Manifesto, Open Bot
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
All elements with the `.reveal` class fade in + slide up when they enter the viewport. Delays are staggered by 60ms based on element index (max 5 elements per group).

### Typewriter Effect
```js
const phrase = 'arthouse_init.exe — gallery & art creators';
// Types one character at a time with a 38ms interval
// Initial delay of 700ms before starting
```

---

## 🔗 External Links

| Destination        | URL                                  |
|--------------------|--------------------------------------|
| Telegram Bot       | https://t.me/arthousexbt_bot         |
| X (Twitter)        | https://x.com/arthousebase           |
| Google Fonts       | https://fonts.googleapis.com         |

---

## 📱 Responsiveness

The page follows a **mobile-first** approach. Desktop styles are applied via:

```css
@media (min-width: 768px) {
  /* larger padding, horizontal buttons, footer row */
}
```

| Element          | Mobile                  | Desktop (≥768px)              |
|------------------|-------------------------|-------------------------------|
| Hero padding     | `80px 24px`             | `100px 48px`                  |
| CTA buttons      | Vertical stack          | Horizontal row                |
| Step padding     | `22px 24px`             | `24px 48px`                   |
| Footer           | Vertical stack          | Horizontal row (flex-wrap)    |

---

## 🚀 Getting Started

No build step required. Simply open the file in a browser:

```bash
# Option 1 — open directly
open arthouse.html

# Option 2 — local server (optional, for development)
npx serve .
# or
python3 -m http.server 8080
```

> **Note:** IBM Plex Mono and Playfair Display are loaded from Google Fonts. An internet connection is required for fonts to render correctly.

---

## ✏️ Customization

### Change Accent Colors
Edit the CSS variables in `:root` inside `<style>`:
```css
--gold:  #d4a843;   /* replace with your preferred color */
--amber: #e8891a;
```

### Update Stats
Find the `<!-- STATS -->` section and change the values:
```html
<span class="stat-val">148</span>   <!-- Following -->
<span class="stat-val">69</span>    <!-- Followers -->
```

### Replace Bot Link
Find and replace all occurrences of `https://t.me/arthousexbt_bot` with your own bot URL.

### Add Ticker Items
Add `<span class="ticker-item">new text</span>` inside `.ticker-track`, then duplicate it in the second half to keep the loop seamless.

---

## 📄 License

© 2026 arthouse · All rights reserved.
