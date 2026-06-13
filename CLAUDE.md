# Vaultline — Due Diligence Site

## Project
Static HTML/CSS landing page. Served locally via `python3 -m http.server 8080`.
Source of truth for visual QA is **Chrome at localhost:8080**, not the VS Code live preview panel.

---

## Design System

### Colors
```
--navy:   #0b1736   (headings, nav, body text)
--accent: #2b9bd7   (trust badge border/shadow, icon strokes)
--muted:  #59607a   (paragraph / lead text)
background: #fff
```

### Spacing scale (8px base)
```
--sp-1:  8px
--sp-2: 16px
--sp-3: 24px
--sp-4: 32px
--sp-5: 48px
--sp-6: 64px
```

### Container & gutter
```css
--gutter: clamp(24px, 6vw, 80px);

.container {
  width: 100%;
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 var(--gutter);
}
```
**One gutter value, no mobile overrides.** The clamp handles all breakpoints automatically.

---

## Layout Rules

### Nav
- Uses `.nav.container` — inherits the gutter for horizontal padding
- **Never use `padding` shorthand on `.nav`** — it zeros out the container's left/right gutter
- Always use `padding-top` / `padding-bottom` separately: `var(--sp-2)` (16px each)

### Sections / Hero
- No `min-height` + `align-items: center` combo — this vertically centers content and creates a large gap above the headline on mobile
- Use `padding` (top/bottom via spacing scale) to control vertical rhythm
- Hero: `padding: var(--sp-5) 0 var(--sp-6)` (48px top, 64px bottom)

### Columns / Rows
- Use `display: flex` for rows
- Use `gap` from the spacing scale for spacing between flex children
- Never use `margin` hacks to space flex children

---

## Typography

### Headline (h1 / .hero-title)
```css
font-size: clamp(30px, 5.5vw, 56px);
font-weight: 800;
line-height: 1.15;
letter-spacing: -0.4px;
max-width: 800px;
margin: 0 auto var(--sp-3);
```
- Weight 800 (not 900/black, not 700/regular bold)
- line-height 1.15 for large display type

### Lead / paragraph
```css
font-size: clamp(15px, 1.6vw, 18px);
line-height: 1.7;
color: var(--muted);
max-width: 560px;
margin: 0 auto var(--sp-4);
```
- max-width 560px constrains line length on desktop
- Line height 1.7 for body readability

---

## Components

### Trust badge (.btn.verified)
```css
display: inline-flex;
align-items: center;
gap: var(--sp-1);
padding: 9px 18px;
border-radius: 999px;
font-weight: 500;
font-size: 14px;
```
- Small, compact pill — not full-width, not heavy weight
- Border: `rgba(43, 155, 215, 0.18)`, subtle shadow only

### Logo (nav)
```css
.logo-icon { height: 28px; width: auto; }
.logo-name { height: 18px; width: auto; }
```
- PNG assets from `/assets/`
- Never use SVG placeholders in production

---

## Rules / What Not To Do

- **No `padding` shorthand on elements that also use `.container`** — it will zero out the gutter
- **No `min-height` + `align-items: center` on hero sections** — creates unpredictable vertical gaps on mobile
- **No per-breakpoint container padding overrides** — the clamp gutter is already responsive
- **No font-size above 800 weight** — 900 looks heavy and unprofessional at display sizes
- **No font-size values above 64px max** on any headline
- **No inline padding hacks on `.lead`** — fix the container/gutter instead
- **VS Code live preview is not a design reference** — always use Chrome at localhost:8080
