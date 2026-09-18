# @systems-impact/ui — the Systems Impact design system

Brand tokens and shared UI components, published as one package so every surface in
the suite — `app.systems-impact.com`, `interview.systems-impact.com`, the website,
decks and PDFs — renders the same product. Extracted from the interview app on
2026-08-05, where it had already been copied from once. Consumed as a git dependency
pinned by tag.

- **Owner:** Systems-Impact · Alexandre. No one else commits here.
- **Live at:** not deployed — consumed as the tag tarball
  `https://github.com/Systems-Impact/SI-design/archive/refs/tags/vX.Y.Z.tar.gz`
- **Repo visibility:** public, deliberately — so consumers can pin a tag without
  credentials. Nothing here is sensitive: brand tokens and shadcn wrappers.

## Division of labor

Claude Code only. Cowork reads `DESIGN-SYSTEM.md` as the brand reference for decks and
documents; it never edits it here.

## Quick commands

```bash
npm install
npm run typecheck    # tsc --noEmit — the only script. No build: consumers transpile the TSX.
```

No dev server, no tests. To see a change, install the candidate in a consumer.

## Tech stack

- **Components:** 16 shadcn (`base-nova`) components on `@base-ui/react`, CVA,
  `tailwind-merge`, `lucide-react`, `sonner`, `next-themes` — all peer dependencies
- **Tokens:** `src/tokens.css` — Tailwind v4 `@theme` mapping, `:root` variables, base
  layer, `.eyebrow` / `.emph` classes. Plain CSS, no React needed to consume it
- **Consumers today:** `SI-platform` (Next), `SI-ai-interview` (Next), `SI-play` (Vite). `website-SI` carries a copy of
  `DESIGN-SYSTEM.md` on `main`; its Astro rewrite on `dev` imports `tokens.css`.
  `SI-interview-engine` does not consume this package.
- **Hosting / data / auth:** none — GitHub is the registry

## Key technical decisions (locked)

- **One package, not a folder per app.** Two staff apps on sibling subdomains share a
  login; a consultant must never see two products. Copies drift; a dependency doesn't.
- **Consumers pin a tag, never `main`.** An app adopts a design change when it chooses to.
- **Ships source, not a build.** Next consumers use `transpilePackages`; every Tailwind v4
  consumer must `@source` the package path or the component classes get purged.
- **Local editability is traded away on purpose.** shadcn components are normally owned
  by the app; here a change lands in every consumer. App-specific variants are composed
  in the app around these primitives, never forked into a second copy.
- **`DESIGN-SYSTEM.md` is framework-agnostic** — the reference for decks, PDFs and
  social as much as for code.

## Key conventions

- Component files `kebab-case.tsx`, one component per file, in `src/components/ui/`.
  New ones are added to the `exports` map in `package.json` or nobody can import them.
- Sentence case for every label and title.
- A colour, size or radius exists in `src/tokens.css` and `DESIGN-SYSTEM.md`, or it
  doesn't exist. Never hardcode one in a component.

## Reference docs

- `docs/STATUS.md` — session journal. **Read at the start of every session.**
- `DESIGN-SYSTEM.md` — the brand spec: palette, type scale, spacing, voice.
- `README.md` — consumption instructions and the change protocol.

## Guardrails

- Never change a component for one app's need. That's a variant, and it lives in the app.
- Never tag without checking every consumer: `SI-platform`, `SI-ai-interview`,
  `SI-play`.
- `website-SI` carries a copy of `DESIGN-SYSTEM.md` (byte-identical as of 2026-09-18).
  Change both in the same commit, or note the drift in `docs/STATUS.md`.

## Verifying a release

`npm run typecheck`, then point each consumer at the candidate tag and run its CI.
Tag only when all three pass.
