# Systems Impact — Design System

> Single source of truth for brand, UI and visual language.
> Extracted from the production site (`index.html`). Use it for the website,
> decks / PowerPoint, PDFs, social and any future surface.

**Personality:** editorial, calm, confident. Warm paper background, near-black ink,
one warm clay accent, a deep forest green for emphasis. Serif display + clean
sans body + monospace labels. Generous whitespace. Subtle texture, never loud.

---

## 1. Color palette

### Core tokens

| Token | Hex | Role |
|---|---|---|
| `--paper` | `#FBF9F4` | Primary background (warm off-white) |
| `--paper-warm` | `#F4EFE5` | Alternate section background, cards |
| `--ink` | `#141210` | Primary text, headings, dark buttons |
| `--ink-2` | `#3A3530` | Body text, secondary text |
| `--muted` | `#8A847B` | Captions, meta, disabled |
| `--line` | `#E6E1D6` | Hairline borders, dividers |
| `--line-2` | `#D6CFBE` | Stronger borders, card edges |
| `--accent` | `#D6612A` | Primary accent — clay/terracotta (links, eyebrows, CTAs hover) |
| `--accent-d` | `#9A4419` | Accent dark (gradients, pressed states) |
| `--forest` | `#0A4E3F` | Emphasis green (italic display words, highlights) |
| `--forest-2` | `#236B5C` | Forest light (secondary green, charts) |
| `--glow` | `#FFE9D5` | Soft warm glow / tint behind accent |

### Usage rules
- **Background alternates** section by section: `--paper` → `--paper-warm` → `--paper` … for rhythm.
- **One accent at a time.** Clay `--accent` is the only "loud" color. Forest is for *emphasis*, not decoration.
- Body copy is `--ink-2`, never pure black; headings are `--ink`.
- Borders are warm greys (`--line` / `--line-2`), never cool grey.
- **Contrast:** `--ink` on `--paper` ≈ 15:1 (AAA). `--accent` on `--paper` passes AA for large text / UI — avoid clay for long body copy.

### Category accents (data, pillars, tags)
Used for color-coding categories in diagrams and dashboards:

| Category | Hex |
|---|---|
| Governance | `#3A5A8C` (blue) |
| Workflows | `#236B5C` (forest-2) |
| Information Flows | `#5B4A93` (violet) |
| Human Dynamics | `#B9842A` (amber) |
| Technology & AI | `#D6612A` (accent) |
| Economics & Incentives | `#9A4A4A` (clay-red) |

---

## 2. Typography

### Families
| Token | Stack | Use |
|---|---|---|
| `--serif` | `'Instrument Serif', Georgia, serif` | Display headings (h1–h3), brand wordmark |
| `--sans` | `'Geist', system-ui, sans-serif` | Body, UI, paragraphs |
| `--mono` | `'Geist Mono', ui-monospace, monospace` | Eyebrows, labels, nav, buttons, meta |

Google Fonts weights loaded: Instrument Serif (regular + italic), Geist 300/400/500/600, Geist Mono 400/500.

### Scale (web — fluid `clamp`)
| Element | Size | Notes |
|---|---|---|
| h1 | `clamp(2.6rem, 6.2vw, 5rem)` | Serif, weight 400, line-height 1.05, letter-spacing −0.015em |
| h2 | `clamp(2rem, 4.4vw, 3.4rem)` | Serif |
| h3 | `clamp(1.15rem, 1.6vw, 1.4rem)` | Serif |
| body `p` | `clamp(.98rem, 1.15vw, 1.05rem)` | Sans, line-height 1.7, color `--ink-2` |
| eyebrow | `.72rem` | Mono, 500, uppercase, letter-spacing .18em, color `--accent` |
| nav / btn label | `.78rem` | Mono, letter-spacing .05–.06em |

### Signature treatment
- Headings are **set in serif at weight 400** — never bold the serif.
- The **emphasis word** in a heading is *italic + forest green* (`.italic { font-style: italic; color: var(--forest) }`).
  e.g. *"We approach organizations as **living systems**."*
- **Eyebrow label** = short uppercase mono kicker above each h2, prefixed with a 24px accent rule (`──`).

### Print / slide scale (suggested, 16:9 @ 1920×1080)
| Element | Size | Use |
|---|---|---|
| Slide title | 54–72 px serif | One line, italic emphasis word allowed |
| Section divider | 96–120 px serif | Full-bleed cover slides |
| Subhead | 28–34 px sans | |
| Body / bullets | 20–24 px sans | Max ~3 bullets per slide |
| Eyebrow / kicker | 14 px mono, uppercase, tracked | Above title |
| Footnote / source | 12 px mono, `--muted` | |

---

## 3. Spacing & layout

- **Container:** max-width `1200px`, side padding `32px`. Narrow variant `780px` for text-heavy blocks.
- **Section vertical rhythm:** `padding: 130px 0` (hero `140px 0 110px`). On mobile reduce proportionally.
- **Baseline grid feel:** generous; let whitespace carry the editorial tone.
- **Z-index:** texture overlay `z:1`, content `z:2`, fixed nav `z:50`.

### Radii
| Use | Radius |
|---|---|
| Cards / panels | `18px` |
| Dashboard frame | `14px` |
| Inner tiles | `12px` |
| Buttons / pills / tags | `999px` (full) |

---

## 4. Components

### Buttons
- **Primary `.btn`:** dark fill (`--ink`), paper text, pill radius, mono `.78rem`.
  Hover → background `--accent`, lift `translateY(-1px)`, soft clay shadow.
