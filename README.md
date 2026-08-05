# Systems Impact — design system

Brand tokens and shared UI, as one source of truth for every surface in the
suite. Extracted from `app-ai-interview` on 2026-08-05, which is where all of it
lived and where it was already being copied from.

## Why this is a package and not a folder per app

The platform split puts staff-facing screens in two applications at once —
`app.systems-impact.com` (team, clients, anonymization review, drop spaces) and
`interview.systems-impact.com` (campaigns, sessions, exports) — on sibling
subdomains, sharing a login. A consultant clicks between them without ever
knowing they changed application. If the token files drift, they see two
different products.

`DESIGN-SYSTEM.md` had already been copied once, into `website-SI`. Byte-identical
at extraction time, which is the only moment a copy ever is.

## What is here

| Path | What | Who consumes it |
|---|---|---|
| `DESIGN-SYSTEM.md` | The brand spec: palette, type scale, spacing, voice. Framework-agnostic — also the reference for decks, PDFs and social | everyone, including humans |
| `src/tokens.css` | The `@theme` mapping, `:root` variables, base layer and the `.eyebrow` / `.emph` component classes. Plain CSS | every app |
| `src/components/ui/` | 16 shadcn (`base-nova`) components | the Next apps |
| `src/lib/utils.ts` | `cn()` | the Next apps |

## Using it

```jsonc
// package.json
"dependencies": {
  "@systems-impact/ui": "github:Systems-Impact/SI-design#v0.1.0"
}
```

Pin the tag, not `main`: an app should adopt a design change when it chooses to,
not on its next `npm install`.

```css
/* src/app/globals.css */
@import "tailwindcss";
@import "tw-animate-css";
@import "shadcn/tailwind.css";
@import "@systems-impact/ui/tokens.css";

/* Tailwind v4 scans sources for class names; the package is outside the app
   tree, so it has to be pointed at explicitly or component classes get purged. */
@source "../../node_modules/@systems-impact/ui/src";
```

```ts
// next.config.ts — the package ships TSX source, not a build
const nextConfig: NextConfig = {
  transpilePackages: ["@systems-impact/ui"],
};
```

```tsx
import { Button } from "@systems-impact/ui/components/button";
import { cn } from "@systems-impact/ui/lib/utils";
```

The Astro website consumes `tokens.css` only; it has no React.

## Changing a component

shadcn components are normally owned and edited in place, and that assumption is
what this package trades away. The trade is deliberate: two apps rendering the
same screens matter more than local editability. So:

- **A change here lands everywhere.** Check both Next apps before tagging.
- **App-specific variants belong in the app**, composed around these primitives
  rather than forked into a second copy of them.
- Tag a version when you change anything; consumers move deliberately.
