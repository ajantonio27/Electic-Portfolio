# Aaron Joseph Antonio — Portfolio

A modern, responsive portfolio website showcasing frontend & backend development projects, built with vanilla HTML, CSS, and JavaScript.

## 🎯 Features

- **Dark/Light Theme Toggle** — Persists to `localStorage`, respects system preference (`prefers-color-scheme`), and follows live system changes.
- **Animated Background** — Floating dots canvas that adapts color per theme for better contrast.
- **Typing Effect** — Dynamic role text with smooth typing/deleting animation.
- **Stat Counters** — Intersection Observer triggers smooth number animations on scroll.
- **Magazine-Style Projects Grid** — Featured 1 big + 2 small cards layout, fully responsive.
- **Responsive Design** — Mobile-first breakpoints (768px, 900px, 1024px).
- **Accessibility First** — Semantic HTML, ARIA labels, keyboard navigation, theme switch with `role="switch"`.

## 📁 Project Structure

```
FINALS PORTFOLIO/
├── index.html             # Landing page with hero, stats, CTA
├── about.html             # About page with bio & skills
├── projects.html          # Projects gallery (magazine layout)
├── contact.html           # Contact form
├── style.css              # Core styles + theme variables
├── projects.css           # Projects-specific & magazine grid
├── about.css              # About page styles
├── contact.css            # Contact page styles
├── script.js              # Global JS (dots, navbar, typing, theme)
├── project.js             # Project interactions
├── README.md              # This file
└── img/                   # Images (LOGO, OPIC, project screenshots, favicon)
```

## 🚀 Getting Started

### Run Locally

Use any HTTP server to serve the folder (required for proper asset loading).

**Python 3:**
```powershell
python -m http.server 8000
# Visit http://localhost:8000/index.html
```

**Node.js (http-server):**
```bash
npx http-server .
# Visit http://localhost:8080/index.html
```

**VS Code:**
- Install the "Live Server" extension.
- Right-click `index.html` → "Open with Live Server".

## 🎨 Theme System

### How It Works
- CSS uses custom properties (`:root` variables) for dynamic theming.
- Light theme is applied via `[data-theme="light"]` attribute on `<html>`.
- Default is **dark mode**; light mode is opt-in.

### Colors

**Dark Mode (default):**
```css
--bg:      #111111;
--text:    #FAFAFA;
--accent:  #F59E0B;
--muted:   #A3A3A3;
--border:  rgba(255,255,255,0.08);
```

**Light Mode:**
```css
--bg:      #f8fafc;
--text:    #0f1724;
--accent:  #F59E0B;
--muted:   #6b7280;
--border:  rgba(15,23,36,0.06);
```

### User Preference
- Stored key: `theme-mode` in `localStorage`.
- On first visit: detects system preference with `window.matchMedia('(prefers-color-scheme: light)').matches`.
- Live follow: if no user preference is set, will adapt to system theme changes.
- Toggle button: `#theme-toggle` in navbar (icon changes moon ↔ sun).

## ♿ Accessibility

- **Semantic HTML:** `<nav>`, `<section>`, `<article>`, `<footer>` properly structured.
- **Theme Toggle:** 
  - Role: `switch`
  - Aria-pressed: Reflects current state (`true` = light, `false` = dark).
  - Title: Updates dynamically (e.g., "Switch to dark theme").
  - Icon: Marked `aria-hidden="true"` so it doesn't confuse screen readers.
- **Keyboard Navigation:** All interactive elements are natively focusable.
- **Color Contrast:** Light theme colors tuned for WCAG AA compliance.
- **Hamburger Menu:** Toggles on mobile (<768px), closes on nav link click.

## 📱 Responsive Breakpoints

| Breakpoint | Behavior |
|-----------|----------|
| 1024px ↓  | Tablet adjustments (2-col grids → 1-col) |
| 900px ↓   | About layout stacks |
| 768px ↓   | Mobile: hero shrinks, burger menu, projects full-width |
| 430px ↓   | Small phones: further font/spacing reductions |