- **Ghost `.btn--ghost`:** transparent fill, ink text, `--ink` border.

### Nav (fixed header)
- Translucent paper `rgba(251,249,244,.78)` + `backdrop-filter: blur(14px)`.
- Bottom hairline appears on scroll (`.scrolled` → `border-bottom: --line`).
- Links: mono, **lowercase**, letter-spacing .06em, hover → `--accent`.
- Brand mark: 22px radial clay dot with pulsing animation + double paper/accent ring.

### Cards
- Background `--paper` or `--paper-warm`, `1px solid --line` (or `--line-2`), radius `18px`.
- Hover: lift + soft warm shadow `0 12px 32px -14px rgba(10,78,63,.12)` (forest-tinted) or ink-tinted on neutral cards.
- **No drop shadow on the dashboard frame** — border only (shadows read dirty on warm paper).

### Eyebrow + section head
```
[── RECOGNIZABLE PATTERNS]        ← mono accent eyebrow with leading rule
What leaders tell us most often   ← serif h2, optional italic emphasis word
```

### Tags / pills
Full-radius, mono micro-label. Category tags use the category accent colors above.

### Data / dashboard panels
- Frame: `--paper`, `1px solid --line-2`, radius `14px`, **no shadow**.
- Category color applied via `--cat` custom property → 3px top border + colored dot before label.
- Status chips: `.live` (active) / `.soon` (muted, upcoming).

---

## 5. Motion

- **Easing:** `ease` / `ease-in-out`, durations `.25s`–`.3s` for UI, `3–3.6s` for ambient (brand pulse).
- **Scroll reveals:** panels fade + rise (`.dp` → `.show`), staggered top-to-bottom one by one.
- **Hover:** `translateY(-1px)` lift + shadow on buttons/cards.
- **Always respect `prefers-reduced-motion`** — disable reveal/animation.
- Keep motion subtle; nothing bounces or spins.

---

## 6. Texture & finish

- Full-viewport **fractal-noise grain** overlay: SVG `feTurbulence`, opacity `.32`, `mix-blend-mode: multiply`, dark-warm tint. Adds paper feel without visible noise.
- For slides/print: a very light paper grain or flat warm fill both work; keep it subtle.

---

## 7. Voice & content

- **Tone:** clear, senior, no hype. Short declaratives.
- **Headline pattern:** plain statement + one *italic forest* emphasis word.
- **Eyebrows:** 2–3 words, uppercase, category-like ("Recognizable patterns", "The Engine").
- Trademark terms: *The Systems Impact Engine™*, *Systems Impact Model™*.
- Sentence case for headings (not Title Case); lowercase for nav.

### Punctuation — em dashes
- **Never use the em dash (`—`) anywhere in copy or UI.** Not in prose, labels, captions, aria-labels or table cells.
- Replace it with the right alternative:
  - **In prose:** a comma, a colon, or split into two sentences (whichever reads cleanest).
  - **As a label separator** (e.g. "Flow map — outbound"): use a middot ` · `.
  - **As a "flat / no change" indicator** in data: use `→`, not `—`.
- The en dash (`–`) is also avoided in prose; use it only for true numeric ranges if unavoidable.

---

## 8. Presentation / PowerPoint quick kit

**Theme colors (set in Slide Master → Theme):**

| Slot | Hex |
|---|---|
| Background 1 (light) | `#FBF9F4` |
| Background 2 (alt) | `#F4EFE5` |
| Text 1 (dark) | `#141210` |
| Text 2 | `#3A3530` |
| Accent 1 | `#D6612A` |
| Accent 2 | `#0A4E3F` |
| Accent 3 | `#236B5C` |
| Accent 4–6 | `#3A5A8C` · `#5B4A93` · `#B9842A` |

**Fonts:** Headings = *Instrument Serif*; Body = *Geist*; Labels/numbers = *Geist Mono*.
(If unavailable on the deck machine: Georgia for serif, Arial/Inter for sans, any mono for labels.)

**Slide patterns:**
- **Cover:** warm paper bg, large serif title with one italic forest word, mono eyebrow above, clay dot mark.
- **Section divider:** `--paper-warm` bg, giant serif number/word, minimal.
- **Content:** left-aligned, eyebrow → title → ≤3 bullets (sans), lots of margin.
- **Data:** category colors for series; 3px colored top-rule on stat cards; mono for numbers.
- **Footer:** mono micro-label + page number in `--muted`, left/right aligned.

**Do**
- Use one accent per slide; forest for emphasis only.
- Keep ≥40% of each slide as whitespace.
- Align everything to a single left margin.

**Don't**
- No pure black, no cool greys, no gradients except the brand dot.
- No bold serif, no Title Case headings, no drop shadows on panels.
- No more than ~3 colors on a single data slide.

---

## 9. Token cheat-sheet (copy/paste)

```css
:root{
  --paper:#FBF9F4; --paper-warm:#F4EFE5;
  --ink:#141210; --ink-2:#3A3530; --muted:#8A847B;
  --line:#E6E1D6; --line-2:#D6CFBE;
  --accent:#D6612A; --accent-d:#9A4419;
  --forest:#0A4E3F; --forest-2:#236B5C; --glow:#FFE9D5;
  --serif:'Instrument Serif',Georgia,serif;
  --sans:'Geist',system-ui,sans-serif;
  --mono:'Geist Mono',ui-monospace,monospace;
}
```

Category accents: `#3A5A8C #236B5C #5B4A93 #B9842A #D6612A #9A4A4A`
