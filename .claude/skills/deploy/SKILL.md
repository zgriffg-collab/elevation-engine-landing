---
name: deploy
description: Build the site and ship it to Cloudflare Pages (free hosting), either via the git-connected flow or a direct wrangler upload. Use when the user says deploy, publish, go live, or host.
---

# Deploy to Cloudflare Pages

Static site → Cloudflare Pages free tier (unlimited bandwidth, free SSL).

## Always first

```bash
npm run build   # must pass; output lands in dist/
```

## Path A — git-connected (preferred if the repo is on GitHub)

If the project is already connected in the Cloudflare dashboard, deploying
IS pushing:

```bash
git add -A && git commit -m "<what changed>" && git push
```

Cloudflare builds and deploys automatically (~1 min). If not yet connected,
walk the owner through it once — it needs THEIR browser login, you can't do
it for them: dash.cloudflare.com → Workers & Pages → Create → Pages →
Connect to Git → pick repo → framework preset **None**, build command
`npm run build`, output directory `dist`.

## Path B — direct upload (no GitHub needed)

```bash
npx wrangler pages project create <project-name>   # first time only
npx wrangler pages deploy dist --project-name=<project-name>
```

`wrangler` opens a browser window for Cloudflare login on first use — the
owner completes that themselves. The site lands on
`https://<project-name>.pages.dev`.

## Custom domain

Dashboard → the Pages project → Custom domains → Set up a domain. Add both
apex and www. If DNS is elsewhere, Cloudflare displays the CNAME to add at
the registrar. After the domain is live, make sure
`brand.config.ts → siteUrl` matches it, rebuild, redeploy (canonical + OG
tags bake the URL in).

## After deploying

Verify: fetch the live URL and check the `<title>` contains the owner's
brand name (not "YourBrand"), and spot-check `/pricing`. Report the live
URL back.
