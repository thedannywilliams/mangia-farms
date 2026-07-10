# CLAUDE.md — Mangia Farms

This file is auto-loaded by Claude Code when you run `claude` in this folder. It gives the assistant context about the project and how to deploy it.

> Existing handoff doc: `README.md` — has full deploy walkthrough and domain setup. Read that for full context.

## What this is

Static brand and shop site for **Mangia Farms** (Skylar's farm). Five pages:

- `index.html` — home
- `shop.html` — pantry (1 product + 2 coming-soon placeholders)
- `about.html` — Skylar's story
- `contact.html` — contact form + market info
- `thanks.html` — form success page
- `type-options.html` — typography testing/preview page (not user-facing)

**Stack:** Vanilla HTML + one shared `styles.css` + an `img/` folder (~1.9 MB of optimized photos). No build step, no framework.

## Deployment

**Production domain:** `mangiafarms.com` (registered through Squarespace Domains)
**Netlify site:** `mangiafarms.netlify.app`
**GitHub repo:** `thedannywilliams/mangia-farms` (public) — pushes authenticate via osxkeychain credential helper

### AUTO-DEPLOY (primary workflow)

The repo is linked to Netlify for continuous deployment. To ship any change:

```bash
git add -A
git commit -m "describe the change"
git push
```

Netlify deploys automatically within ~30 seconds of push. No build command — publish directory is the repo root.

**After making edits, always commit + push (per user's standing instruction — don't ask).**

### Fallback: drag-and-drop deploy
1. Open https://app.netlify.com/drop
2. Drag the entire `MANGIA FARMS SITE` folder onto the drop zone

⚠️ Avoid mixing Drop deploys with Git deploys — a Drop deploy will be overwritten by the next push.

### Domain setup notes

The custom domain (`mangiafarms.com`) is connected via Squarespace DNS pointing to Netlify. Full domain setup steps are in `README.md`.

## When asking Claude Code in this folder

Useful prompts:
- "Deploy to production"
- "Add a new product to shop.html using the same card pattern"
- "Update the contact info on contact.html"
- "Optimize images in img/ — they're getting too heavy"
- "Add a meta description and OG tags to all pages for better social sharing"
- "What pages were modified in the last 7 days?"
