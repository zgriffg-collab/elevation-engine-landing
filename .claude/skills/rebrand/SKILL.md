---
name: rebrand
description: Interview the owner and fill in src/brand.config.ts completely — identity, copy, colours, pricing, legal. Use when the user wants to make the template their own brand, or says "rebrand", "set up my brand", "make this mine".
---

# Rebrand this site

Turn the YourBrand placeholder site into the owner's brand by editing
`src/brand.config.ts` (and only that file, plus assets in `public/brand/`).

## Step 1 — collect the essentials

Ask for anything not already provided (one compact question list, not a
drip-feed):

1. Brand name
2. Domain (and whether the app lives at app.<domain>)
3. Support email
4. WhatsApp number for the floating contact button (or "skip")
5. Brand colour — ONE hex is enough; you derive the ramp
6. Which visual variant: original / nebula / bloom / ember / tidal (offer to
   leave the theme's own colours if they have no brand colour yet)
7. Legal entity name + country (warn: required before going live)
8. Anything they sell differently from the default copy (pricing tiers,
   audience)

## Step 2 — apply

- Fill identity, nav, hero, footer, legal fields. Rewrite copy references to
  "YourBrand" naturally with the new name (`grep -ri yourbrand src/` to
  verify none remain — the config drives all of them, so leftovers mean a
  hardcoded string that should be moved into the config).
- `theme:` — set their chosen variant.
- `colors:` — if they gave a brand colour, build a coherent light→dark ramp
  of that hue (c50 near-white tint … c900 near-black shade) and set it;
  otherwise leave `null` so the theme's own accent applies.
- Pricing/FAQ/testimonials — only change what they asked; testimonials stay
  EMPTY unless they provide real ones.
- Remind them to drop logo.svg / favicon.svg / og.svg into `public/brand/`
  (offer to generate simple SVG placeholders with their initial + colour).

## Step 3 — verify

Run `npm run build`. It must pass. Then tell them to look at
`npm run dev` and list what you changed, plus every `[SQUARE BRACKET]`
placeholder that still needs a human decision (legal entity, jurisdiction).
