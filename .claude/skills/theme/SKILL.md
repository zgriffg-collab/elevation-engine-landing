---
name: theme
description: Switch between the six visual variants or six home layouts, or design a new one (src/themes.ts / src/homeLayouts.ts). Use when the user mentions themes, variants, looks, restyling, fonts, layouts, section order, or "make it look like…".
---

# Switch or create a visual variant / home layout

## Switching

One edit in `src/brand.config.ts`:

```ts
theme: "original" | "nebula" | "bloom" | "ember" | "tidal" | "mono"
```

- original — frosted glass + drifting grid, green, Space Grotesk
- nebula — indigo/violet, solid elevated cards, Sora
- bloom — rose serif (Fraunces), soft paper cards
- ember — amber/orange, flat bordered cards, Bricolage Grotesque
- tidal — sky/cyan, crisp hairline cards, Manrope
- mono — black & white minimalism, Inter (the Linear/Notion look)

If the owner also has brand colours set (`colors:` not null), those override
the theme's accent — point that out if they expected the theme's colours.

## Creating a new variant

1. In `src/themes.ts`: add the new key to `ThemeName`, then copy the
   existing theme object closest in spirit and adjust:
   - `fonts` — display + body family and a Google Fonts `css2` URL loading
     exactly those weights (400–700 body, 500–700 display)
   - `colors` — a coherent 6-stop light→dark ramp of one hue
   - `page` — bgColor, orb/glow background-image stack, gridColor
     ("transparent" = no grid), grainOpacity (0–1)
   - `material` — card bg/border/shadows; keep blur "0px" unless you want
     the frosted-glass effect
   - `radius` — `["<large>", "<medium>"]` for card corners, or `null` to
     keep the template's per-element radii
2. Set `theme:` in brand.config.ts to the new key.
3. `npm run build` must pass; eyeball `npm run dev` on `/`, `/pricing` and
   `/guide` (the guide's theme gallery lists every theme automatically).

Keep all values plain CSS strings — no functions or imports in themes.ts.

## Home layouts (independent of theme)

One edit in `src/brand.config.ts`:

```ts
homeLayout: "classic" | "story" | "split" | "demo" | "vsl" | "compact"
```

- classic — big hero + animated inbox showcase, full section story
- story — the LONG page: adds industries, integrations and a mid-page CTA
- split — copy left / live chat demo right, features first
- demo — how-it-works right after the hero, industries next
- vsl — video hero (`hero.videoId`; styled placeholder until set), pricing early
- compact — minimal hero (no demo), short one-pager

Layouts are defined in `src/homeLayouts.ts` as `{ hero, sections[] }`. The
hero treatments ("showcase" | "split" | "video" | "minimal") and the section
components live in `src/App.tsx` (see the `SECTION_COMPONENTS` map and the
`Hero` function). To reorder/drop sections or make a new layout, edit
homeLayouts.ts only. New hero treatment = extend `HeroVariant` + add a
branch in `Hero`.

Live previews without changing config: any URL with `?theme=` / `?layout=`
(sticks for the whole browser session; the floating chip exits).