### Magazine Grid (Projects)
- **Desktop:** Left column (big card) + Right column (2 stacked small cards).
- **Tablet (900px):** Big card full-width, small cards side-by-side.
- **Mobile (768px):** All cards full-width, stacked vertically.

## 🧪 Testing Features

### Theme Toggle
1. Open site in dark mode.
2. Click the moon icon → switches to light mode (sun icon appears).
3. Refresh page → light mode persists.
4. Clear `localStorage` → defaults to system preference.
5. Change OS theme → auto-updates if no localStorage preference.

### Floating Dots
- Dots should be light gray on light theme, white on dark theme.
- Resize window → dots reflow and re-animate smoothly.

### Typing Effect
- Hero section displays: "Web Developer | IT Student | UI/UX & Digital Marketing Enthusiast"
- Text types, pauses ~2.8s, erases, and repeats.

### Stat Counters
- Scroll to stats row → numbers animate from 0 to target.
- Uses `IntersectionObserver` to trigger only once.

## 🌐 Deployment

### GitHub Pages
1. Push this repo to GitHub.
2. Go to **Settings > Pages**.
3. Select `main` branch as source.
4. Site goes live at `https://<username>.github.io/<repo>/`.

**Note:** If deploying to a subdirectory, update asset paths (e.g., `<link href="/repo/style.css">` → `<link href="style.css">`).

### Netlify / Vercel
- Connect repo, select publish directory (root), deploy.
- Automatic builds on push.

### Self-Hosted
- Copy all files to web server.
- Ensure `img/` folder is included.
- Test in browser; all assets should load without 404 errors.

## 📝 Code Highlights

### Theme Toggle Logic (script.js)
```javascript
const THEME_KEY = 'theme-mode';
const root = document.documentElement;

function applyTheme(mode) {
    if (mode === 'light') root.setAttribute('data-theme', 'light');
    else root.removeAttribute('data-theme');
    // Update icon, aria-pressed, and title...
}

// Listen to system changes if user hasn't chosen
if (mq) mq.addEventListener('change', (e) => {
    if (!localStorage.getItem(THEME_KEY)) applyTheme(e.matches ? 'light' : 'dark');
});

// Initialize
applyTheme(localStorage.getItem(THEME_KEY) || (mq?.matches ? 'light' : 'dark'));

// Toggle on click
toggle.addEventListener('click', () => {
    const next = root.getAttribute('data-theme') === 'light' ? 'dark' : 'light';
    applyTheme(next);
    localStorage.setItem(THEME_KEY, next);
});
```

### Floating Dots Canvas (script.js)
- Creates 80 animated dots using `requestAnimationFrame`.
- Dots wrap at screen edges and fade in/out smoothly.
- Color adapts: `rgba(255,255,255,...)` on dark, `rgba(15,23,36,...)` on light.

### Magazine Grid (projects.css)
```css
.mag-grid {
    display: grid;
    grid-template-columns: 1.5fr 1fr;  /* Left: big, Right: 2 stacked */
    gap: var(--sp-3);
}
```

## 📊 Browser Support

| Browser | Status |
|---------|--------|
| Chrome 90+ | ✅ Full support |
| Firefox 88+ | ✅ Full support |
| Safari 14+ | ✅ Full support |
| Edge 90+ | ✅ Full support |
| IE 11 | ❌ CSS variables, ES6+ not supported |

## 🔮 Future Improvements

- [ ] Add analytics (Google Analytics or Plausible).
- [ ] Implement a simple contact form backend (Formspree, Netlify Forms).
- [ ] Add dark theme image variants for better contrast.
- [ ] Create project case studies with more detail.
- [ ] Add blog/articles section.
- [ ] Implement e2e testing (Cypress, Playwright).
- [ ] Add service worker for offline support.
- [ ] Optimize images with WebP + fallbacks.

## 📧 Contact

**Aaron Joseph Antonio**
- Email: ajantonio2729@gmail.com
- GitHub: [@ajantonio27](https://github.com/ajantonio27)
- LinkedIn: [aaron-joseph-78a72b350](https://www.linkedin.com/in/antonio-aaron-joseph-78a72b350/)

## 📄 License

This portfolio is open-source. Feel free to fork and customize for your own portfolio.

---


