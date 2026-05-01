# jariwalamail — Coming Soon Page

A single-file, zero-dependency coming soon page for [jariwalamail.com](https://jariwalamail.com). Dark editorial luxury aesthetic with interactive animations, and an email capture form — all in one self-contained HTML file.

---

## Preview

> **Live:** [jariwalamail.com](https://jariwalamail.com)

---

## Features

- **Zero dependencies** — single `index.html` file, no build step, no npm, no framework
- **Custom cursor** — gold dot with a lagging ring; hover state on interactive elements
- **Animated grid** — golden dot-intersected grid drawn on `<canvas>` as a structural backdrop
- **Floating particles** — slow-drifting `<canvas>` particles for atmospheric depth
- **Headline shimmer** — radial light gradient follows the cursor across the display type on hover
- **Email capture** — inline validation with a success overlay; no backend required by default
- **Noise texture overlay** — CSS SVG filter grain for depth
- **Corner registration marks** — print-production-style framing details
- **Google Fonts** — Playfair Display, DM Mono, Outfit (loaded via CDN)
- **Fully responsive** — fluid `clamp()` typography scales from mobile to large displays

---

## File Structure

```
jariwalamail/
├── index.html   # The entire page — HTML, CSS, and JS in one file
└── README.md
```

---

## Getting Started

No build tools required. Just open the file.

```bash
git clone https://github.com/sahiljariwala/jariwalamail.git
cd jariwalamail
open index.html   # macOS
# or: xdg-open index.html (Linux)
# or: start index.html (Windows)
```

For a local dev server with live reload:

```bash
# Using Python (built-in)
python3 -m http.server 8000

# Using Node.js
npx serve .

# Using VS Code
# Install the "Live Server" extension, then right-click index.html → Open with Live Server
```

Then visit `http://localhost:8000/index.html`.

---

## Deployment

Since this is a single static HTML file, it deploys anywhere.

### GitHub Pages

1. Push the repo to GitHub
2. Go to **Settings → Pages**
3. Set source to `main` branch, root folder
4. GitHub will serve `index.html` by default

### Netlify (drag-and-drop)

1. Go to [netlify.com](https://netlify.com) and log in
2. Drag the project folder onto the Netlify dashboard
3. Done — live in seconds

### Netlify CLI

```bash
npm install -g netlify-cli
netlify deploy --prod --dir .
```

### Vercel

```bash
npm install -g vercel
vercel --prod
```

### Cloudflare Pages

1. Connect the GitHub repo in the Cloudflare Pages dashboard
2. Build command: *(leave blank)*
3. Output directory: `/` (root)

---

## Customization

All customization lives inside `index.html`. No config files, no environment variables.

### Brand name & tagline

```html
<!-- Top bar logo -->
<span class="logo-type">Jariwala&nbsp;Mail</span>

<!-- Eyebrow text -->
<p class="eyebrow">The Studio Behind the Icons</p>

<!-- Main headline -->
<h1 class="headline">
  Some&shy;thing<br><em>Remark&shy;able</em><br>is Coming
</h1>

<!-- Italic subline -->
<p class="subline">jariwalamail.com — est. 2025</p>

<!-- Body copy -->
<p class="description">
  A new kind of creative communication...
</p>
```

### Color palette

All colors are defined as CSS custom properties in `:root`:

```css
:root {
  --ink:        #0a0a0a;  /* page background        */
  --paper:      #f5f0e8;  /* primary text            */
  --gold:       #c9a84c;  /* accent — all highlights */
  --gold-light: #e8cc82;  /* accent — italic text    */
  --dim:        #1a1a1a;  /* secondary surfaces      */
  --mid:        #888888;  /* muted text              */
  --border: rgba(201,168,76,0.18); /* subtle borders */
}
```

Swap `--gold` / `--gold-light` to any accent ramp to re-theme the entire page.

### Email capture

By default the form shows a success message client-side only. To wire it to a backend or third-party service, replace the `handleNotify()` function:

```js
async function handleNotify() {
  const email = document.getElementById('email-input').value;
  if (!email || !email.includes('@')) { /* validation */ return; }

  // Example: POST to your own API
  await fetch('/api/subscribe', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ email }),
  });

  // Example: Mailchimp / ConvertKit / Resend via their REST API
  // await fetch('https://api.resend.com/audiences/...', { ... });

  document.getElementById('success-msg').style.display = 'flex';
}
```

### Typography

Fonts are loaded from Google Fonts. Swap the `<link>` in `<head>` and update the `font-family` declarations to change the typeface:

| Role | Current font | CSS variable |
|---|---|---|
| Display headline | Playfair Display | `font-family: 'Playfair Display', serif` |
| Monospaced labels | DM Mono | `font-family: 'DM Mono', monospace` |
| Body / UI copy | Outfit | `font-family: 'Outfit', sans-serif` |

---

## Browser Support

| Browser | Support |
|---|---|
| Chrome 90+ | ✅ Full |
| Firefox 88+ | ✅ Full |
| Safari 14+ | ✅ Full |
| Edge 90+ | ✅ Full |
| Mobile (iOS / Android) | ✅ Full — custom cursor hidden on touch |

The page uses `<canvas>`, CSS custom properties, CSS `clamp()`, and `mask-image`. All are baseline-supported in modern browsers.

---

## Performance

| Metric | Value |
|---|---|
| Page weight | ~14 KB (HTML + inline CSS/JS) |
| External requests | 1 — Google Fonts |
| JavaScript frameworks | None |
| Build step | None |

To make the page fully offline / self-hosted, download the Google Fonts stylesheet and font files and serve them locally.

---

## License

MIT — free to use, modify, and deploy for personal or commercial projects. Attribution appreciated but not required.

---

## Credits

Designed and built with intent. Inspired by the craft of agencies who've shaped visual culture for the world's most iconic brands.

> *"Good design is as little design as possible — except when it isn't."*
